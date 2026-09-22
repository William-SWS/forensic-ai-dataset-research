# IA aplicada à Forense Digital — Revisão de Literatura Anotada

**Modo:** ARS `deep-research` / `lit-review` (Fases 2–3: busca sistemática → verificação de fontes → síntese)
**Data da busca:** 2026-09-22
**Escopo solicitado:** (i) IA para detecção e classificação de maliciosidade em rede; (ii) IA na classificação de imagens forenses; (iii) IA para forense de dumps de memória, imagem/multimídia e análise de discos rígidos
**Fontes verificadas:** 39 (todas com DOI ou arXiv ID confirmado)

---

## 1. Estratégia de busca

| Item | Detalhe |
|---|---|
| Bases/índices | Crossref API (metadados canônicos), arXiv API, indexação web de Springer Nature, ScienceDirect, ACM DL, IEEE Xplore, MDPI |
| Janela temporal | 2020–2026, com inclusão de anchors seminais anteriores quando canônicos |
| Idioma | Inglês (literatura primária da área) |
| Strings principais | `("digital forensics" OR "forensic investigation") AND ("deep learning" OR "machine learning" OR "large language model")`; `("network intrusion detection" OR "malicious traffic classification") AND (transformer OR GNN OR "encrypted traffic")`; `("memory forensics" OR "memory dump") AND (CNN OR "malware classification" OR volatility)`; `("image forgery detection" OR "image forensics" OR deepfake) AND survey`; `("file fragment classification" OR "file carving") AND ("deep learning" OR transformer)`; `("admissibility" OR Daubert) AND ("explainable AI" OR "digital evidence")` |
| Critérios de inclusão | Peer-reviewed (Tier 1) ou pré-print de grupo identificável com contribuição metodológica (Tier 2); relevância direta a ≥1 dos três eixos; publicação ≤6 anos salvo anchor canônico |
| Critérios de exclusão | Blogs, material de marketing de fornecedor, conteúdo do LinkedIn, teses não publicadas, itens cujo metadado bibliográfico não pôde ser confirmado |
| Verificação | Cada referência teve título, autoria, veículo, volume/páginas, ano e DOI confirmados contra a Crossref API ou a arXiv API. **Nenhuma referência foi incluída com base apenas em resultado de busca.** |

**Itens descartados na verificação:** três resultados de busca foram excluídos por serem material não acadêmico (posts de LinkedIn/blogs de fornecedor sobre admissibilidade de IA) e um por ser tese de mestrado homônima a artigo já indexado (`ForensicLLM`, dissertação LSU vs. artigo FSI:DI — mantido o artigo).

---

## 2. Eixo 0 — Guarda-chuva: estado da arte de IA em forense digital

Cinco revisões delimitam o campo e servem como ponto de partida obrigatório para o enquadramento de qualquer artigo novo.

**Du, X., Hargreaves, C., Sheppard, J., Anda, F., Sayakkara, A., Le-Khac, N., & Scanlon, M. (2020).** *SoK: Exploring the state of the art and the future potential of artificial intelligence in digital forensic investigation.* ARES 2020, 1–10.
— **Anchor canônico.** Systematization-of-Knowledge que organiza aplicações de IA por fase do processo forense e identifica o gargalo central: o volume de dados cresce mais rápido que a capacidade de análise humana. Base para justificar automação. *Nível de evidência: VII (revisão narrativa/SoK), Grade A pelo padrão da área.*

**Nayerifard, T., Amintoosi, H., Ghaemi Bafghi, A., & Dehghantanha, A. (2023).** *Machine learning in digital forensics: A systematic literature review.* arXiv:2306.04965.
— SLR cobrindo 2010–2021. Conclusão central e diretamente relevante ao seu escopo: **a forense de imagem é o subdomínio que mais se beneficiou de ML**, e CNNs são a técnica dominante. Útil para justificar por que o eixo (ii) é o mais maduro. *Nível: I (SLR); Tier 2 (pré-print).*

**Dunsin, D., Ghanem, M., Ouazzane, K., & Vassilev, V. (2024).** *A comprehensive analysis of the role of artificial intelligence and machine learning in modern digital forensics and incident response.* Forensic Science International: Digital Investigation, 48, 301675.
— Mapeia IA/ML sobre o ciclo de DFIR (não apenas análise), incluindo resposta a incidentes. Veículo top da área (FSI:DI = journal do DFRWS). *Nível: VII; Grade A.*

**Fähndrich, J., Honekamp, W., Povalej, R., Rittelmeier, H., Berner, S., & Labudde, D. (2023).** *Digital forensics and strong AI: A structured literature review.* Forensic Science International: Digital Investigation, 46, 301617.
— Revisão estruturada com recorte conceitual distinto: separa o que é IA "fraca" aplicada (classificadores de tarefa) do que exigiria IA geral. Bom contraponto crítico ao otimismo das demais. *Nível: I/VII híbrido; Grade A.*

**Aigbogun, O., & Varol, C. (2026).** *Where intelligence has taken hold, and where it has not: A PRISMA-guided systematic mapping review of digital forensics.* Electronics, 15(17), 3763.
— **A revisão mais útil para localizar lacuna.** Mapeamento PRISMA-ScR de 82 estudos primários sobre seis domínios forenses, tratando a adoção de métodos inteligentes como *variável a ser medida* em vez de pressuposto. Identifica explicitamente domínios onde a IA **não** penetrou. *Nível: I (systematic mapping review); Grade A.*

