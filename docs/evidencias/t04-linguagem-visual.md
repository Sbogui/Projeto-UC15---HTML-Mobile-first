# T04 — Linguagem visual e movimento acessível

## Alterações realizadas

- Aplicação de gradiente decorativo no cabeçalho, utilizando as cores roxas do tema.
- Transições suaves nos estados dos botões.
- Uso de `transform` para indicar interação sem alterar o fluxo do documento.
- Respeito à preferência `prefers-reduced-motion`, removendo os deslocamentos dos botões.
- Preservação do indicador de foco visível para navegação por teclado.
- Manutenção da identidade visual escura, roxa e amarela.

## Verificação de contraste

| Combinação | Contraste |
|---|---:|
| Texto principal / fundo escuro | 16,60:1 |
| Texto principal / cartões | 15,19:1 |
| Texto escuro / botão amarelo | 12,09:1 |
| Texto escuro / botão em hover | 14,49:1 |
| Texto desabilitado / fundo desabilitado | 6,09:1 |
| Borda dos campos / fundo escuro | 5,51:1 |
| Foco amarelo / fundo escuro | 12,09:1 |

As combinações avaliadas atendem aos limites usuais de contraste da WCAG para os respectivos usos.

## Testes manuais

- [x] Gradiente do cabeçalho visível.
- [x] Botão muda de aparência ao passar o mouse e ao clicar.
- [x] Indicador de foco visível durante a navegação por teclado.
- [x] Informações compreensíveis sem depender exclusivamente de cor ou movimento.
- [x] Movimento reduzido respeitado, sem deslocamento dos botões.

**Resultado:** testes visuais aprovados. Evidências registradas em 16/10/2026.