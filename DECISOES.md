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
