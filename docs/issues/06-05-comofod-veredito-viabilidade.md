# 06-05 CoMoFoD: veredito de viabilidade e registro

**Status:** concluído
**Notebook:** `notebooks/02_eda_comofod.ipynb`, seção final
**Depende de:** 06-02, 06-03, 06-04, 06-06

## Por que

A EDA só cumpre seu objetivo se terminar em um julgamento por base: **a base sustenta um modelo de IA útil?** O veredito deve usar apenas números medidos nos tickets anteriores e alimentar o **datasheet** do CoMoFoD (ticket 07). No Loghub o veredito está na seção 3 do `01_eda_loghub.ipynb`; este ticket faz o equivalente.

## O que fazer

- Escrever uma célula final de veredito com: escala efetiva (200 cenas, que vêm de 41 fotografias distintas; ver 06-06), significado e qualidade das máscaras (06-02), robustez e cobertura do PSNR (06-03), desempenho do baseline e tamanho do vazamento (06-04), riscos e limites.
- Registrar o resultado em `docs/decisions.md` (nova entrada ao fim).
- Registrar as condições de uso do *release agreement* no veredito (uso acadêmico, sem redistribuir, imagens não modificadas, citar Tralić et al. 2013).

## Fora do escopo

- O datasheet em si (ticket 07).
- Comparar com outras bases de imagem (CASIA v2, DEFACTO), que ficaram fora do trio.

## Critérios de aceite

- [x] Cada afirmação do veredito cita um número que aparece na saída de uma célula anterior do mesmo notebook. Hipóteses não testadas são marcadas como tal.
- [x] O veredito diz explicitamente que as 10.400 imagens vêm de 200 cenas e de **41 fotografias** (ticket 06-06) e o que isso significa para a divisão treino/teste.
- [x] O veredito inclui a limitação de que o baseline usa características globais e não mede localização.
- [x] O notebook inteiro executa do zero, sem erro (`jupyter nbconvert --execute`), e o tempo de execução é registrado.
- [x] `docs/decisions.md` ganha uma entrada com os números principais e remete ao notebook.
- [x] Nenhuma imagem da base é copiada para fora de `data/interim/` nem incluída no repositório.

## Notas

- O CoMoFoD é pequeno demais para treinar um modelo profundo do zero; o valor realista é **benchmark de robustez** e teste de transferência. Isso é uma hipótese de leitura até os números sustentarem.

## Resultado (2026-10-15)

- Veredito na seção 5 do notebook, com números das saídas. Conclusão: características globais simples não são viáveis (AUC 0,495 por fotografia); 41 fotografias é pouco para treinar; valor realista como benchmark de robustez e teste de transferência (hipótese de uso).
- O notebook executa do zero sem erro (`nbconvert --execute`), em 2 min 33 s, com 1 figura (histogramas, sem imagens da base).
- Nenhuma imagem da base é copiada para fora de `data/interim/` nem aparece na saída do notebook (figura de exemplo desligada).
- Entrada correspondente em `docs/decisions.md`.