---

## 3. Eixo 1 — IA para detecção e classificação de maliciosidade em rede

### 3.1 Revisões de fundamentação

**Xu, Z., Wu, Y., Wang, S., Gao, J., Qiu, T., Wang, Z., Wan, H., & Zhao, X. (2025).** *Deep learning-based intrusion detection systems: A survey.* arXiv:2504.07839 (v3, out. 2025).
— Survey que cobre o **pipeline completo** do DL-IDS: coleta, armazenamento de logs, parsing de logs, sumarização em grafo, detecção e *investigação* do ataque. Essa última etapa é o que conecta IDS a forense de rede — a maioria dos surveys de IDS para em "detecção". Inclui seção de datasets de benchmark. *Nível: VII; Tier 2.*

**Neto, E., Iqbal, S., Buffett, S., Sultana, M., & Taylor, A. (2025).** *Deep learning for intrusion detection in emerging technologies: A comprehensive survey and new perspectives.* Artificial Intelligence Review, 58.
— Recorte em tecnologias emergentes (IoT, 5G, edge, veicular). Relevante porque o cenário forense real raramente é uma rede corporativa homogênea. Autoria do NRC Canada. *Nível: VII; Grade A.*

**Hozouri, A., Mirzaei, A., & Effatparvar, M. (2025).** *A comprehensive survey on intrusion detection systems with advances in machine learning, deep learning and emerging cybersecurity challenges.* Discover Artificial Intelligence, 5.
— Cobertura ampla e recente; útil como fonte de taxonomia (classificadores clássicos → DNN → ensembles híbridos → federated learning). *Nível: VII; Grade B (veículo mais novo, menor track record).*

### 3.2 Contribuições metodológicas

**Lin, X., Xiong, G., Gou, G., Li, Z., Shi, J., & Yu, J. (2022).** *ET-BERT: A contextualized datagram representation with pre-training transformers for encrypted traffic classification.* WWW '22, 633–642.
— **Anchor metodológico do subcampo.** Transfere o paradigma pré-treinamento/fine-tuning para bytes de datagrama, permitindo classificação de tráfego **cifrado** com pouco dado rotulado. É a linha de base contra a qual todo trabalho posterior de tráfego cifrado se compara. *Nível: VI (estudo experimental); Grade A (WWW é A*).*

**Zhan, M., Yang, J., Jia, D., & Fu, G. (2025).** *EAPT: An encrypted traffic classification model via adversarial pre-trained transformers.* Computer Networks, 257, 110973.
— Evolução direta do ET-BERT introduzindo pré-treinamento adversarial. Relevante para o problema de robustez (ver §6.3). *Nível: VI; Grade A.*

**Luo, X., Liu, C., Xiong, G., Yang, C., Gou, G., Ren, Y., & Li, Z. (2025).** *MalRAG: A retrieval-augmented LLM framework for open-set malicious traffic identification.* arXiv:2511.14129.
— Ataca o problema de **conjunto aberto** (open-set): identificar tráfego malicioso de famílias não vistas no treino, que é exatamente a condição forense real. Usa RAG em vez de re-treino. Mesmo grupo do ET-BERT (CAS/IIE). *Nível: VI; Tier 2 (pré-print recente).*

**El Mahdaouy, A., Ait Yahia, I., Oualil, S., & Berrada, I. (2026).** *Deep learning for contextualized NetFlow-based network intrusion detection: Methods, data, evaluation and deployment.* arXiv:2602.05594 (v3).
— Foco em **NetFlow contextualizado** e, criticamente, em *avaliação e implantação* — o elo mais fraco da literatura de NIDS. *Nível: VII/VI; Tier 2.*

---

## 4. Eixo 2 — IA na classificação de imagens forenses e multimídia

**Zanardelli, M., Guerrini, F., Leonardi, R., & Adami, N. (2023).** *Image forgery detection: A survey of recent deep-learning approaches.* Multimedia Tools and Applications, 82, 17521–17566.
— Survey de referência para *image forgery detection* com DL, organizando por tipo de manipulação (copy-move, splicing, inpainting) e por domínio de feature. *Nível: VII; Grade A.*

**Nguyen-Le, H., Tran, V., Nguyen, D., & Le-Khac, N. (2026).** *Deepfake detection across image, video, and audio: A comprehensive survey with empirical evaluation of generalization and robustness.* Artificial Intelligence Review, 59.
— **A referência mais importante deste eixo para fins forenses.** Não é só survey: inclui **avaliação empírica de generalização e robustez cross-dataset**, que é a métrica que importa em perícia e a que a literatura costuma omitir. Coautoria de Le-Khac (UCD, também autor do SoK). *Nível: I/VI; Grade A.*

**Khan, A., Laghari, A., Inam, S., Ullah, S., Shahzad, M., & Syed, D. (2025).** *A survey on multimedia-enabled deepfake detection: State-of-the-art tools and techniques, emerging trends, current challenges & limitations, and future directions.* Discover Computing, 28.
— Complementa o anterior com inventário de **ferramentas** (não apenas métodos), útil para a seção de instrumentação de um artigo aplicado. *Nível: VII; Grade B.*

