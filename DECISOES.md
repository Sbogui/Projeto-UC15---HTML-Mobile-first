# Decisões do projeto

Registro das decisões técnicas e de produto da Copa Senac Hackathon. Cada entrada diz o que foi decidido, por que e o que ficou de fora.

## D01 — Tema e modalidade

- **Decisão:** hackathon fictício, a Copa Senac Hackathon, com equipes, rodadas e placar geral.
- **Por quê:** o tema cobre o produto mínimo (home, notícias, cronograma, placar, filtro, formulário) sem depender de dados reais.
- **Fora:** eventos reais, marcas e logotipos de terceiros.

## D02 — Licença

- **Decisão:** todos os direitos reservados (arquivo `LICENSE`).
- **Por quê:** escolha do autor para o trabalho acadêmico.
- **Observação:** Bootstrap e jQuery, quando entrarem, mantêm suas licenças MIT, com origem e licença documentadas.

## D03 — Estrutura de pastas

- **Decisão:** o protótipo fica em `prototipo/` (`index.html`, `assets/`, `js/`). As demais pastas previstas (`docs/`, `wordpress/tema-filho/`, `tests/`) e os arquivos `TESTES.md` e `CMS.md` são criados quando a tarefa correspondente começar.
- **Por quê:** o Git não versiona pastas vazias, e arquivos sem conteúdo escondem o que ainda não foi feito.

## D04 — Sem framework no início

- **Decisão:** HTML, CSS e JavaScript escritos à mão até o T05. Bootstrap entra no T06 e jQuery no T08, com justificativa.
- **Por quê:** o projeto compara a solução própria com a de framework, então precisa existir primeiro a solução própria.

## D05 — Viewport sem bloquear zoom

- **Decisão:** `<meta name="viewport" content="width=device-width, initial-scale=1">`, sem `maximum-scale` e sem `user-scalable=no`.
- **Por quê:** sem a linha, o celular desenha a página em uma largura virtual de desktop (cerca de 980px) e encolhe tudo. Bloquear o zoom prejudica quem precisa ampliar o texto (WCAG 1.4.4).
- **Como verificar:** modo dispositivo móvel do DevTools. Com a linha, a página ocupa a largura da tela, e o zoom continua permitido.

## D06 — Formulário de novidades: fallback e melhoria progressiva

- **Fallback (piso):** `<form>` com `label` ligado ao campo, `type="email"` e `required`. O navegador valida o formato e envia sem JavaScript. O envio recarrega a página na seção `#novidades`.
- **Melhoria progressiva (T07):** o JavaScript vai interceptar o envio, impedir o recarregamento e escrever a mensagem de resultado em `<p role="status">`. Sem JavaScript, o formulário continua funcionando como no piso.
- **Por quê:** a base precisa funcionar para qualquer navegador, e o JavaScript acrescenta conforto sem ser condição para usar.
- **Limite conhecido:** não há servidor. O método `get` coloca o e-mail na URL, o que só é aceitável como demonstração local, sem dados reais.

## D07 — Paleta e tipografia

- **Decisão:** paleta violeta e verde (opção B, entre três avaliadas), fontes do sistema (`system-ui` e alternativas) e escala em `rem` a partir de 16px: 0,875 (apoio), 1 (texto), 1,25 (h3), 1,5 (h2) e 2 (h1). Tudo declarado como custom properties em `:root`, em `prototipo/assets/styles.css`.
- **Contraste (fórmula da WCAG):** texto sobre o fundo 15,9; texto suave 8,0; primária 6,4; branco sobre a primária 6,8; destaque verde 4,8; erro 6,1; borda de campo 5,0. O mínimo é 4,5 para texto e 3 para bordas de campo.
- **Por quê:** o azul e o laranja ficaram de fora para não imitar a identidade do Senac (README). As fontes do sistema dispensam arquivos externos, funcionam offline e não custam requisição. O `rem` acompanha a fonte configurada pela pessoa.
- **Como verificar:** DevTools, seletor de cor de uma regra (mostra a razão de contraste), e troca de um token em `:root` para ver o efeito em toda a página.
- **Fora:** modo escuro (previsto, se couber, depois do T04) e fontes externas.

