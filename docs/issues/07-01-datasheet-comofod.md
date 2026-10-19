# 07-01 CoMoFoD: datasheet

**Status:** concluído
**Arquivo:** `docs/datasheets/comofod.md`
**Depende de:** 06-05 (veredito de viabilidade) e decisão 16 (termos aceitos)

## Por que

O entregável 1 do projeto é um datasheet por base, com origem, volume, rótulos, licença, acesso e riscos. No CoMoFoD, as condições de uso do *release agreement* estavam repetidas em quatro lugares (`docs/decisions.md` entrada 16, `README.md`, `docs/relatorio-andamento.md` e o notebook 02), sempre resumidas, e três cláusulas não estavam em nenhum deles: a base vem sem garantia, os donos podem mudar os termos a qualquer momento e o uso é gratuito. O datasheet passa a ser **o único lugar com o texto completo dos termos**; os demais documentos apontam para ele.

## O que fazer

- Criar `docs/datasheets/comofod.md` com: origem e citação, acesso, composição e estrutura, rótulos, números medidos na EDA, riscos e limitações, usos recomendados e não recomendados, termos de uso.
- Na seção de termos, transcrever o *release agreement* na íntegra, com o link e a data da leitura, e traduzir cada cláusula em uma regra prática para o projeto.
- Trocar os resumos dos termos no `README.md` e no `docs/relatorio-andamento.md` por um resumo curto mais o link para o datasheet.
- Conferir se a apresentação em `docs/presentations/` contém alguma imagem da base.

## Fora do escopo

- Datasheets das outras três bases (tickets futuros 07-02 a 07-04).
- Novas medições: o datasheet só usa números que já saem do notebook 02.

## Critérios de aceite

- [x] O datasheet traz o *release agreement* completo, o link e a data da leitura (2026-10-15).
- [x] As cláusulas que faltavam (sem garantia, termos revisáveis, uso gratuito) estão registradas, com o efeito de cada uma no projeto.
- [x] Cada número do datasheet aparece na saída do notebook 02 ou nos tickets 06-01 a 06-06.
- [x] `README.md` e `docs/relatorio-andamento.md` apontam para o datasheet.
- [x] Nenhuma imagem da base entra no datasheet nem no repositório.

## Resultado (2026-10-18)

- Datasheet em `docs/datasheets/comofod.md`.
- `README.md` e `docs/relatorio-andamento.md` passam a ter só um resumo de uma linha e o link.
- Apresentação conferida: as 45 imagens embutidas no `.pptx` são logotipos (UECE, LARCES) e ícones; nenhuma vem do CoMoFoD.
- Entrada correspondente em `docs/decisions.md`.