**Sardhara, A., Vekariya, V., Pathak, A., & Dash, S. (2026).** *DeepForgeryNet: A hybrid CNN–LSTM and transfer learning framework for robust image forgery and deepfake detection.* Frontiers in Artificial Intelligence, 9.
— Exemplar recente da arquitetura híbrida dominante: CNN para traço forense local + LSTM para consistência global. Serve como baseline contemporâneo. *Nível: VI; Grade B.*

**Nowroozi, E., Dehghantanha, A., Parizi, R., & Choo, K. (2021).** *A survey of machine learning techniques in adversarial image forensics.* Computers & Security, 100, 102092.
— **Contraponto obrigatório.** Sistematiza o lado anti-forense: como GANs e exemplos adversariais fabricam traços forenses sintéticos e derrubam classificadores forenses. Qualquer artigo que proponha um classificador de imagem forense sem discutir isso será atacado em revisão. *Nível: VII; Grade A.*

---

## 5. Eixo 3 — IA em dumps de memória, disco e file carving

### 5.1 Forense de memória volátil

**Dehfouli, Y., & Habibi Lashkari, A. (2025).** *Memory analysis for malware detection: A comprehensive survey using the OSCAR methodology.* ACM Computing Surveys, 58, 1–58.
— **Ponto de partida obrigatório do eixo.** Survey de 58 páginas na ACM CSUR (o veículo de maior autoridade para surveys em computação), estruturado pela metodologia forense OSCAR — ou seja, organiza a literatura de ML pelo *processo forense*, não pela arquitetura de rede neural. Coautoria de Habibi Lashkari (criador do dataset CIC-MalMem-2022). *Nível: I/VII; Grade A+.*

**Carrier, T., Victor, P., Tekeoglu, A., & Habibi Lashkari, A. (2022).** *Detecting obfuscated malware using memory feature engineering.* ICISSP 2022, 177–188.
— Artigo de origem do **CIC-MalMem-2022**, o dataset de facto do subcampo: features extraídas por VolMemLyzer a partir de dumps de memória, com rótulos por tipo (ransomware, spyware, trojan) e subtipo. Citação obrigatória se você usar o dataset. *Nível: VI; Grade A.*

**Bozkir, A., Tahillioglu, E., Aydos, M., & Kara, I. (2021).** *Catch them alive: A malware detection approach through memory forensics, manifold learning and computer vision.* Computers & Security, 103, 102166.
— **Anchor da linha "memória como imagem".** Converte dumps de processo em imagens e aplica visão computacional + manifold learning. Estabelece o paradigma de representação visual que domina o subcampo. *Nível: VI; Grade A.*

**Shah, S., Ahmad, A., Jamil, N., & Khan, A. (2022).** *Memory forensics-based malware detection using computer vision and machine learning.* Electronics, 11(16), 2579.
— Replicação/extensão do paradigma visual em veículo aberto; útil como comparativo. *Nível: VI; Grade B.*

**Naeem, H., Dong, S., Falana, O., & Ullah, F. (2023).** *Development of a deep stacked ensemble with process based volatile memory forensics for platform independent malware detection and classification.* Expert Systems with Applications, 223, 119952.
— Ensemble empilhado com granularidade **por processo** e alegação de independência de plataforma — endereça diretamente a limitação Windows-cêntrica do resto do subcampo. *Nível: VI; Grade A.*

**Maniriho, P., Mahmood, A., & Chowdhury, M. (2024).** *MeMalDet: A memory analysis-based malware detection framework using deep autoencoders and stacked ensemble under temporal evaluations.* Computers & Security, 142, 103864.
— **Metodologicamente o mais rigoroso do conjunto.** O diferencial está em *temporal evaluations*: avalia sob deriva temporal (treino em malware antigo, teste em malware novo), o protocolo que revela a inflação de acurácia dos demais trabalhos. *Nível: VI; Grade A.*

**Yu, S., Li, B., Zhao, Y., Chen, Y., Sun, Y., & Chang, H. (2026).** *Intelligent malware detection method based on memory segments.* Cybersecurity, 9.
— Granularidade de **segmento de memória** em vez de dump inteiro ou processo — nível intermediário de abstração pouco explorado. *Nível: VI; Grade B.*

**Odeh, A., Taleb, A., Alhajahjeh, T., & Navarro, F. (2025).** *Advanced memory forensics for malware classification with deep learning algorithms.* Cluster Computing, 28.
— Comparação head-to-head de CNN, RNN e autoencoders sobre features de memória forense. Valor principal é o comparativo controlado entre famílias de arquitetura. *Nível: VI; Grade B.*

**Alaeiyan, M., & Lakzian, P. (2026).** *Malware detection via memory dump images: Investigating the role of uneven kernel filters in CNNs with visual explainability.* Journal of Computer Virology and Hacking Techniques, 22.
— Contribuição específica e verificável: kernels **não-quadrados** em CNNs sobre imagens de dump, com explicabilidade visual. A explicabilidade é o que torna o resultado utilizável em laudo. *Nível: VI; Grade B.*

