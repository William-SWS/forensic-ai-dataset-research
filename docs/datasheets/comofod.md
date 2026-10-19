# Datasheet: CoMoFoD Small

Nicho: imagem, detecção e localização de falsificação por cópia e colagem (*copy-move*).
Análise exploratória: `notebooks/02_eda_comofod.ipynb` (tickets 06-01 a 06-06).
Última revisão: 2026-10-18.

## Origem

- **Autores:** Dijana Tralić, Ivan Zupančić, Sonja Grgić e Mislav Grgić, Video Communications Laboratory (VCL), Faculdade de Engenharia Elétrica e Computação (FER), Universidade de Zagreb.
- **Página oficial:** https://www.vcl.fer.hr/comofod/
- **Citação obrigatória:** Tralić D., Zupancic I., Grgic S., Grgic M., "CoMoFoD - New Database for Copy-Move Forgery Detection", in *Proc. 55th International Symposium ELMAR-2013*, pp. 49-54, setembro de 2013.
- **Propósito declarado:** avaliar algoritmos de detecção de *copy-move* sob diferentes transformações e pós-processamentos.

## Acesso

- **CoMoFoD Small** (512x512, 200 conjuntos): download direto, sem cadastro, depois de ler o *release agreement*. Arquivo `comofod_small.rar`, 3.213.318.957 bytes, sha256 `6ea6a5e9788f02838f5992cb192b9404f5c64e1980551c31985f4afd87d401e9` (medido em 2026-10-15; a página não publica hash).
- **CoMoFoD Large** (3000x2000): só por contato com os autores. Não usado neste projeto.
- No projeto: `data/raw/comofod/` (arquivo intacto) e `data/interim/comofod/` (extraído). As duas pastas estão fora do git.

## Composição

| Item | Valor medido |
|---|---|
| Arquivos de imagem | 10.400 (3,21 GB extraídos) |
| Cenas (conjuntos) | 200, todas com 52 arquivos |
| Fotografias distintas por trás das cenas | **41** (mediana de 4 cenas por foto, máximo 13) |
| Imagens classificáveis | 10.000 (5.000 originais, 5.000 falsificadas) |
| Resolução | 512x512 em todas as imagens-base |
| Modo de cor | misto: RGB e RGBA nos quatro tipos de arquivo-base |

Cada cena tem:

- `O` (original), `F` (falsificada), `B` (máscara binária) e `M` (máscara colorida);
- 24 variantes de `O` e 24 de `F` com pós-processamento: brilho (BC), contraste (CA), redução de cor (CR), desfoque (IB) e ruído (NA), com 3 níveis cada, e JPEG (JC), com 9 níveis.

Categorias de manipulação (segundo o `readme.txt`): TRANSLATION 40, ROTATION 40, SCALING 40, DISTORTION 39 e COMBINATION 41.

## Rótulos

- **Classe da imagem** (original ou falsificada): dada pelo nome do arquivo.
- **Máscara `B`:** marca regiões pequenas, mediana de 2,6% da imagem (de 0,3% a 29%). Os números são compatíveis com `B` marcar **a região de origem e a colada** (cobertura mediana de 100% da diferença `O≠F`, IoU mediano 0,50), mas isso não está documentado pelos autores.
- **PSNR (`psnr.txt`):** cobre só ruído (NA) sobre originais, 600 das 9.600 variantes pós-processadas (6,25%).

## Riscos e limitações

1. **Unidade independente é a fotografia, não a cena.** As 200 cenas vêm de 41 fotografias. Dividir treino e teste por imagem ou por cena vaza: o random forest de referência cai de AUC 0,984 (por imagem) e 0,967 (por cena) para **0,495 por fotografia**.
2. **Escala pequena.** 41 fotografias não bastam para treinar um modelo profundo do zero.
3. **Atalho global em rotação e escala.** Em 35 cenas (18 de rotação e 17 de escala) `O` e `F` diferem em mais de 50% dos pixels. Um detector pode aprender esse processamento global em vez da adulteração. A causa não foi investigada.
4. **Máscaras sem documentação.** O significado de `B` foi inferido dos números, e o IoU cai para 0,24 nas cenas de escala.
5. **PSNR incompleto.** Não se extrapola o PSNR de `O` para `F` nem para outros pós-processamentos.
6. **Sem garantia dos autores.** O *release agreement* diz que os donos não se responsabilizam por erros ou omissões. As inconsistências acima (cenas repetidas, artefato global, máscaras sem documentação) são, portanto, problema de quem usa a base: devem ser medidas e relatadas, não presumidas inexistentes.
7. **Não avaliado neste projeto:** localização em nível de pixel, detectores *copy-move* clássicos e redes convolucionais.