## D08 — Estados interativos e origem de uma regra

| Estado | Regra | Sinal além da cor |
|---|---|---|
| Normal | `button` com fundo `--cor-primaria` e texto branco; alvo mínimo de 2,75rem | Tamanho do alvo |
| Hover | `a:hover` e `button:not(:disabled):hover` | Sublinhado de 2px no link; botão mais escuro |
| Foco | `:focus-visible` com anel de 3px e deslocamento de 2px | Anel contínuo |
| Ativo | `button:not(:disabled):active` | O botão desce 1px (`transform`) |
| Inválido | `input:user-invalid` | Borda de 3px (só depois da interação) |
| Desabilitado | `button:disabled` e `input:disabled` | Cursor `not-allowed` e borda tracejada no campo |

- **Origem de uma regra:** o anel de foco do cabeçalho. A regra base `:focus-visible` (especificidade 0,1,0) usa a cor primária, que some no cabeçalho violeta. A regra `header :focus-visible` (0,1,1) troca só a cor do anel para branco e vence pela especificidade, sem `!important`. No DevTools, a regra base aparece riscada.
- **Por quê:** o foco nunca é removido, nenhuma informação depende só de hover, e `:user-invalid` evita pintar o formulário de erro antes da primeira tentativa.
- **Limite conhecido:** o texto de uma mensagem de erro vem do balão do navegador e, no T07, da região `role="status"`. Por enquanto, o estado inválido só muda a aparência do campo.

## D09 — Unidades e seletores

| Uso | Unidade | Por quê |
|---|---|---|
| Fonte, espaços, alvos (2,75rem) e raio de borda | `rem` | Acompanha a fonte configurada pela pessoa. Zoom e preferência de fonte ampliam o layout junto |
| Largura de leitura dos parágrafos | `ch` | Mede em caracteres (65), independente do tamanho da fonte |
| Largura do conteúdo | `rem` (60rem) e `%` | O limite acompanha a fonte, e o `%` deixa o conteúdo fluido abaixo do limite |
| Bordas e anel de foco (1px, 2px e 3px) | `px` | Traços devem manter espessura fixa e nítida, e não crescem com a fonte |
| Altura de linha | número sem unidade (1,5 e 1,25) | Herda proporcional ao tamanho de cada elemento. Uma unidade fixa quebraria nos títulos |
| Movimento | `ms` | Duração é tempo, não distância. Zerada em `prefers-reduced-motion` |
| Alinhamento do cabeçalho com o conteúdo | `max(1rem, calc((100% - 60rem) / 2))` | Combina um mínimo fixo com uma medida fluida |

**Seletores complexos e pseudo-elementos, com a função de cada um:**

- `main > section:first-of-type`: o destaque é sempre a primeira seção do conteúdo (contrato do HTML). Se a ordem mudar, o estilo muda junto. Quando houver variações, passa a usar classe.
- `tbody tr:nth-child(even)`: zebra por posição, só apresentação.
- `button:not(:disabled):hover`: só controles ativos reagem ao ponteiro.
- `::marker`: cor do marcador da lista do destaque. Não gera conteúdo.
- `::selection`: legibilidade do texto selecionado, branco sobre `#4A32B0` (contraste 8,8).
- **Regra comum:** nenhum pseudo-elemento usa `content`. Se não carregar, nada se perde.

## D10 — Link de pular