**Yaseen, Q., Manasrah, A., & Oudat, E. (2026).** *Memory-resident malware detection using explainable AI and adaptive compression.* Array, 31, 101101.
— Combina XAI com compressão adaptativa, endereçando o custo de processar dumps de memória em escala — restrição operacional real em laboratório forense. *Nível: VI; Grade B.*

### 5.2 Disco, file carving e classificação de fragmentos

**Liu, W., Wang, Y., Wu, K., Yap, K., & Chau, L. (2023).** *A byte sequence is worth an image: CNN for file fragment classification using bit shift and n-gram embeddings.* arXiv:2304.06983.
— Estabelece a analogia byte→imagem para classificação de fragmentos, com embeddings de bit shift e n-grama. *Nível: VI; Tier 2.*

**Liu, W., Wu, K., Liu, T., Wang, Y., Yap, K., & Chau, L. (2025).** *ByteNet: Rethinking multimedia file fragment classification through visual perspectives.* IEEE Transactions on Multimedia, 27, 1305–1319.
— Versão madura e peer-reviewed da linha anterior, em veículo de primeira linha. **A referência a citar** para classificação de fragmentos multimídia. *Nível: VI; Grade A.*

**Zou, B., & Liu, H. (2026).** *Hierarchical deep learning for file fragment classification.* Electronics, 15(7), 1507.
— Classificação hierárquica (clustering aglomerativo + classificadores especializados por categoria) em vez de flat multi-class. Aborda o problema de granularidade de classes, que é onde os modelos flat falham (ex.: distinguir JPEG de PNG de dados comprimidos genéricos). *Nível: VI; Grade B.*

**Toma, I., Tonmoy, A., Bhowmik, A., & Sarker, S. (2025).** *A multi-task hybrid deep learning based framework for robust file fragment classification in digital forensics.* INCET 2025, 1–6.
— Formulação multi-tarefa. Veículo modesto (conferência), incluído por cobertura do ângulo multi-task. *Nível: VI; Grade C.*

> **Lacuna observável neste sub-eixo:** a literatura de "análise de disco rígido" com IA é quase inteiramente **classificação de fragmentos para carving**. Praticamente não há trabalho de IA sobre artefatos de sistema de arquivos (journal NTFS/ext4, $MFT, timestamps, reconstrução de timeline), que é o que o perito realmente faz em análise de disco. Isso é consistente com o achado de Aigbogun e Varol (2026) sobre domínios onde a IA não penetrou.

---

## 6. Eixo transversal — LLMs, admissibilidade e robustez

### 6.1 LLMs em forense digital (fronteira 2024–2026)

**Wickramasekara, A., Breitinger, F., & Scanlon, M. (2025).** *Exploring the potential of large language models for improving digital forensic investigation efficiency.* Forensic Science International: Digital Investigation, 52, 301859.
— Primeiro mapeamento sistemático de capacidades de LLM sobre o **modelo de processo DFRWS**, identificando três pontos de integração: reconhecimento de padrões (examination), análise de evidência (analysis) e apresentação/relatório (presentation). *Nível: VII; Grade A.*

**Sharma, B., Ghawaly, J., McCleary, K., Webb, A., & Baggili, I. (2025).** *ForensicLLM: A local large language model for digital forensics.* Forensic Science International: Digital Investigation, 52, 301872.
— LLaMA-3.1-8B quantizado em 4 bits, fine-tuned em Q&A extraído de artigos forenses e artefatos curados. **Local** — o que resolve a objeção de cadeia de custódia contra APIs de terceiros. Autoria de Baggili (figura central da área). *Nível: VI; Grade A.*

**Michelet, G., Henseler, H., Beek, H., Scanlon, M., & Breitinger, F. (2025).** *Fine-tuning large language models for digital forensics: Case study and general recommendations.* Digital Threats: Research and Practice, 6, 1–18.
— Recomendações práticas de fine-tuning derivadas de estudo de caso. Complementa o ForensicLLM no nível do método. *Nível: VI; Grade A.*

**Chernyshev, M., Baig, Z., Syed, N., Doss, R., & Shore, M. (2026).** *Large language models in digital forensics: Capabilities, challenges and future directions.* Forensic Science International: Digital Investigation, 56, 302043.
— SLR de 33 trabalhos peer-reviewed (2023–2025). Articula a **tensão fundamental** do campo: a natureza probabilística da saída de LLM contra o requisito determinístico da prova forense, além de explicabilidade, reprodutibilidade e admissibilidade. *Nível: I; Grade A.*

**Khatiwala, J., Addai, D., & Xu, W. (2026).** *Evaluating the reliability of digital forensic evidence discovered by large language model: A case study.* arXiv:2602.20202.
— Tentativa direta de **medir** confiabilidade da evidência descoberta por LLM. É a pergunta certa; estudo de caso único limita generalização. *Nível: VI; Tier 2.*

**Chakir, Y., & Lahsen-Cherif, I. (2025).** *ForensicsData: A digital forensics dataset for large language models.* arXiv:2509.05331.
— Dataset para avaliação de LLMs em tarefas forenses — infraestrutura que o campo não tinha. *Nível: N/A (recurso); Tier 2.*

