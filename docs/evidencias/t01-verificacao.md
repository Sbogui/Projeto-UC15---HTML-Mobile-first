# Verificação do T01

- Data: 16/10/2026
- Commit verificado: `9a30903` (branch main)
- Arquivo verificado: `prototipo/index.html`
- Sistema: Windows

## Aceite do T01

Conteúdo compreensível sem CSS, navegação acionável sem JavaScript e zoom permitido.

## 1. Conferência automática

Script PowerShell sobre o HTML. Estrutura esperada e encontrada:

| Elemento | Esperado | Encontrado |
|---|---|---|
| `<h1>` | 1 | 1 |
| `<h2>` | 5 | 5 |
| `<h3>` | 3 | 3 |
| `<header>` | 1 | 1 |
| `<nav>` | 1 | 1 |
| `<main>` | 1 | 1 |
| `<footer>` | 1 | 1 |
| `<section>` | 5 | 5 |
| `<article>` | 3 | 3 |
| `<table>` | 2 | 2 |
| `<form>` | 1 | 1 |
| `<label>` | 1 | 1 |
| `<ul>` | 2 | 2 |
| `<button>` | 1 | 1 |

Recursos que não devem existir (o conteúdo vem antes de CSS e JavaScript, e o zoom não é bloqueado):

| Padrão | Esperado | Encontrado |
|---|---|---|
| `<script` | 0 | 0 |
| `<style` | 0 | 0 |
| `rel="stylesheet"` | 0 | 0 |
| `maximum-scale` | 0 | 0 |
| `user-scalable` | 0 | 0 |

Referências internas (`href="#..."`, `for`, `aria-labelledby` e `aria-describedby`): 15 encontradas, 0 sem alvo.

## 2. Testes manuais (resultado informado pelo autor)

| Teste | Resultado |
|---|---|
| Leitura sem CSS | Todas as seções têm conteúdo e o portal se entende só lendo |
| Navegação por teclado (Tab) | 10 paradas: link de pular, 5 links do menu, 2 links do destaque, campo de e-mail e botão |
| Zoom e modo celular | O autor informou que a página funcionou sem problemas |

## 3. Conclusão por critério de aceite

| Critério | Evidência | Situação |
|---|---|---|
| Conteúdo compreensível sem CSS | Nenhum `<style>` nem stylesheet; teste de leitura | Atendido |
| Navegação acionável sem JavaScript | Nenhum `<script>`; 10 paradas de Tab | Atendido |
| Zoom permitido | Sem `maximum-scale` nem `user-scalable`; zoom testado | Atendido |

## Limitações conhecidas

- A largura da tabela do placar em telas estreitas não foi medida neste teste. O tratamento está previsto no CSS (T03 e T05).
- O envio do formulário apenas recarrega a página. A mensagem de resultado vem com o JavaScript (T07).
- Ainda não houve teste em celular real. Ele entra no T05.
