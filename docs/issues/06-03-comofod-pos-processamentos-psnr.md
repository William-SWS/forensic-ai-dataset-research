# 06-03 CoMoFoD: pós-processamentos e PSNR

**Status:** concluído
**Notebook:** `notebooks/02_eda_comofod.ipynb`, seção 3
**Depende de:** 06-01

## Por que

Boa parte do valor do CoMoFoD é medir a **robustez** de um detector a degradações (brilho, contraste, redução de cor, desfoque, ruído, compressão JPEG). O arquivo `psnr.txt` quantifica a degradação de cada variante, mas não está documentado quais variantes ele cobre. É preciso conhecer essa cobertura antes de usá-lo.

## O que fazer

- Ler o `psnr.txt` e juntá-lo ao inventário do ticket 06-01.
- Resumir o PSNR por pós-processamento e nível (mediana).
- Verificar quais tipos de arquivo (`O`, `F`, que pós-processamentos) o `psnr.txt` cobre e quais ficam de fora.

## Fora do escopo

- Reavaliar o PSNR com outra métrica ou recalcular a partir dos pixels.

## Critérios de aceite

- [x] O notebook imprime o número de linhas do `psnr.txt` e quantas não têm correspondência no inventário (esperado: 0; se não for, listar).
- [x] Uma tabela mostra a mediana do PSNR por pós-processamento (linhas) e nível (colunas).
- [x] Uma frase informa a cobertura real do `psnr.txt` (por exemplo, "cobre apenas as variantes de `O`") e quantas das variantes esperadas não têm PSNR, calculado a partir dos dados.
- [x] As variantes JPEG (JC, 9 níveis) são tratadas explicitamente, mesmo que o PSNR cubra só parte delas.

## Notas

- Se o `psnr.txt` cobrir só um dos lados (`O` ou `F`), não extrapolar para o outro: registrar como limitação.

## Resultado (2026-10-15)

- `psnr.txt` tem 600 linhas, 0 sem correspondência no inventário. **Cobre só ruído (NA, 3 níveis) sobre originais (`O`)**: 600 de 9.600 variantes pós-processadas (6,25%). BC, CA, CR, IB e JC, e todas as variantes de `F`, ficam sem PSNR (incluindo as 1.800+1.800 de JPEG).
- Mediana do PSNR do ruído: 20,7 dB (nível 1), 23,1 (nível 2) e 33,0 (nível 3).
- Limitação registrada: não se extrapola o PSNR de `O` para `F`.