**Murtuza, S. (2026).** *Forensic implications of localized AI: Artifact analysis of Ollama, LM Studio, and llama.cpp.* arXiv:2603.23996.
— Inversão interessante do problema: IA como **objeto** de perícia, não ferramenta. Artefatos deixados por runtimes de LLM local. Relevante se você quiser um ângulo pouco disputado. *Nível: VI; Tier 2.*

### 6.2 Validade jurídica

**Ottaviani, M., Spadazzi, F., Bubbico, T., De Paola, L., & La Russa, R. (2026).** *The evolution of scientific evidence between artificial intelligence and legal validity.* Legal Medicine, 83, 102852.
— Única fonte **peer-reviewed** localizada sobre validade legal de prova produzida por IA (o restante do material disponível sobre Daubert/Rule 702 e IA é literatura cinza de fornecedores e escritórios, excluída na triagem). Perspectiva de medicina legal, não de common law norte-americana — o que pode ser vantagem ou limitação conforme sua jurisdição-alvo. *Nível: VII; Grade B.*

> ⚠️ **Lacuna de evidência confirmada:** não existe, na literatura peer-reviewed localizada, um protocolo de validação de modelo de IA forense construído explicitamente para satisfazer critérios de admissibilidade (testabilidade, taxa de erro conhecida, peer review, aceitação geral). A discussão existe em literatura cinza; o instrumento metodológico não existe. **Esta é a lacuna mais explorável do conjunto.**

### 6.3 Robustez adversarial

Ver **Nowroozi et al. (2021)** em §4 e **Zhan et al. (2025)** em §3.2. O padrão transversal: todo eixo tem seu vetor anti-forense (GAN para imagem, evasão para tráfego, ofuscação/fileless para memória), e a literatura de proposição de métodos raramente se cruza com a literatura de ataque.

---

## 7. Síntese temática

### 7.1 Convergências (o que as fontes concordam)

1. **CNN é a arquitetura hegemônica em todos os três eixos**, e o mecanismo comum é a *redução a representação visual*: dump de memória → imagem em escala de cinza (Bozkir et al., 2021; Shah et al., 2022), sequência de bytes → imagem (Liu et al., 2023, 2025), datagrama → token (Lin et al., 2022). A convergência não é coincidência: é reaproveitamento de arquiteturas de visão computacional maduras sobre dados binários.
2. **O gargalo declarado é sempre volume, não acurácia** (Du et al., 2020; Dunsin et al., 2024). A justificativa para IA em forense é throughput e triagem, não superioridade classificatória sobre o perito.
3. **A forense de imagem é o subdomínio mais maduro** (Nayerifard et al., 2023), e a análise de sistema de arquivos/disco o menos (Aigbogun & Varol, 2026). Dois mapeamentos independentes com metodologias diferentes convergem nisso.
4. **Malware moderno (polimórfico, ofuscado, fileless) derrotou a detecção estática**, o que é a justificativa unânime para forense de memória (Dehfouli & Habibi Lashkari, 2025; Carrier et al., 2022; Naeem et al., 2023).
5. **Explicabilidade é requisito, não recurso opcional**, quando o destino é o laudo (Alaeiyan & Lakzian, 2026; Yaseen et al., 2026; Chernyshev et al., 2026).

### 7.2 Divergências e tensões não resolvidas

| Tensão | Posição A | Posição B | Estado |
|---|---|---|---|
| Representação para forense de memória | Features tabulares engenheiradas (VolMemLyzer, 55 features) — Carrier et al. (2022), Odeh et al. (2025) | Dump como imagem + visão computacional — Bozkir et al. (2021), Alaeiyan & Lakzian (2026) | **Não resolvida.** Os dois paradigmas raramente são comparados sob protocolo idêntico. Lacuna metodológica direta. |
| Granularidade de análise de memória | Dump completo | Por processo (Naeem et al., 2023) / por segmento (Yu et al., 2026) | Tendência a granularidade fina, sem estudo comparativo sistemático. |
| Necessidade de pré-treinamento em tráfego | Pré-treino massivo é essencial (Lin et al., 2022; Zhan et al., 2025) | Abordagens diretas em byte sem tokenização/pré-treino são competitivas | Disputa ativa em 2025–2026. |
| LLM em forense | Ganho de eficiência real, com modelo local resolvendo custódia (Sharma et al., 2025) | Incompatibilidade estrutural entre saída probabilística e prova determinística (Chernyshev et al., 2026) | **Tensão de fundo, não resolvida.** É o debate mais quente do campo agora. |

### 7.3 Viés sistemático identificado (checkpoint do Devil's Advocate)

Três problemas recorrentes que atravessam a literatura dos três eixos:

- **Inflação de acurácia por protocolo de avaliação inadequado.** A vasta maioria dos trabalhos reporta métricas em split aleatório sobre dataset único, balanceado e de snapshot temporal único. Maniriho et al. (2024) demonstram, com avaliação temporal explícita, que essa métrica não sobrevive à deriva; Nguyen-Le et al. (2026) demonstram o mesmo para deepfakes via avaliação cross-dataset. **Consequência prática: acurácias reportadas na faixa de 97–99% não devem ser lidas como desempenho operacional esperado.** (As cifras específicas citadas em abstracts não foram confirmadas em texto integral nesta rodada — ver §9.)
- **Monocultura de dataset.** Forense de memória está fortemente ancorada em CIC-MalMem-2022 (Windows-cêntrico, features VolMemLyzer, dump único); forense de fragmentos em GovDocs/FFT-75; tráfego em CIC-IDS/UNSW-NB15. Generalização para fora desses conjuntos é raramente demonstrada.
- **Desconexão entre proposição e ataque.** A literatura que propõe classificadores forenses e a literatura anti-forense (Nowroozi et al., 2021) citam-se pouco. Modelos são publicados sem avaliação adversarial.