## Usos

- **Recomendado:** benchmark de robustez a pós-processamentos e teste de transferência de um detector treinado em outra base (hipótese de uso; não medida aqui), sempre com divisão por fotografia.
- **Não recomendado:** treinar um classificador do zero só com esta base; relatar métricas com divisão por imagem ou por cena; qualquer uso comercial (proibido pelos termos).

## Termos de uso

### Texto do *release agreement*

Fonte: https://www.vcl.fer.hr/comofod/release_agreemen.html, lido e aceito em 2026-10-15 (decisão 16). Transcrição na íntegra:

> You can download the CoMoFoD database here under the following terms:
>
> The CoMoFoD database will not be further distributed, published, copied, or further disseminated in any way or form whatsoever, whether for profit or not. This includes further distributing, copying or disseminating to a facility or organization unit in the requesting university, organization, or company. CoMoFoD images may be used to create new images but the downloaded images will not be modified.
>
> All the images will be used for the purpose of academic or scientific research only. The CoMoFoD database, in whole or in part, will not be used for any commercial purpose in any form. Commercial distribution or any act related to commercial use of this database is strictly prohibited.
>
> All documents and papers that report research results obtained using the CoMoFoD database will acknowledge the use of the CoMoFoD database. Please cite the following paper:
> Tralic D., Zupancic I., Grgic S., Grgic M., "CoMoFoD - New Database for Copy-Move Forgery Detection", in Proc. 55th International Symposium ELMAR-2013, pp. 49-54, September 2013
>
> While every effort has been made to ensure accuracy, CoMOFoD database owners cannot accept responsibility for errors or omissions.
>
> Use of CoMoFoD database is free of charge.
>
> CoMOFoD database owners reserve the right to revise, amend, alter or delete the information provided herein at any time, but shall not be responsible for or liable in respect of any such revisions, amendments, alterations or deletions.

### O que isso significa no projeto

| Cláusula | Regra prática |
|---|---|
| Não distribuir, publicar, copiar nem disseminar, nem dentro da própria instituição | `data/raw/` e `data/interim/` ficam fora do git. Nenhuma imagem, recorte ou miniatura da base entra em notebooks versionados, documentos, slides ou artefatos publicados. Quem for reproduzir baixa a base por conta própria na página oficial. |
| As imagens baixadas não podem ser modificadas; imagens novas podem ser criadas | O notebook só lê as imagens. Imagens derivadas (ex.: novas variantes) são permitidas, mas ficam em `data/interim/` e também não são publicadas, porque reproduzem o conteúdo da base. |
| Só pesquisa acadêmica ou científica; nenhum uso comercial | Nenhum modelo treinado nesta base, nem parte dela, vai para produto ou serviço comercial. |
| Citar Tralić et al., ELMAR 2013 | Todo relatório, apresentação, artigo ou notebook que mostre resultado obtido com a base traz a citação acima. |
| Sem garantia de exatidão | Ver risco 6: as inconsistências medidas são relatadas como limitação. |
| Uso gratuito | Sem custo de licença. |
| Os donos podem mudar os termos a qualquer momento | Antes de publicar qualquer resultado, reler a página do acordo e comparar com a transcrição acima. Se mudar, registrar uma nova entrada em `docs/decisions.md` e atualizar esta seção. |

### O que pode ser publicado

Métricas, tabelas, histogramas e outros agregados calculados a partir da base, além de nomes de arquivo e índices de cena, desde que acompanhados da citação. A figura de exemplo do notebook 02 existe sob a flag `EXIBIR_EXEMPLO = False` e só deve ser ligada localmente, sem versionar a saída.
