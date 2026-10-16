# 06-02 CoMoFoD: o que as máscaras marcam e o tamanho da região adulterada

**Status:** concluído
**Notebook:** `notebooks/02_eda_comofod.ipynb`, seção 2
**Depende de:** 06-01

## Por que

A base serve a **localização** de falsificação, então a qualidade e o significado das máscaras decidem se ela sustenta um modelo. Cada cena traz duas máscaras (`B` binária e `M` colorida) cujo conteúdo não está documentado. A leitura visual de uma cena sugere que `B` marca a região de origem **e** a região colada, mas isso é uma hipótese a medir.

## O que fazer

- Para as 200 cenas, comparar `O` e `F` (pixels em que diferem) com a máscara `B`: cobertura da diferença dentro da máscara e IoU.
- Medir a fração da imagem marcada em `B` e a distribuição por categoria de manipulação.
- Comparar o tamanho da região do `readme.txt` com a área marcada em `B`.
- Registrar o formato das imagens e das máscaras (tamanho, modo de cor, valores únicos).
- Gerar uma figura de uma cena típica (original, falsificada, `B`, `M`).

## Fora do escopo

- Qualquer modelo (ticket 06-04).
- Corrigir ou refazer máscaras.

## Critérios de aceite

- [x] Há uma tabela com mediana e quantis da cobertura da diferença `O≠F` na máscara `B` e do IoU, para as 200 cenas; cenas sem nenhuma diferença entre `O` e `F` são contadas.
- [x] Um parágrafo no notebook afirma **o que `B` representa** (só a região colada, ou origem mais cópia, ou outra coisa), citando o número que sustenta a conclusão. Se os números não decidirem, o parágrafo diz isso.
- [x] Há um histograma da fração marcada (% da imagem) e a mediana por categoria de manipulação.
- [x] Há a correlação (ou outra medida declarada) entre a área do `readme.txt` e a área da máscara, com a ressalva de que a área do readme é anterior à transformação.
- [x] A tabela de formatos mostra se todas as imagens-base têm 512x512 e se as máscaras são RGBA.
- [x] A figura de exemplo existe no notebook, desligada por padrão (ver Resultado).

## Notas

- A fração marcada é pequena em relação à imagem (a área do readme vai de centenas a dezenas de milhares de pixels, de 262.144): isso afeta o desbalanceamento de pixels de um futuro modelo de localização.
- Só leitura das imagens; nada é gravado fora de `data/interim/`.

## Resultado (2026-10-15)

- Todas as imagens-base têm 512x512, mas o **modo de cor é misto**: `B` 126 RGB e 74 RGBA, `M` 162 e 38, `O` 195 e 5, `F` 196 e 4. Por isso o notebook converte tudo para RGB/L antes de comparar.
- `B` marca regiões pequenas: mediana de 2,6% da imagem (de 0,3% a 29%); correlação em log com a área do `readme.txt`: 0,976.
- Nas 163 cenas com diferença localizada, cobertura mediana de 100% e IoU mediano de 0,50: compatível com `B` marcando origem e cópia, enquanto `O≠F` só vê a cópia (leitura dos números, não documentada). Em escala o IoU mediano é 0,24.
- **Achado extra:** em 35 cenas (18 de ROTATION, 17 de SCALING, 0 nas outras três categorias) `O` e `F` diferem em mais de 50% dos pixels. A causa não está documentada.
- Nenhuma cena sem diferença entre `O` e `F`.
- **Desvio do critério da figura:** a figura de exemplo existe no notebook sob a flag `EXIBIR_EXEMPLO`, **desligada por padrão**, porque o *release agreement* proíbe redistribuir as imagens e o notebook é versionado. A saída padrão imprime só os nomes da cena de exemplo.