---

## 8. Lacunas → oportunidades de pesquisa

Priorizadas por (a) sustentação na evidência localizada e (b) viabilidade.

| # | Lacuna | Pergunta de pesquisa candidata | Sustentação |
|---|---|---|---|
| **G1** | Ausência de protocolo de validação de modelo de IA forense orientado a admissibilidade | *Que protocolo de validação — taxa de erro conhecida, testabilidade, avaliação cross-dataset e temporal — um classificador de IA forense deve satisfazer para sustentar escrutínio de admissibilidade, e como os métodos publicados se comportam sob ele?* | §6.2; Chernyshev et al. (2026); Ottaviani et al. (2026) |
| **G2** | Paradigmas de representação de memória nunca comparados sob protocolo único | *Features engenheiradas vs. representação visual de dumps de memória: qual generaliza melhor sob deriva temporal e para fora do CIC-MalMem-2022?* | §7.2; Maniriho et al. (2024) como modelo metodológico |
| **G3** | IA praticamente ausente da análise de disco propriamente dita | *Métodos de aprendizado podem apoiar reconstrução de timeline e análise de artefatos de sistema de arquivos, além da classificação de fragmentos para carving?* | §5.2; Aigbogun & Varol (2026) |
| **G4** | Robustez adversarial não avaliada nos métodos propostos | *Qual a degradação de classificadores forenses de memória e de fragmentos sob ataques anti-forenses de ofuscação e adversariais?* | §6.3; Nowroozi et al. (2021) |
| **G5** | Confiabilidade de LLM em forense medida apenas em estudo de caso único | *Com que confiabilidade e reprodutibilidade um LLM local recupera evidência verificável, sob avaliação repetida e temperatura controlada?* | Khatiwala et al. (2026); Chakir & Lahsen-Cherif (2025) como dataset |
| **G6** | Condição de conjunto aberto sub-explorada fora de tráfego | *A abordagem de recuperação aumentada (RAG) que funciona para tráfego malicioso open-set transfere para famílias de malware não vistas em memória?* | Luo et al. (2025) |

**Recomendação:** G1 e G2 são as mais defensáveis. G1 tem lacuna confirmada e apelo interdisciplinar (computação + direito probatório); G2 é um estudo comparativo puramente empírico, executável com datasets públicos e sem necessidade de dado novo — o caminho mais curto para um artigo publicável.

---

## 9. Limitações desta revisão

1. **Verificação bibliográfica, não leitura integral.** Todas as 39 referências tiveram metadados confirmados contra Crossref ou arXiv. A caracterização de conteúdo deriva de títulos, abstracts e sumários de indexação — **não** de leitura de texto integral. Alegações de desempenho numérico foram deliberadamente omitidas por não terem sido confirmadas na fonte primária.
2. **Iniciais de autoria truncadas.** Os metadados da Crossref foram consumidos com uma inicial por autor; nomes do meio podem estar ausentes. Confirme a autoria completa antes de submeter qualquer manuscrito que use estas referências.
3. **Ano de publicação de Zanardelli et al.** — a Crossref registra `issued` 2022 (online-first); o volume 82 do MTAP é de 2023. Citado como 2023; verifique conforme a norma do veículo-alvo.
4. **Sem PRISMA.** Esta é uma revisão de literatura anotada em modo `lit-review`, não uma revisão sistemática: não houve registro de protocolo, dupla triagem independente, nem fluxo PRISMA. Para revisão sistemática, escalar para o modo `systematic-review`.
5. **Viés de indexação e idioma.** Busca restrita ao inglês e a índices majoritariamente ocidentais. Literatura chinesa e russa relevante em forense de memória e tráfego pode estar sub-representada.
6. **ScienceDirect, ACM DL e Springer bloquearam acesso direto** (HTTP 403 / paywall de redirecionamento). Metadados obtidos via Crossref; conteúdo caracterizado por abstract indexado.
7. **Seis pré-prints arXiv** (Tier 2) foram incluídos por cobrirem a fronteira 2025–2026 sem equivalente peer-reviewed. Estão marcados como tal. Verifique se houve publicação formal antes de citar.

---

## 10. Declaração de uso de IA

Esta revisão foi produzida com assistência de IA (Claude Opus 5, via pipeline ARS `deep-research` em modo `lit-review`). Busca, triagem, verificação de metadados via API e redação da síntese foram executadas pelo sistema; a verificação de metadados bibliográficos foi determinística (Crossref/arXiv APIs), a caracterização de conteúdo não. A curadoria final, a leitura das fontes primárias e a responsabilidade pelas afirmações em qualquer manuscrito derivado permanecem com o autor humano.

---

## 11. Referências (APA 7ª ed.)

