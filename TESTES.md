# Matriz de testes responsivos — T05

## Objetivo

Verificar a adaptação do protótipo Copa Senac Hackathon a diferentes
larguras de tela, preservando a legibilidade e o acesso ao conteúdo.

## Resultados dos testes visuais

| Largura | Condição verificada | Resultado |
|---|---|---|
| 320 px | Menu, textos, cartões, tabelas e formulário | Aprovado |
| 375 px | Layout de celular e legibilidade | Aprovado |
| 640 px | Reorganização do conteúdo em largura intermediária | Aprovado |
| 1024 px | Distribuição do conteúdo em tela ampla | Aprovado |
| 1440 px | Layout em desktop | Aprovado |

Os testes visuais nas larguras acima foram realizados no navegador.
Não foram identificados problemas visuais durante a verificação.

## Recursos responsivos implementados

- Tipografia fluida com `clamp()`.
- Media queries orientadas pelo espaço disponível.
- Container query para os cartões de notícias.
- Rolagem horizontal nas áreas das tabelas, sem ocultar colunas.
- Quebra de textos longos e adaptação dos espaçamentos.

## Verificações complementares

| Condição | Situação |
|---|---|
| Zoom de 200% | Pendente de confirmação específica |
| Orientação retrato e paisagem | Pendente de confirmação específica |
| Navegação completa por teclado | Pendente de confirmação específica |
| Teclado virtual em celular | Pendente de confirmação específica |
| Teste em celular físico | Pendente |

## Critérios de aceite

- [x] A página foi verificada em diferentes larguras de tela.
- [x] Não foram identificados problemas visuais nos testes realizados.
- [x] O conteúdo das tabelas permanece acessível por rolagem horizontal.
- [x] Não foram ocultadas informações apenas para acomodar telas menores.
- [ ] Verificações complementares e teste em dispositivo físico.
