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