Aigbogun, O., & Varol, C. (2026). Where intelligence has taken hold, and where it has not: A PRISMA-guided systematic mapping review of digital forensics. *Electronics, 15*(17), 3763. https://doi.org/10.3390/electronics15173763

Alaeiyan, M., & Lakzian, P. (2026). Malware detection via memory dump images: Investigating the role of uneven kernel filters in CNNs with visual explainability. *Journal of Computer Virology and Hacking Techniques, 22*. https://doi.org/10.1007/s11416-026-00644-x

Bozkir, A., Tahillioglu, E., Aydos, M., & Kara, I. (2021). Catch them alive: A malware detection approach through memory forensics, manifold learning and computer vision. *Computers & Security, 103*, 102166. https://doi.org/10.1016/j.cose.2020.102166

Carrier, T., Victor, P., Tekeoglu, A., & Habibi Lashkari, A. (2022). Detecting obfuscated malware using memory feature engineering. *Proceedings of the 8th International Conference on Information Systems Security and Privacy*, 177–188. https://doi.org/10.5220/0010908200003120

Chakir, Y., & Lahsen-Cherif, I. (2025). *ForensicsData: A digital forensics dataset for large language models* [Preprint]. arXiv. https://arxiv.org/abs/2509.05331

Chernyshev, M., Baig, Z., Syed, N., Doss, R., & Shore, M. (2026). Large language models in digital forensics: Capabilities, challenges and future directions. *Forensic Science International: Digital Investigation, 56*, 302043. https://doi.org/10.1016/j.fsidi.2025.302043

Dehfouli, Y., & Habibi Lashkari, A. (2025). Memory analysis for malware detection: A comprehensive survey using the OSCAR methodology. *ACM Computing Surveys, 58*, 1–58. https://doi.org/10.1145/3764580

Du, X., Hargreaves, C., Sheppard, J., Anda, F., Sayakkara, A., Le-Khac, N., & Scanlon, M. (2020). SoK: Exploring the state of the art and the future potential of artificial intelligence in digital forensic investigation. *Proceedings of the 15th International Conference on Availability, Reliability and Security*, 1–10. https://doi.org/10.1145/3407023.3407068

Dunsin, D., Ghanem, M., Ouazzane, K., & Vassilev, V. (2024). A comprehensive analysis of the role of artificial intelligence and machine learning in modern digital forensics and incident response. *Forensic Science International: Digital Investigation, 48*, 301675. https://doi.org/10.1016/j.fsidi.2023.301675

El Mahdaouy, A., Ait Yahia, I., Oualil, S., & Berrada, I. (2026). *Deep learning for contextualized NetFlow-based network intrusion detection: Methods, data, evaluation and deployment* [Preprint]. arXiv. https://arxiv.org/abs/2602.05594

Fähndrich, J., Honekamp, W., Povalej, R., Rittelmeier, H., Berner, S., & Labudde, D. (2023). Digital forensics and strong AI: A structured literature review. *Forensic Science International: Digital Investigation, 46*, 301617. https://doi.org/10.1016/j.fsidi.2023.301617

Hozouri, A., Mirzaei, A., & Effatparvar, M. (2025). A comprehensive survey on intrusion detection systems with advances in machine learning, deep learning and emerging cybersecurity challenges. *Discover Artificial Intelligence, 5*. https://doi.org/10.1007/s44163-025-00578-1

Khan, A., Laghari, A., Inam, S., Ullah, S., Shahzad, M., & Syed, D. (2025). A survey on multimedia-enabled deepfake detection: State-of-the-art tools and techniques, emerging trends, current challenges & limitations, and future directions. *Discover Computing, 28*. https://doi.org/10.1007/s10791-025-09550-0

Khatiwala, J. P., Addai, D. K. N., & Xu, W. (2026). *Evaluating the reliability of digital forensic evidence discovered by large language model: A case study* [Preprint]. arXiv. https://arxiv.org/abs/2602.20202

Lin, X., Xiong, G., Gou, G., Li, Z., Shi, J., & Yu, J. (2022). ET-BERT: A contextualized datagram representation with pre-training transformers for encrypted traffic classification. *Proceedings of the ACM Web Conference 2022*, 633–642. https://doi.org/10.1145/3485447.3512217

Liu, W., Wang, Y., Wu, K., Yap, K., & Chau, L. (2023). *A byte sequence is worth an image: CNN for file fragment classification using bit shift and n-gram embeddings* [Preprint]. arXiv. https://arxiv.org/abs/2304.06983

Liu, W., Wu, K., Liu, T., Wang, Y., Yap, K., & Chau, L. (2025). ByteNet: Rethinking multimedia file fragment classification through visual perspectives. *IEEE Transactions on Multimedia, 27*, 1305–1319. https://doi.org/10.1109/TMM.2024.3521830

Luo, X., Liu, C., Xiong, G., Yang, C., Gou, G., Ren, Y., & Li, Z. (2025). *MalRAG: A retrieval-augmented LLM framework for open-set malicious traffic identification* [Preprint]. arXiv. https://arxiv.org/abs/2511.14129

Maniriho, P., Mahmood, A., & Chowdhury, M. (2024). MeMalDet: A memory analysis-based malware detection framework using deep autoencoders and stacked ensemble under temporal evaluations. *Computers & Security, 142*, 103864. https://doi.org/10.1016/j.cose.2024.103864