- **Decisão:** o primeiro elemento da página é `<a class="pular" href="#conteudo">`, uma barra fina, sempre visível, no fluxo, acima do cabeçalho. O texto usa a mesma margem lateral do cabeçalho (`max(1rem, calc((100% - 60rem) / 2))`) e fica alinhado ao título.
- **Alternativas descartadas:** caixa flutuando sobre o cabeçalho, link escondido até receber foco e caixa solta no canto. A primeira cobria o título, a segunda deslocava a página no primeiro `Tab`, e a terceira ficava desalinhada do resto. A escolha final é do autor.
- **Por quê:** o primeiro anel de foco era cortado pela borda da janela (o link estava no canto 0,0).
- **Origem de uma regra:** `.pular:focus-visible` (0,2,0) vence a regra base `:focus-visible` (0,1,0) e muda só o `outline-offset` para `-3px`, que desenha o anel dentro da barra. Sem `!important`.

## D11 — Tema escuro, roxo e amarelo (substitui a paleta do D07)

- **Decisão:** tema escuro com roxo escuro no fundo (`#14101F`), no cabeçalho (`#2D1B69`) e nos cartões (`#1E1830`), e amarelo (`#FFC83D`) como cor de contraste para links, títulos `h2`, anel de foco, marcadores e botão. `color-scheme: dark` em `:root`.
- **Contraste (fórmula da WCAG):** texto claro sobre o fundo 16,6 e sobre o cartão 15,2; texto suave sobre o cartão 8,8; amarelo sobre o fundo 12,1, sobre o cartão 11,1 e sobre o cabeçalho 9,2; texto escuro sobre o botão amarelo 12,1; borda de campo sobre o cartão 5,0; erro sobre o cartão 8,4. O mínimo é 4,5 para texto e 3 para bordas de campo.
- **O que muda nas decisões anteriores:** a paleta violeta e verde do D07 deixa de valer (escala tipográfica, fontes do sistema e `rem` continuam). No D08, o anel de foco único em amarelo dispensa a regra `header :focus-visible` (o amarelo contrasta com o cabeçalho roxo), que foi removida. A origem de uma regra passa a ser a do D10.
- **Por quê:** preferência do autor por um visual escuro, com o amarelo concentrando a atenção nas ações. O azul e o laranja continuam de fora para não imitar a identidade do Senac.
- **Fora:** alternância entre tema claro e escuro (`prefers-color-scheme`) ou controle manual. Fica como possibilidade futura.

## D12 — Bootstrap 5.3.8 com customização controlada

- **Decisão:** usar Bootstrap 5.3.8 com CSS e bundle JavaScript armazenados em `prototipo/assets/vendor/bootstrap-5.3.8/`. A licença MIT acompanha os arquivos em `LICENSE`. A versão é fixa para manter o comportamento previsível.
- **Uso:** grid de notícias com `row`, `row-cols-*` e `g-3`; breakpoint `lg` para a navegação responsiva; offcanvas para o menu mobile; modal para informações da Copa.
- **Tema:** as cores do projeto continuam definidas pelos tokens CSS próprios. As customizações de botão, menu e modal ficam em seletores e variáveis específicas, sem editar os arquivos originais do Bootstrap nem sobrescrever globalmente seus componentes.
- **Comparação com a solução anterior:** a grade de notícias era feita com CSS Grid e `auto-fit`; agora as colunas usam as classes responsivas do Bootstrap. O CSS próprio continua responsável pela identidade visual, tabelas responsivas, tipografia e regras específicas do conteúdo.
- **Custos e limitações:** os arquivos locais adicionam aproximadamente 232 KB de CSS e 80 KB de JavaScript minificados ao repositório. A hospedagem local permite carregar os componentes sem depender de CDN durante a execução. A equipe passa a manter a versão e a licença desses arquivos. O bundle Bootstrap 5 não exige jQuery.
- **Acessibilidade a validar:** testar navegação por teclado, foco, fechamento do menu e do modal, tecla `Esc`, leitor de tela e larguras próximas ao breakpoint de 992 px.
- **Referências:** https://getbootstrap.com/docs/5.3/components/offcanvas/ ; https://getbootstrap.com/docs/5.3/components/modal/ ; https://getbootstrap.com/docs/5.3/layout/grid/
