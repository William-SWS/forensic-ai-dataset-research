# 06-01 CoMoFoD: inventário e integridade da base

**Status:** concluído
**Notebook:** `notebooks/02_eda_comofod.ipynb`, seção 1
**Depende de:** download do CoMoFoD Small (decisão 17, feito) e ambiente (decisão 18, feito). A extração para `data/interim/comofod/` já foi feita.

## Por que

Antes de qualquer análise é preciso saber que a **base bruta** está inteira e como ela se organiza. O CoMoFoD distribui 200 conjuntos de imagens (aqui chamados de **cena**; veja 06-06: não são independentes) e um `readme.txt` que classifica cada cena por tipo de manipulação. Sem esse inventário, o resto da EDA repousa em suposições sobre a estrutura.

## O que fazer

- Ler `data/interim/comofod/CoMoFoD_small_v2/` e interpretar cada nome de arquivo (`<cena>_<tipo>[_<pós><nível>].<ext>`) em uma tabela: cena, tipo (`O` original, `F` falsificada, `B` e `M` máscaras), pós-processamento (BC, CA, CR, IB, JC, NA), nível, extensão, bytes.
- Conferir a estrutura esperada por cena (52 arquivos: 4 imagens-base mais, para `O` e para `F`, 3 níveis de BC, CA, CR, IB e NA e 9 níveis de JC).
- Ler o `readme.txt` e atribuir a cada cena uma das cinco categorias (translação, rotação, escala, distorção, combinação) e a área da região copiada.

## Fora do escopo

- Qualquer leitura de pixels (ticket 06-02).
- Regravar ou modificar imagens: o *release agreement* proíbe alterar as imagens baixadas.

## Critérios de aceite

- [x] O notebook roda do zero e imprime: número de arquivos de imagem, número de cenas, quantidade de arquivos fora do padrão de nome e tamanho total em GB.
- [x] Um `assert` (ou verificação equivalente que falhe de forma visível) confirma que toda cena tem exatamente 52 arquivos e a composição esperada por tipo e pós-processamento. O resultado esperado é 10.400 arquivos de imagem, e a contagem real medida é registrada.
- [x] A tabela de categorias do `readme.txt` soma 200 cenas, e as cenas sem categoria (se houver) são listadas.
- [x] As contagens por categoria impressas são conferidas contra o `readme.txt` (a leitura manual dos cabeçalhos sugere 40, 40, 40, 39 e 41; confirmar, não assumir).

## Notas

- O Small tem 200 conjuntos de 512x512; o Large (3000x2000, 60 conjuntos) só é distribuído por contato e está fora do estudo.
- O `readme.txt` tem formatos irregulares (por exemplo `3540[2256]S80`, `(2)`, `*`). Extrair só o que for confiável (categoria e primeiro número) e registrar o que não for.

## Resultado (2026-10-15)

- 10.400 arquivos de imagem, 200 cenas, 0 fora do padrão de nome, 3,21 GB. Todas as cenas têm 52 arquivos; um `assert` no notebook falha se isso mudar.
- Categorias (soma 200, nenhuma cena sem categoria): COMBINATION 41, TRANSLATION 40, ROTATION 40, SCALING 40, DISTORTION 39. A área da região copiada vai de 360 a 37.542 px (mediana 3.369), de 262.144.
- Notebook: `notebooks/02_eda_comofod.ipynb`, seções 1 e 1.1.