Michelet, G., Henseler, H., Beek, H., Scanlon, M., & Breitinger, F. (2025). Fine-tuning large language models for digital forensics: Case study and general recommendations. *Digital Threats: Research and Practice, 6*, 1–18. https://doi.org/10.1145/3748264

Murtuza, S. (2026). *Forensic implications of localized AI: Artifact analysis of Ollama, LM Studio, and llama.cpp* [Preprint]. arXiv. https://arxiv.org/abs/2603.23996

Naeem, H., Dong, S., Falana, O., & Ullah, F. (2023). Development of a deep stacked ensemble with process based volatile memory forensics for platform independent malware detection and classification. *Expert Systems with Applications, 223*, 119952. https://doi.org/10.1016/j.eswa.2023.119952

Nayerifard, T., Amintoosi, H., Ghaemi Bafghi, A., & Dehghantanha, A. (2023). *Machine learning in digital forensics: A systematic literature review* [Preprint]. arXiv. https://doi.org/10.48550/arXiv.2306.04965

Neto, E., Iqbal, S., Buffett, S., Sultana, M., & Taylor, A. (2025). Deep learning for intrusion detection in emerging technologies: A comprehensive survey and new perspectives. *Artificial Intelligence Review, 58*. https://doi.org/10.1007/s10462-025-11346-z

Nguyen-Le, H., Tran, V., Nguyen, D., & Le-Khac, N. (2026). Deepfake detection across image, video, and audio: A comprehensive survey with empirical evaluation of generalization and robustness. *Artificial Intelligence Review, 59*. https://doi.org/10.1007/s10462-026-11608-4

Nowroozi, E., Dehghantanha, A., Parizi, R., & Choo, K. (2021). A survey of machine learning techniques in adversarial image forensics. *Computers & Security, 100*, 102092. https://doi.org/10.1016/j.cose.2020.102092

Odeh, A., Taleb, A., Alhajahjeh, T., & Navarro, F. (2025). Advanced memory forensics for malware classification with deep learning algorithms. *Cluster Computing, 28*. https://doi.org/10.1007/s10586-025-05104-7

Ottaviani, M., Spadazzi, F., Bubbico, T., De Paola, L., & La Russa, R. (2026). The evolution of scientific evidence between artificial intelligence and legal validity. *Legal Medicine, 83*, 102852. https://doi.org/10.1016/j.legalmed.2026.102852

Sardhara, A., Vekariya, V., Pathak, A., & Dash, S. (2026). DeepForgeryNet: A hybrid CNN–LSTM and transfer learning framework for robust image forgery and deepfake detection. *Frontiers in Artificial Intelligence, 9*. https://doi.org/10.3389/frai.2026.1810912

Shah, S., Ahmad, A., Jamil, N., & Khan, A. (2022). Memory forensics-based malware detection using computer vision and machine learning. *Electronics, 11*(16), 2579. https://doi.org/10.3390/electronics11162579

Sharma, B., Ghawaly, J., McCleary, K., Webb, A., & Baggili, I. (2025). ForensicLLM: A local large language model for digital forensics. *Forensic Science International: Digital Investigation, 52*, 301872. https://doi.org/10.1016/j.fsidi.2025.301872

Toma, I., Tonmoy, A., Bhowmik, A., & Sarker, S. (2025). A multi-task hybrid deep learning based framework for robust file fragment classification in digital forensics. *2025 6th International Conference for Emerging Technology*, 1–6. https://doi.org/10.1109/INCET64471.2025.11140445

Wickramasekara, A., Breitinger, F., & Scanlon, M. (2025). Exploring the potential of large language models for improving digital forensic investigation efficiency. *Forensic Science International: Digital Investigation, 52*, 301859. https://doi.org/10.1016/j.fsidi.2024.301859

Xu, Z., Wu, Y., Wang, S., Gao, J., Qiu, T., Wang, Z., Wan, H., & Zhao, X. (2025). *Deep learning-based intrusion detection systems: A survey* [Preprint]. arXiv. https://arxiv.org/abs/2504.07839

Yaseen, Q., Manasrah, A., & Oudat, E. (2026). Memory-resident malware detection using explainable AI and adaptive compression. *Array, 31*, 101101. https://doi.org/10.1016/j.array.2026.101101

Yu, S., Li, B., Zhao, Y., Chen, Y., Sun, Y., & Chang, H. (2026). Intelligent malware detection method based on memory segments. *Cybersecurity, 9*. https://doi.org/10.1186/s42400-025-00537-4

Zanardelli, M., Guerrini, F., Leonardi, R., & Adami, N. (2023). Image forgery detection: A survey of recent deep-learning approaches. *Multimedia Tools and Applications, 82*, 17521–17566. https://doi.org/10.1007/s11042-022-13797-w

Zhan, M., Yang, J., Jia, D., & Fu, G. (2025). EAPT: An encrypted traffic classification model via adversarial pre-trained transformers. *Computer Networks, 257*, 110973. https://doi.org/10.1016/j.comnet.2024.110973

Zou, B., & Liu, H. (2026). Hierarchical deep learning for file fragment classification. *Electronics, 15*(7), 1507. https://doi.org/10.3390/electronics15071507
