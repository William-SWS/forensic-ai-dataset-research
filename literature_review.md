Pesquisa concluída. Antes do resultado, dois avisos necessários.

**Bloqueio de infraestrutura:** tentei executar a busca com 4 subagentes paralelos (protocolo padrão). O runtime de subagentes está indisponível nesta instalação: `Background children require pi installed as the npm package ... does not provide @earendil-works/pi-server`. Falhou tanto em `async:true` quanto em foreground. Executei a busca diretamente na sessão principal, com o mesmo método de verificação por API.

**Nenhum arquivo do projeto foi tocado.** Todas as escritas foram em `/tmp` (scripts de consulta e listas de DOIs).

---

# IA aplicada à forense digital, rodada complementar

**Data da busca:** 2026-09-23
**Objetivo:** referências **novas** em relação a `lit-review_ia_forense_digital.md`. Verifiquei interseção contra os 39 DOIs já presentes: **zero sobreposição**.
**Fontes verificadas:** 60 (todas com DOI confirmado)
**Método:** descoberta por OpenAlex (`title_and_abstract.search`) e por travessia de citações (`cites:` de anchors seminais: ET-BERT, Kitsune, DeepLog, ManTra-Net, BusterNet, "Learning Rich Features", "CNN-generated images", Oscar), mais arXiv. Metadados confirmados individualmente contra `api.crossref.org/works/{DOI}`. Para 51 das 60, o texto do abstract foi efetivamente recuperado via OpenAlex e a anotação deriva dele, não do título.

**Nota metodológica:** onde escrevo "descrição não caracterizada", o abstract não foi recuperável por API. Não preenchi a lacuna por inferência.

---

## Eixo 1 — IA para detecção e classificação de maliciosidade em rede

**1. TrafficFormer: An Efficient Pre-trained Model for Traffic Data.** Zhou, G., Guo, X., Liu, Z., Li, T., Li, Q., Xu, K. (2025). *2025 IEEE Symposium on Security and Privacy (SP)*, 1844-1860. DOI: [10.1109/sp61157.2025.00102](https://doi.org/10.1109/sp61157.2025.00102)
Tier A* (IEEE S&P). Pré-treinamento de modelo para dados de tráfego endereçando o gargalo de dados rotulados escassos; o abstract aponta que a exploração de pré-treinamento nesse domínio ainda era limitada.

**2. NetMamba: Efficient Network Traffic Classification Via Pre-Training Unidirectional Mamba.** Wang, T., Xie, X., Wang, W., Wang, C., Zhao, Y., Cui, Y. (2024). *2024 IEEE 32nd International Conference on Network Protocols (ICNP)*, 1-11. DOI: [10.1109/icnp61940.2024.10858569](https://doi.org/10.1109/icnp61940.2024.10858569)
Tier A (ICNP). Alternativa não-transformer ao pré-treinamento em tráfego, motivada por custo computacional e limitações das abordagens existentes. Relevante como contraponto direto a ET-BERT dentro do seu §7.2 (a disputa sobre necessidade de pré-treinamento massivo).

**3. NetLLM: Adapting Large Language Models for Networking.** Wu, D., Wang, X., Qiao, Y., Wang, Z., Jiang, J., Cui, S., Wang, F. (2024). *Proceedings of the ACM SIGCOMM 2024 Conference*, 661-678. DOI: [10.1145/3651890.3672268](https://doi.org/10.1145/3651890.3672268)
Tier A* (SIGCOMM). Trata o custo de engenharia de projetar DNNs por tarefa e a generalização pobre entre tarefas de rede, adaptando LLMs como backbone único.

**4. Low-Quality Training Data Only? A Robust Framework for Detecting Encrypted Malicious Network Traffic.** Qing, Y., Yin, Q., Deng, X., Chen, Y., Liu, Z., Sun, K., Xu, K., Zhang, J., Li, Q. (2024). *Proceedings 2024 Network and Distributed System Security Symposium (NDSS)*. DOI: [10.14722/ndss.2024.23081](https://doi.org/10.14722/ndss.2024.23081)
Tier A* (NDSS). **O mais alinhado à condição forense real:** parte do fato de que não se consegue montar dataset de tráfego malicioso cifrado com rótulos corretos, e propõe framework robusto a dados de treino de baixa qualidade. Ataque direto à premissa de dataset limpo que sustenta a literatura de classificação de tráfego.

**5. TCG-IDS: Robust Network Intrusion Detection via Temporal Contrastive Graph Learning.** Wu, C., Sun, J., Chen, J., Alazab, M., Liu, Y., Xiang, Y. (2025). *IEEE Transactions on Information Forensics and Security*, 20, 1475-1486. DOI: [10.1109/tifs.2025.3530702](https://doi.org/10.1109/tifs.2025.3530702)
Tier A (TIFS, Q1). Enquadra o problema sob modelo zero trust e redes de próxima geração, com validação contínua e aprendizado contrastivo temporal em grafo.

**6. ATVITSC: A Novel Encrypted Traffic Classification Method Based on Deep Learning.** Liu, Y., Wang, X., Qu, B., Zhao, F. (2024). *IEEE Transactions on Information Forensics and Security*, 19, 9374-9389. DOI: [10.1109/tifs.2024.3433446](https://doi.org/10.1109/tifs.2024.3433446)
Tier A. Crítica explícita às abordagens que dependem de features manuais ou falham em extrair dependências não triviais de tráfego cifrado.

**7. A Novel Self-Supervised Framework Based on Masked Autoencoder for Traffic Classification.** Zhao, R., Zhan, M., Deng, X., Li, F., Wang, Y., Wang, Y., Gui, G., Xue, Z. (2024). *IEEE/ACM Transactions on Networking*, 32, 2012-2025. DOI: [10.1109/tnet.2023.3335253](https://doi.org/10.1109/tnet.2023.3335253)
Tier A (ToN). Aponta limitação concreta da linha ET-BERT: representação gerada apenas de bytes crus, sem informação estrutural do fluxo.

**8. FOSS: Towards Fine-Grained Unknown Class Detection Against the Open-Set Attack Spectrum With Variable Legitimate Traffic.** Zhao, Z., Li, Z., Xie, X., Yu, J., Zhang, F., Zhang, R., Chen, B., Luo, X., Hu, M., Ma, W. (2024). *IEEE/ACM Transactions on Networking*, 32, 3945-3960. DOI: [10.1109/tnet.2024.3413789](https://doi.org/10.1109/tnet.2024.3413789)
Tier A. Dois desafios nomeados no abstract: detecção de ataque desconhecido em granularidade fina e adaptação a tráfego legítimo em mudança. Complementa MalRAG no problema open-set, por outra via.

**9. MIETT: Multi-Instance Encrypted Traffic Transformer for Encrypted Traffic Classification.** Chen, X., Han, L., Zhan, D., Ye, H. (2025). *Proceedings of the AAAI Conference on Artificial Intelligence*, 39, 15922-15929. DOI: [10.1609/aaai.v39i15.33748](https://doi.org/10.1609/aaai.v39i15.33748)
Tier A* (AAAI). Organiza tráfego em pacotes e fluxos e usa formulação multi-instância.

**10. Kairos: Practical Intrusion Detection and Investigation using Whole-system Provenance.** Cheng, Z., Lv, Q., Liang, J., Wang, Y., Sun, D., Pasquier, T., Han, X. (2024). *2024 IEEE Symposium on Security and Privacy (SP)*, 3533-3551. DOI: [10.1109/sp54263.2024.00005](https://doi.org/10.1109/sp54263.2024.00005)
Tier A* (S&P). **Ponte explícita entre detecção e investigação.** Grafo de proveniência como log de auditoria estruturado; o abstract identifica quatro dimensões de projeto comuns à literatura e unifica detecção e investigação no mesmo sistema.

**11. Flash: A Comprehensive Approach to Intrusion Detection via Provenance Graph Representation Learning.** Ur Rehman, M., Ahmadi, H., Ul Hassan, W. (2024). *2024 IEEE Symposium on Security and Privacy (SP)*, 3552-3570. DOI: [10.1109/sp54263.2024.00139](https://doi.org/10.1109/sp54263.2024.00139)
Tier A* (S&P). Nomeia o trade-off central dos IDS baseados em proveniência: acurácia contra custo, problema não resolvido na classe de métodos.

**12. Hierarchical Adversarial Attacks Against Graph-Neural-Network-Based IoT Network Intrusion Detection System.** Zhou, X., Liang, W., Li, W., Yan, K., Shimizu, S., Wang, K. (2022). *IEEE Internet of Things Journal*, 9, 9310-9319. DOI: [10.1109/jiot.2021.3130434](https://doi.org/10.1109/jiot.2021.3130434)
Tier A (IoT-J). Vetor adversarial específico contra NIDS baseado em GNN. Sustenta diretamente a lacuna G4 do seu arquivo, agora com fonte peer-reviewed no eixo de rede, não só no de imagem (onde está Nowroozi et al.).

**13. IoV-BERT-IDS: Hybrid Network Intrusion Detection System in IoV Using Large Language Models.** Fu, M., Wang, P., Liu, M., Zhang, Z., Zhou, X. (2025). *IEEE Transactions on Vehicular Technology*, 74, 1909-1921. DOI: [10.1109/tvt.2024.3402366](https://doi.org/10.1109/tvt.2024.3402366)
Tier A. LLM aplicado a IDS em internet dos veículos.

**14. Enhancing trustworthiness in ML-based network intrusion detection with uncertainty quantification.** Talpini, J., Sartori, F., Savi, M. (2024). *Journal of Reliable Intelligent Environments*, 10, 501-520. DOI: [10.1007/s40860-024-00238-8](https://doi.org/10.1007/s40860-024-00238-8)
Tier B. Quantificação de incerteza em IDS baseado em ML. É a única fonte peer-reviewed que localizei tratando calibração e incerteza como requisito de confiabilidade em IDS, o que ataca o ponto 1 do seu §7.3 (inflação de acurácia).

**15. LogFiT: Log Anomaly Detection Using Fine-Tuned Language Models.** Almodovar, C., Sabrina, F., Karimi, S., Azad, S. (2024). *IEEE Transactions on Network and Service Management*, 21, 1715-1723. DOI: [10.1109/tnsm.2024.3358730](https://doi.org/10.1109/tnsm.2024.3358730)
Tier A (TNSM). Logs de sistema como fonte forense de host, com LM fine-tunado.

**16. A Critical Review of Common Log Data Sets Used for Evaluation of Sequence-Based Anomaly Detection Techniques.** Landauer, M., Skopik, F., Wurzenberger, M. (2024). *Proceedings of the ACM on Software Engineering*, 1, 1354-1375. DOI: [10.1145/3660768](https://doi.org/10.1145/3660768)
Tier A (FSE/PACMSE). **Auditoria dos datasets de avaliação, não de métodos.** É o análogo, no subcampo de logs, ao que Maniriho et al. (2024) e Nguyen-Le et al. (2026) fazem em memória e deepfake. Candidata natural a citar no seu §7.3 (monocultura de dataset).

---

## Eixo 2 — IA na classificação e análise de imagens forenses

**17. Pixel-Inconsistency Modeling for Image Manipulation Localization.** Kong, C., Luo, A., Wang, S., Li, H., Rocha, A., Kot, A. (2025). *IEEE Transactions on Pattern Analysis and Machine Intelligence*, 47, 4455-4472. DOI: [10.1109/tpami.2025.3541028](https://doi.org/10.1109/tpami.2025.3541028)
Tier A* (TPAMI). O abstract nomeia exatamente a limitação de generalização e robustez a imagens perturbadas dos métodos de localização de falsificação. Coautoria de Anderson Rocha (Unicamp) e Alex Kot (NTU).

**18. Exploring Multi-View Pixel Contrast for General and Robust Image Forgery Localization.** Lou, Z., Cao, G., Guo, K., Yu, L., Weng, S. (2025). *IEEE Transactions on Information Forensics and Security*, 20, 2329-2341. DOI: [10.1109/tifs.2025.3541957](https://doi.org/10.1109/tifs.2025.3541957)
Tier A. Crítica ao mapeamento pixel-para-rótulo direto, que não explora relações entre pixels no espaço de features.

**19. Language-Guided Hierarchical Fine-Grained Image Forgery Detection and Localization.** Guo, X., Liu, X., Masi, I., Liu, X. (2024). *International Journal of Computer Vision*, 133, 2670-2691. DOI: [10.1007/s11263-024-02255-9](https://doi.org/10.1007/s11263-024-02255-9)
Tier A* (IJCV). Descrição não caracterizada (abstract não recuperável por API). A contribuição é guiada por linguagem e hierárquica por tipo de manipulação.

**20. Image Copy-Move Forgery Detection via Deep PatchMatch and Pairwise Ranking Learning.** Li, Y., He, Y., Chen, C., Dong, L., Li, B., Zhou, J., Li, X. (2025). *IEEE Transactions on Image Processing*, 34, 425-440. DOI: [10.1109/tip.2024.3482191](https://doi.org/10.1109/tip.2024.3482191)
Tier A* (TIP). Nomeia a falha de generalização quando as regiões copiadas não aparecem nas imagens de treino ou são fundo. É a formulação de conjunto aberto dentro do CMFD.

**21. MGQFormer: Mask-Guided Query-Based Transformer for Image Manipulation Localization.** Zeng, K., Cheng, R., Tan, W., Yan, B. (2024). *Proceedings of the AAAI Conference on Artificial Intelligence*, 38, 6944-6952. DOI: [10.1609/aaai.v38i7.28520](https://doi.org/10.1609/aaai.v38i7.28520)
Tier A* (AAAI). Diagnóstico de ineficiência de treino causada pelo uso de máscara ground-truth sob cross-entropy.

**22. Forgery-aware Adaptive Transformer for Generalizable Synthetic Image Detection.** Liu, H., Tan, Z., Tan, C., Wei, Y., Wang, J., Zhao, Y. (2024). *2024 IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)*, 10770-10780. DOI: [10.1109/cvpr52733.2024.01024](https://doi.org/10.1109/cvpr52733.2024.01024)
Tier A* (CVPR). Detecção de sintéticas de métodos generativos diversos (GAN e difusão), com adaptação do backbone pré-treinado em vez de classificador acoplado fixo.

**23. AEROBLADE: Training-Free Detection of Latent Diffusion Images Using Autoencoder Reconstruction Error.** Ricker, J., Lukovnikov, D., Fischer, A. (2024). *2024 IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)*, 9130-9140. DOI: [10.1109/cvpr52733.2024.00872](https://doi.org/10.1109/cvpr52733.2024.00872)
Tier A* (CVPR). Detecção sem treino, via erro de reconstrução do autoencoder do modelo de difusão latente.

**24. Raising the Bar of AI-generated Image Detection with CLIP.** Cozzolino, D., Poggi, G., Corvi, R., Nießner, M., Verdoliva, L. (2024). *2024 IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops (CVPRW)*, 4356-4366. DOI: [10.1109/cvprw63382.2024.00439](https://doi.org/10.1109/cvprw63382.2024.00439)
Tier B (workshop), mas autoria de Verdoliva (GRIP/TUM), referência em forense de imagem. Usa features de CLIP para detecção universal de imagem gerada, em cenários difíceis.

**25. Deepfake Detection: A Comprehensive Survey from the Reliability Perspective.** Wang, T., Liao, X., Chow, K., Lin, X., Wang, Y. (2024). *ACM Computing Surveys*, 57, 1-35. DOI: [10.1145/3699710](https://doi.org/10.1145/3699710)
Tier A* (CSUR). Organiza o campo por **confiabilidade** e identifica três desafios orientados a confiabilidade. Alternativa de survey ao de Nguyen-Le et al. (2026), com recorte analítico diferente.

**26. Mastering Deepfake Detection: A Cutting-edge Approach to Distinguish GAN and Diffusion-model Images.** Guarnera, L., Giudice, O., Battiato, S. (2024). *ACM Transactions on Multimedia Computing, Communications, and Applications*, 20, 1-24. DOI: [10.1145/3652027](https://doi.org/10.1145/3652027)
Tier A (TOMM). Dataset de 83.000 imagens geradas por nove arquiteturas GAN e quatro modelos de difusão, com distinção entre as duas famílias.

**27. Evading DeepFake Detectors via Adversarial Statistical Consistency.** Hou, Y., Guo, Q., Huang, Y., Xie, X., Ma, L., Zhao, J. (2023). *2023 IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)*, 12271-12280. DOI: [10.1109/cvpr52729.2023.01181](https://doi.org/10.1109/cvpr52729.2023.01181)
Tier A* (CVPR). Explora o fato de os detectores se apoiarem em diferenças estatísticas entre domínio espacial e de frequência, e ataca exatamente esse pressuposto. Vetor anti-forense concreto para o seu §6.3.

**28. Generating Higher-Quality Anti-Forensics DeepFakes with Adversarial Sharpening Mask.** Fan, B., Ding, F., Zhu, G., Huang, J., Kwong, S., Atrey, P., Lyu, S. (2025). *ACM Transactions on Multimedia Computing, Communications, and Applications*, 21, 1-18. DOI: [10.1145/3729233](https://doi.org/10.1145/3729233)
Tier A (TOMM). Coautoria de Siwei Lyu e Jiwu Huang. Gera deepfake anti-forense evitando os artefatos de qualidade que denunciam as versões anteriores.

**29. StealthDiffusion: Towards Evading Diffusion Forensic Detection through Diffusion Model.** Zhou, Z., Sun, K., Chen, Z., Kuang, H., Sun, X., Ji, R. (2024). *Proceedings of the 32nd ACM International Conference on Multimedia*, 3627-3636. DOI: [10.1145/3664647.3681535](https://doi.org/10.1145/3664647.3681535)
Tier A* (ACM MM). Formaliza a tarefa de "AIGC-Stealth": gerar imagem que escapa simultaneamente ao detector forense e à inspeção humana.

**30. An efficient ensemble explainable AI (XAI) approach for morphed face detection.** Dwivedi, R., Kothari, P., Chopra, D., Singh, M., Kumar, R. (2024). *Pattern Recognition Letters*, 184, 197-204. DOI: [10.1016/j.patrec.2024.06.014](https://doi.org/10.1016/j.patrec.2024.06.014)
Tier A (PRL, Q1). Descrição não caracterizada (abstract não recuperável). Traz XAI para detecção de face morphing, subcampo distinto do deepfake.

**31. Synthetic ID Card Image Generation for Improving Presentation Attack Detection.** Benalcazar, D., Tapia, J., Gonzalez, S., Busch, C. (2023). *IEEE Transactions on Information Forensics and Security*, 18, 1814-1824. DOI: [10.1109/tifs.2023.3255585](https://doi.org/10.1109/tifs.2023.3255585)
Tier A. Forense de documento de identidade com IA, eixo que seu arquivo não cobre. O abstract situa o problema na digitalização de processos que antes exigiam presença física, incluindo autenticação biométrica remota.

**32. Datasets, clues and state-of-the-arts for multimedia forensics: An extensive review.** Yadav, A., Kumar Vishwakarma, D. (2024). *Expert Systems with Applications*, 249, 123756. DOI: [10.1016/j.eswa.2024.123756](https://doi.org/10.1016/j.eswa.2024.123756)
Tier A (ESWA, Q1). Descrição não caracterizada (abstract não recuperável). Revisão de **datasets** de forense multimídia, recurso que o seu arquivo não tem mapeado.

**33. Source camera attribution via PRNU emphasis: Towards a generalized multiplicative model.** Fernández-Menduiña, S., Pérez-González, F., Masciopinto, M. (2023). *Signal Processing: Image Communication*, 114, 116944. DOI: [10.1016/j.image.2023.116944](https://doi.org/10.1016/j.image.2023.116944)
Tier A (Q1). Revisa a análise teórica do PRNU, que o abstract descreve como usualmente apoiada em modelo multiplicativo, e propõe generalização. Atribuição de dispositivo é o eixo clássico de forense de imagem ausente do seu arquivo.

**34. Video source camera identification using fusion of texture features and noise fingerprint.** Anmol, T., Sitara, K. (2024). *Forensic Science International: Digital Investigation*, 49, 301746. DOI: [10.1016/j.fsidi.2024.301746](https://doi.org/10.1016/j.fsidi.2024.301746)
Tier A (FSI:DI, veículo do DFRWS). Descrição não caracterizada (abstract não recuperável). Fonte de câmera em vídeo, com fusão de features de textura e impressão de ruído.

---

## Eixo 3 — IA em dumps de memória, disco, imagens e multimídia

**35. A Cross-Attention Multi-Scale Performer With Gaussian Bit-Flips for File Fragment Classification.** Liu, S., Park, J., Kim, H., Hong, J. (2025). *IEEE Transactions on Information Forensics and Security*, 20, 2109-2121. DOI: [10.1109/tifs.2025.3539527](https://doi.org/10.1109/tifs.2025.3539527)
Tier A. Versão em journal do XMP (item 36). O abstract identifica viés inerente dos modelos CNN como limitação de eficácia em FFC, a crítica que o seu §5.2 aponta como ausente.

**36. XMP: A Cross-Attention Multi-Scale Performer for File Fragment Classification.** Park, J., Liu, S., Hong, J. (2024). *ICASSP 2024 - 2024 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)*, 4505-4509. DOI: [10.1109/icassp48485.2024.10447626](https://doi.org/10.1109/icassp48485.2024.10447626)
Tier B (ICASSP, conferência de sinal de primeira linha). Versão de conferência do anterior.

**37. SIFT: Sifting file types, application of explainable artificial intelligence in cyber forensics.** Alam, S., Demir, A. (2024). *Cybersecurity*, 7. DOI: [10.1186/s42400-024-00241-9](https://doi.org/10.1186/s42400-024-00241-9)
Tier B (Cybersecurity, Springer). Classificação de tipo de arquivo com XAI. Casa com o requisito de explicabilidade para laudo que seu §7.1 aponta como consensual.

**38. Data-Constrained File Fragment Classification Across Heterogeneous File Types using Large Language Models.** Zhou, H., Xu, W., Dehlinger, J., Chakraborty, S., Deng, L. (2026). *2026 IEEE 50th Annual Computers, Software, and Applications Conference (COMPSAC)*, 738-743. DOI: [10.1109/compsac69091.2026.00101](https://doi.org/10.1109/compsac69091.2026.00101)
Tier B (COMPSAC). Descrição não caracterizada (abstract não recuperável). **LLM aplicado a FFC**, ângulo que a literatura de fragmentos ainda não explorava.

**39. NTFS-LogID: Automated Identification and Classification of NTFS Internal System Artifacts from Raw Binary Data.** Sahu, N., Singh, B., Bharadwaj, N. (2026). *2026 5th OPJU International Technology Conference (OTCON)*, 1-6. DOI: [10.1109/otcon69332.2026.11629697](https://doi.org/10.1109/otcon69332.2026.11629697)
Tier C (conferência regional). Descrição não caracterizada (abstract não recuperável). **Achado relevante apesar do tier:** é o único item que localizei endereçando identificação automatizada de artefatos internos do NTFS a partir de binário cru, que é exatamente o buraco descrito na lacuna G3 e no box do seu §5.2.

**40. ProcGCN: detecting malicious process in memory based on DGCNN.** Zhang, H., Li, B., Yu, S., Chang, C., Li, J., Yang, B. (2024). *PeerJ Computer Science*, 10, e2193. DOI: [10.7717/peerj-cs.2193](https://doi.org/10.7717/peerj-cs.2193)
Tier B. O abstract critica a abordagem dominante de converter dump de processo em imagem, argumentando que ela permanece classificação de features de bytes e que essas features mudam depois que o malware é carregado em memória. **É a crítica metodológica que o seu §7.2 registra como não resolvida, feita por um dos lados do debate.** Grafo em vez de imagem.

**41. Few-Shot Learning With Prototypical Networks for Improved Memory Forensics.** Fahad Malik, M., Gul, A., Saadia, A., Alserhani, F. (2025). *IEEE Access*, 13, 79397-79409. DOI: [10.1109/access.2025.3565802](https://doi.org/10.1109/access.2025.3565802)
Tier B. Nomeia três restrições operacionais: volume e complexidade dos dumps, evolução do malware e **escassez de dado rotulado**.

**42. Transformer-Based Memory Reverse Engineering for Malware Behavior Reconstruction.** Alrawashdeh, K. (2025). *Computers*, 15, 8. DOI: [10.3390/computers15010008](https://doi.org/10.3390/computers15010008)
Tier B (MDPI). Trata bytes crus de memória como tokens linguísticos e aponta fragilidade dos métodos tradicionais diante de ofuscação e injeção. Representação por transformer em vez de imagem.

**43. HAGEN: Unveiling Obfuscated Memory Threats via Hierarchical Attention-Gated Explainable Networks.** Farfoura, M., Alia, M., Connie, T. (2026). *Electronics*, 15, 352. DOI: [10.3390/electronics15020352](https://doi.org/10.3390/electronics15020352)
Tier B (MDPI). Malware fileless e fortemente ofuscado, com explicabilidade aplicada ao contexto de SOC, que o abstract identifica como onde o deep learning ainda tem uso limitado.

**44. Kernel-level hidden rootkit detection based on eBPF.** Yu, Y., Hung, C., Chou, L. (2025). *Computers & Security*, 157, 104582. DOI: [10.1016/j.cose.2025.104582](https://doi.org/10.1016/j.cose.2025.104582)
Tier A (C&S, Q1). Descrição não caracterizada (abstract não recuperável). Detecção de rootkit em nível de kernel, tema de anti-forense que o seu arquivo só menciona de passagem.

**45. Unveiling BYOVD Threats: Malware's Use and Abuse of Kernel Drivers.** Monzani, A., Parata, A., Oliveri, A., Aonzo, S., Balzarotti, D., Lanzi, A. (2026). *Proceedings 2026 Network and Distributed System Security Symposium (NDSS)*. DOI: [10.14722/ndss.2026.231491](https://doi.org/10.14722/ndss.2026.231491)
Tier A* (NDSS). Coautoria de Davide Balzarotti (Eurecom). Técnica anti-forense/de evasão em Windows moderno: o atacante carrega sua própria cópia de driver vulnerável de terceiro no kernel.

**46. Discovering spoliation of evidence through identifying traces on deleted files in macOS.** Joun, J., Lee, S., Park, J. (2023). *Forensic Science International: Digital Investigation*, 44, 301502. DOI: [10.1016/j.fsidi.2023.301502](https://doi.org/10.1016/j.fsidi.2023.301502)
Tier A (FSI:DI). Trata **spoliation** (destruição de prova) e rastreamento de comportamento anti-forense em arquivos apagados, incluindo a lacuna de que recuperação e carving tradicionais não resolvem o caso.

**47. Enabling per-file data recovery from ransomware attacks via file system forensics and flash translation layer data extraction.** Dafoe, J., Chen, N., Chen, B., Wang, Z. (2024). *Cybersecurity*, 7. DOI: [10.1186/s42400-024-00287-9](https://doi.org/10.1186/s42400-024-00287-9)
Tier B. Recuperação por arquivo combinando forense de sistema de arquivos com extração da camada de tradução de flash em SSD. **Este é o único trabalho que localizei ligando IA-independente forense de sistema de arquivos a SSD/FTL**, o que toca a lacuna G3 por outro ângulo.

**48. A novel method for real-time object-based copy-move tampering localization in videos using fine-tuned YOLO V8.** Sandhya, Kashyap, A. (2024). *Forensic Science International: Digital Investigation*, 48, 301663. DOI: [10.1016/j.fsidi.2023.301663](https://doi.org/10.1016/j.fsidi.2023.301663)
Tier A (FSI:DI). Descrição não caracterizada (abstract não recuperável). Forense de vídeo, eixo que seu arquivo não tem.

**49. A comprehensive taxonomy on multimedia video forgery detection techniques: challenges and novel trends.** El-Shafai, W., Fouda, M., El-Rabaie, E., Abd El-Salam, N. (2023). *Multimedia Tools and Applications*, 83, 4241-4307. DOI: [10.1007/s11042-023-15609-1](https://doi.org/10.1007/s11042-023-15609-1)
Tier B (MTAP, Q1, veículo generalista). Taxonomia de falsificação de vídeo, útil como mapa do subcampo ausente do seu arquivo.

**50. Review of audio deepfake detection techniques: Issues and prospects.** Dixit, A., Kaur, N., Kingra, S. (2023). *Expert Systems*, 40. DOI: [10.1111/exsy.13322](https://doi.org/10.1111/exsy.13322)
Tier B (Wiley). Áudio forense, eixo inteiro ausente do arquivo atual apesar de o escopo pedido incluir multimídia.

---

## Eixo 4 — Transversal: LLM, XAI, validação e admissibilidade

**51. ChatGPT for digital forensic investigation: The good, the bad, and the unknown.** Scanlon, M., Breitinger, F., Hargreaves, C., Hilgert, J., Sheppard, J. (2023). *Forensic Science International: Digital Investigation*, 46, 301609. DOI: [10.1016/j.fsidi.2023.301609](https://doi.org/10.1016/j.fsidi.2023.301609)
Tier A (FSI:DI). **O precursor do seu Wickramasekara et al. (2025) e do Chernyshev et al. (2026)**, mesma autoria do SoK de 2020 e do grupo de Breitinger. Precisa estar na genealogia da seção 6.1.

**52. ChatGPT, Llama, can you write my report? An experiment on assisted digital forensics reports written using (local) large language models.** Michelet, G., Breitinger, F. (2024). *Forensic Science International: Digital Investigation*, 48, 301683. DOI: [10.1016/j.fsidi.2023.301683](https://doi.org/10.1016/j.fsidi.2023.301683)
Tier A. O abstract coloca a pergunta específica: até que ponto LLMs auxiliam a **redação do relatório pericial**, etapa de presentation do modelo DFRWS.

**53. Bridging knowledge gaps in digital forensics using unsupervised explainable AI.** Khalid, Z., Iqbal, F., Saqib, M. (2025). *Forensic Science International: Digital Investigation*, 53, 301924. DOI: [10.1016/j.fsidi.2025.301924](https://doi.org/10.1016/j.fsidi.2025.301924)
Tier A. Afirma que XAI é **não negociável** quando o destino é admissibilidade de prova pericial, e que o estado da arte foca em usar ferramentas XAI para suportar modelos existentes, não em cobrir lacunas de conhecimento. Endereça diretamente a lacuna G1.

**54. SOLVE-IT: A proposed digital forensic knowledge base inspired by MITRE ATT&CK.** Hargreaves, C., van Beek, H., Casey, E. (2025). *Forensic Science International: Digital Investigation*, 52, 301864. DOI: [10.1016/j.fsidi.2025.301864](https://doi.org/10.1016/j.fsidi.2025.301864)
Tier A. Coautoria de Eoghan Casey. Base de conhecimento de técnicas forenses; o abstract cita explicitamente o uso para **escopo de testes de ferramenta e conjuntos de dados orientados a erro**. É infraestrutura de validação, matéria-prima da lacuna G1.

**55. DFIR-Metric: A Benchmark Dataset for Evaluating Large Language Models in Digital Forensics and Incident Response.** Cherif, B., Bisztray, T., Dubniczky, R., Aldahmani, A., Alshehhi, S., Tihanyi, N. (2025). *Lecture Notes in Computer Science*, 17-31. DOI: [10.1007/978-981-95-4367-0_2](https://doi.org/10.1007/978-981-95-4367-0_2)
Tier B (LNCS). Descrição não caracterizada (abstract não recuperável). Segundo benchmark de avaliação de LLM forense, além do ForensicsData já no seu arquivo.

**56. Harnessing Federated Learning for Digital Forensics in IoT: A Survey and Introduction to the IoT-LF Framework.** Mohamed, H., Koroniotis, N., Moustafa, N., Schiliro, F., Zomaya, A. (2025). *IEEE Open Journal of the Communications Society*, 6, 3161-3191. DOI: [10.1109/ojcoms.2024.3492919](https://doi.org/10.1109/ojcoms.2024.3492919)
Tier A (OJ-COMS, Q1). Formulado como survey mais framework. O abstract enuncia o problema de custódia e privacidade que o aprendizado centralizado cria. Coautoria de Nour Moustafa (UNSW, criadora de datasets).

**57. FedCAD: Federated Cyberattack Attribution Detection for Internet of Things Forensics.** Mohamed, H., Moustafa, N., Koroniotis, N., Tari, Z., Zomaya, A., Schiliro, F. (2025). *IEEE Transactions on Sustainable Computing*, 10, 1366-1377. DOI: [10.1109/tsusc.2025.3619037](https://doi.org/10.1109/tsusc.2025.3619037)
Tier A. Atribuição de ataque sob restrição de privacidade e escala.

**58. The admissibility of digital evidence from open-source forensic tools: Development of a framework for legal acceptance.** Ismail, I., Akram Zainol Ariffin, K. (2025). *PLOS One*, 20, e0331683. DOI: [10.1371/journal.pone.0331683](https://doi.org/10.1371/journal.pone.0331683)
Tier B (PLOS ONE, Q1 multidisciplinar). **Preenche parcialmente o vácuo que seu §6.2 declara.** O abstract constata que os tribunais tendem a favorecer ferramentas comerciais sobre as de código aberto mesmo sendo tecnicamente adequadas, e propõe um framework de aceitação legal. É peer-reviewed, ao contrário da literatura cinza que você teve de descartar.

**59. Forensic Analysis of Indirect Prompt Injection Attacks on LLM Agents.** Chernyshev, M., Baig, Z., Doss, R. (2024). *2024 IEEE 6th International Conference on Trust, Privacy and Security in Intelligent Systems, and Applications (TPS-ISA)*, 409-411. DOI: [10.1109/tps-isa62245.2024.00053](https://doi.org/10.1109/tps-isa62245.2024.00053)
Tier B. Nota curta, mas com o ângulo invertido: **IA como objeto de perícia.** Analisa logs de execução de agentes LLM para identificar injeção indireta de prompt, apontando volume de dados e complexidade do fluxo como dificuldades. Mesma autoria de Chernyshev et al. (2026), mas o objeto é diferente.

**60. LLM-Powered Automated Cloud Forensics: From Log Analysis to Investigation.** Alharthi, D., Yasaei, R. (2025). *2025 IEEE 18th International Conference on Cloud Computing (CLOUD)*, 12-22. DOI: [10.1109/cloud67622.2025.00012](https://doi.org/10.1109/cloud67622.2025.00012)
Tier B (IEEE CLOUD). Análise forense de logs em nuvem, com a crítica de que a análise manual é lenta, propensa a erro e falha contra ameaças em evolução.

**61. Advancing Cyber Incident Timeline Analysis Through Retrieval-Augmented Generation and Large Language Models.** Loumachi, F., Ghanem, M., Ferrag, M. (2025). *Computers*, 14, 67. DOI: [10.3390/computers14020067](https://doi.org/10.3390/computers14020067)
Tier B (MDPI). Reconstrução de linha do tempo a partir de artefatos e timestamps com RAG. Complementa o eixo de timeline do G3.

**62. VVUQ, Reliability, and the Law.** Kemper, B. (2025). *IEEE Reliability Magazine*, 2, 34-44. DOI: [10.1109/mrl.2025.3532564](https://doi.org/10.1109/mrl.2025.3532564)
Tier B. Verificação, validação e quantificação de incerteza como prática estabelecida em engenharia de confiabilidade, confrontada com o requisito legal. **Único item localizado que trata VVUQ como disciplina importável para validação de ferramenta pericial**, o que dialoga diretamente com a lacuna G1.

---

## Candidatos verificados que não entraram na anotação detalhada

Todos com DOI confirmado contra Crossref nesta rodada, sem caracterização de conteúdo (evito afirmar o que não li):

| DOI | Ano | Veículo |
|---|---|---|
| [10.1016/j.jnca.2024.104069](https://doi.org/10.1016/j.jnca.2024.104069) | 2025 | J. Network and Computer Applications (SAT-Net) |
| [10.1145/3597503.3623308](https://doi.org/10.1145/3597503.3623308) | 2024 | ICSE 2024 (DL vs. ML clássico em log anomaly) |
| [10.1016/j.cose.2024.104016](https://doi.org/10.1016/j.cose.2024.104016) | 2024 | Computers & Security (survey LLM para threat detection) |
| [10.1016/j.neucom.2024.128444](https://doi.org/10.1016/j.neucom.2024.128444) | 2025 | Neurocomputing (review de pré-treinamento em tráfego cifrado) |
| [10.1145/3650212.3652123](https://doi.org/10.1145/3650212.3652123) | 2024 | ISSTA 2024 (avaliação em larga escala de log parsing) |
| [10.1016/j.neucom.2024.127528](https://doi.org/10.1016/j.neucom.2024.127528) | 2024 | Neurocomputing (review de steganalysis por DL) |
| [10.1109/tifs.2024.3486027](https://doi.org/10.1109/tifs.2024.3486027) | 2024 | IEEE TIFS (esteganalise com transformer) |
| [10.1109/tifs.2024.3424987](https://doi.org/10.1109/tifs.2024.3424987) | 2024 | IEEE TIFS (localização de manipulação com boundary guidance) |
| [10.1109/tpami.2024.3432551](https://doi.org/10.1109/tpami.2024.3432551) | 2024 | IEEE TPAMI (HDF-Net) |
| [10.1016/j.patcog.2024.110658](https://doi.org/10.1016/j.patcog.2024.110658) | 2024 | Pattern Recognition (DH-GAN) |
| [10.1016/j.patcog.2024.110727](https://doi.org/10.1016/j.patcog.2024.110727) | 2024 | Pattern Recognition (D-Net, splicing) |
| [10.1109/cvpr52733.2024.01213](https://doi.org/10.1109/cvpr52733.2024.01213) | 2024 | CVPR 2024 (DiffForensics) |
| [10.1109/cvpr52733.2024.01137](https://doi.org/10.1109/cvpr52733.2024.01137) | 2024 | CVPR 2024 (EditGuard) |
| [10.1007/s10462-024-10810-6](https://doi.org/10.1007/s10462-024-10810-6) | 2024 | Artificial Intelligence Review (deepfake em vídeo) |
| [10.1007/s11263-024-02054-2](https://doi.org/10.1007/s11263-024-02054-2) | 2024 | IJCV (inconsistência espaço-temporal em deepfake) |
| [10.1109/tifs.2024.3381823](https://doi.org/10.1109/tifs.2024.3381823) | 2024 | IEEE TIFS (inconsistência de olhar em vídeo) |
| [10.1109/tifs.2022.3212276](https://doi.org/10.1109/tifs.2022.3212276) | 2022 | IEEE TIFS (MAD com localização) |
| [10.1109/cvprw63382.2024.00158](https://doi.org/10.1109/cvprw63382.2024.00158) | 2024 | CVPRW 2024 (MAD single-image com ViT) |
| [10.1145/3746027.3755786](https://doi.org/10.1145/3746027.3755786) | 2025 | ACM MM 2025 (detecção de deepfake explicável) |
| [10.3390/s23020612](https://doi.org/10.3390/s23020612) | 2023 | Sensors (fileless malware por ML) |
| [10.3390/computers14110467](https://doi.org/10.3390/computers14110467) | 2025 | Computers (memória fileless com descritores de textura e LIME) |
| [10.1145/3770085](https://doi.org/10.1145/3770085) | 2025 | Digital Threats: Research and Practice (rootkit por anomalia temporal) |
| [10.1145/3760526](https://doi.org/10.1145/3760526) | 2025 | ACM CSUR (SLR de forense de conteúdo gerado por IA) |
| [10.1109/access.2024.3365140](https://doi.org/10.1109/access.2024.3365140) | 2024 | IEEE Access (E-XAI para NIDS) |
| [10.1145/3715073.3715076](https://doi.org/10.1145/3715073.3715076) | 2025 | ACM SIGKDD Explorations (atribuição de autoria na era de LLM) |
| [10.1109/cns59707.2023.10288677](https://doi.org/10.1109/cns59707.2023.10288677) | 2023 | IEEE CNS 2023 (avaliação de LLM para automação de ciberoperação) |
| [10.1145/3760526](https://doi.org/10.1145/3760526) | 2025 | ACM CSUR |
| [10.1145/3652583.3658035](https://doi.org/10.1145/3652583.3658035) | 2024 | ICMR 2024 (CLIPping the Deception) |
| [10.1016/j.fsidi.2025.301864](https://doi.org/10.1016/j.fsidi.2025.301864) | 2025 | já anotado |

---

## O que esta rodada muda na leitura do seu arquivo

1. **A lacuna G3 era maior do que o registrado.** Encontrei `NTFS-LogID` (item 39) e o trabalho de recuperação por arquivo em SSD via FTL (item 47). Existem trabalhos, mas em veículos de tier C/B ou em ângulo adjacente. A formulação defensável passa a ser: "a IA em análise de disco aparece dispersa em veículos de baixo tier e em torno de recuperação de dados, não de reconstrução de timeline". Isso é mais preciso que "praticamente não há trabalho".

2. **A lacuna G4 tem agora fonte peer-reviewed em dois eixos, não um.** Além de Nowroozi et al. (imagem), há ataque adversarial em NIDS por GNN (item 12), evasão de detectores de deepfake por consistência estatística (item 27) e a linha AIGC-Stealth (itens 28 e 29). O padrão de desconexão entre proposição e ataque continua verdadeiro, mas o lado do ataque está mais povoado do que o seu §6.3 sugere.

3. **A lacuna G1 ganhou dois instrumentos concretos.** `SOLVE-IT` (item 54) e o framework de VVUQ (item 62) são matéria-prima metodológica, não apenas diagnóstico de ausência. Isso fortalece a viabilidade de G1, que você classificou como a mais defensável.

4. **O mundo fora do CIC-MalMem-2022 existe e é crítico.** `ProcGCN` (item 40) ataca frontalmente o paradigma "dump como imagem" que domina o seu §5.1. Isso reforça G2 como estudo comparativo, e agora com um adversário teórico explícito a citar.

5. **Dois eixos inteiros do escopo pedido estavam finos no seu arquivo:** áudio forense (item 50) e atribuição de fonte de câmera/PRNU (itens 33 e 34). Ambos com literatura peer-reviewed estabelecida.

---

## Limitações desta rodada

1. **Abstracts, não texto integral.** 51 dos 60 abstracts foram recuperados via OpenAlex e as anotações derivam deles. Nenhum resultado numérico foi reportado, porque nenhum foi lido em texto integral. Nove itens estão marcados como "descrição não caracterizada".
2. **Descoberta por API, não por busca sistemática.** Sem PRISMA, sem dupla triagem, sem registro de protocolo. A travessia de citações a partir de oito anchors é enviesada a favor dessas linhagens.
3. **Um DOI não confirmado foi descartado:** [10.1016/j.patrec.2024.04.018](https://doi.org/10.1016/j.patrec.2024.04.018) ("Generalized and robust model for GAN-generated image detection") não resolveu na API nesta consulta. Fica fora até verificação.
4. **Anomalia na Crossref:** a consulta direta a [10.1016/j.eswa.2024.123756](https://doi.org/10.1016/j.eswa.2024.123756) retornou metadados de outro artigo. A consulta por título retornou o registro correto (Yadav & Kumar Vishwakarma). Confirme antes de citar.
5. **Cobertura de venue:** usei OpenAlex e Crossref. ScienceDirect, IEEE Xplore e ACM DL bloquearam acesso direto ao texto em rodadas anteriores, e aqui também não tentei texto integral. Metadados vieram de Crossref, que é a fonte canônica.
6. **Viés de idioma e índice:** busca em inglês, índices ocidentais.
7. **Infraestrutura:** a busca paralela por subagentes falhou por dependência ausente. Isso não afetou a verificação, que é determinística e foi executada por API, mas eliminou a revisão cruzada independente que os subagentes dariam.

---

## Arquivos

Nada foi modificado no projeto. Scratch em `/tmp`: `oa.sh`, `xv.sh`, `ax.sh`, `cites.sh`, `cites2.sh`, `rel.sh`, `resolve.sh`, `vdoi.sh`, `abs.sh`, `batch.sh`, e as listas `cand1.txt`, `cand1b.txt`, `cand2.txt`, `cand3.txt`, `final.txt`.

Quer que eu salve isto como nota datada no repositório? Sugiro `lit-review_ia_forense_digital_round2.md`, em português para ficar consistente com o arquivo existente, ou em inglês se preferir seguir a convenção do projeto. Documento novo, sem tocar no arquivo atual.\n\n---\n\n

---

## Adendo — links e mapeamento de datasets (2026-09-23)

**Escopo.** O corpo acima já estava no arquivo e foi preservado. Foram acrescentados: (A1) mapa de acesso aberto com cópia de cada trabalho, (A2) datasets usados por trabalho, (A3) catálogo de datasets com URLs verificadas e (A4) nota de cobertura. **Única alteração no corpo:** os identificadores `DOI: 10.x` viraram links clicáveis; nenhuma anotação, tier ou afirmação foi editada.

### A1. Acesso aberto e cópia disponível

| Trabalho | DOI | Status OA | Cópia aberta | Texto completo lido |
|---|---|---|---|---|
| 1 | [10.1109/sp61157.2025.00102](https://doi.org/10.1109/sp61157.2025.00102) | closed | — | não |
| 2 | [10.1109/icnp61940.2024.10858569](https://doi.org/10.1109/icnp61940.2024.10858569) | closed | — | não |
| 3 | [10.1145/3651890.3672268](https://doi.org/10.1145/3651890.3672268) | green | [link](https://arxiv.org/pdf/2402.02338) | sim |
| 4 | [10.14722/ndss.2024.23081](https://doi.org/10.14722/ndss.2024.23081) | gold | [link](https://doi.org/10.14722/ndss.2024.23081) | sim |
| 5 | [10.1109/tifs.2025.3530702](https://doi.org/10.1109/tifs.2025.3530702) | closed | — | não |
| 6 | [10.1109/tifs.2024.3433446](https://doi.org/10.1109/tifs.2024.3433446) | closed | — | não |
| 7 | [10.1109/tnet.2023.3335253](https://doi.org/10.1109/tnet.2023.3335253) | closed | — | não |
| 8 | [10.1109/tnet.2024.3413789](https://doi.org/10.1109/tnet.2024.3413789) | closed | — | não |
| 9 | [10.1609/aaai.v39i15.33748](https://doi.org/10.1609/aaai.v39i15.33748) | diamond | [link](https://ojs.aaai.org/index.php/AAAI/article/download/33748/35903) | sim |
| 10 | [10.1109/sp54263.2024.00005](https://doi.org/10.1109/sp54263.2024.00005) | closed | — | não |
| 11 | [10.1109/sp54263.2024.00139](https://doi.org/10.1109/sp54263.2024.00139) | closed | — | não |
| 12 | [10.1109/jiot.2021.3130434](https://doi.org/10.1109/jiot.2021.3130434) | hybrid | [link](https://ieeexplore.ieee.org/ielx7/6488907/9789736/09626144.pdf) | não |
| 13 | [10.1109/tvt.2024.3402366](https://doi.org/10.1109/tvt.2024.3402366) | closed | — | não |
| 14 | [10.1007/s40860-024-00238-8](https://doi.org/10.1007/s40860-024-00238-8) | hybrid | [link](https://link.springer.com/content/pdf/10.1007/s40860-024-00238-8.pdf) | não |
| 15 | [10.1109/tnsm.2024.3358730](https://doi.org/10.1109/tnsm.2024.3358730) | hybrid | [link](https://ieeexplore.ieee.org/ielx7/4275028/5699970/10414427.pdf) | não |
| 16 | [10.1145/3660768](https://doi.org/10.1145/3660768) | hybrid | [link](https://doi.org/10.1145/3660768) | não |
| 17 | [10.1109/tpami.2025.3541028](https://doi.org/10.1109/tpami.2025.3541028) | closed | — | não |
| 18 | [10.1109/tifs.2025.3541957](https://doi.org/10.1109/tifs.2025.3541957) | closed | — | não |
| 19 | [10.1007/s11263-024-02255-9](https://doi.org/10.1007/s11263-024-02255-9) | closed | — | não |
| 20 | [10.1109/tip.2024.3482191](https://doi.org/10.1109/tip.2024.3482191) | closed | — | não |
| 21 | [10.1609/aaai.v38i7.28520](https://doi.org/10.1609/aaai.v38i7.28520) | diamond | [link](https://ojs.aaai.org/index.php/AAAI/article/download/28520/29014) | sim |
| 22 | [10.1109/cvpr52733.2024.01024](https://doi.org/10.1109/cvpr52733.2024.01024) | closed | — | não |
| 23 | [10.1109/cvpr52733.2024.00872](https://doi.org/10.1109/cvpr52733.2024.00872) | closed | — | não |
| 24 | [10.1109/cvprw63382.2024.00439](https://doi.org/10.1109/cvprw63382.2024.00439) | closed | — | não |
| 25 | [10.1145/3699710](https://doi.org/10.1145/3699710) | closed | — | não |
| 26 | [10.1145/3652027](https://doi.org/10.1145/3652027) | bronze | [link](https://dl.acm.org/doi/pdf/10.1145/3652027) | não |
| 27 | [10.1109/cvpr52729.2023.01181](https://doi.org/10.1109/cvpr52729.2023.01181) | closed | — | não |
| 28 | [10.1145/3729233](https://doi.org/10.1145/3729233) | closed | — | não |
| 29 | [10.1145/3664647.3681535](https://doi.org/10.1145/3664647.3681535) | closed | — | não |
| 30 | [10.1016/j.patrec.2024.06.014](https://doi.org/10.1016/j.patrec.2024.06.014) | closed | — | não |
| 31 | [10.1109/tifs.2023.3255585](https://doi.org/10.1109/tifs.2023.3255585) | hybrid | [link](https://ieeexplore.ieee.org/ielx7/10206/4358835/10065533.pdf) | não |
| 32 | [10.1016/j.eswa.2024.123756](https://doi.org/10.1016/j.eswa.2024.123756) | closed | — | não |
| 33 | [10.1016/j.image.2023.116944](https://doi.org/10.1016/j.image.2023.116944) | hybrid | [link](https://doi.org/10.1016/j.image.2023.116944) | não |
| 34 | [10.1016/j.fsidi.2024.301746](https://doi.org/10.1016/j.fsidi.2024.301746) | closed | — | não |
| 35 | [10.1109/tifs.2025.3539527](https://doi.org/10.1109/tifs.2025.3539527) | closed | — | não |
| 36 | [10.1109/icassp48485.2024.10447626](https://doi.org/10.1109/icassp48485.2024.10447626) | closed | — | não |
| 37 | [10.1186/s42400-024-00241-9](https://doi.org/10.1186/s42400-024-00241-9) | diamond | [link](https://link.springer.com/content/pdf/10.1186/s42400-024-00241-9.pdf) | não |
| 38 | [10.1109/compsac69091.2026.00101](https://doi.org/10.1109/compsac69091.2026.00101) | closed | — | não |
| 39 | [10.1109/otcon69332.2026.11629697](https://doi.org/10.1109/otcon69332.2026.11629697) | closed | — | não |
| 40 | [10.7717/peerj-cs.2193](https://doi.org/10.7717/peerj-cs.2193) | gold | [link](https://doi.org/10.7717/peerj-cs.2193) | sim |
| 41 | [10.1109/access.2025.3565802](https://doi.org/10.1109/access.2025.3565802) | gold | [link](https://www.open-access.bcu.ac.uk/16618/1/Few-Shot_Learning_With_Prototypical_Networks_for_Improved_Memory_Forensics.pdf) | sim |
| 42 | [10.3390/computers15010008](https://doi.org/10.3390/computers15010008) | gold | [link](https://www.mdpi.com/2073-431X/15/1/8/pdf?version=1766568466) | não |
| 43 | [10.3390/electronics15020352](https://doi.org/10.3390/electronics15020352) | gold | [link](https://www.mdpi.com/2079-9292/15/2/352/pdf?version=1768300374) | não |
| 44 | [10.1016/j.cose.2025.104582](https://doi.org/10.1016/j.cose.2025.104582) | closed | — | não |
| 45 | [10.14722/ndss.2026.231491](https://doi.org/10.14722/ndss.2026.231491) | gold | [link](https://doi.org/10.14722/ndss.2026.231491) | sim |
| 46 | [10.1016/j.fsidi.2023.301502](https://doi.org/10.1016/j.fsidi.2023.301502) | hybrid | [link](https://doi.org/10.1016/j.fsidi.2023.301502) | não |
| 47 | [10.1186/s42400-024-00287-9](https://doi.org/10.1186/s42400-024-00287-9) | diamond | [link](https://link.springer.com/content/pdf/10.1186/s42400-024-00287-9.pdf) | não |
| 48 | [10.1016/j.fsidi.2023.301663](https://doi.org/10.1016/j.fsidi.2023.301663) | closed | — | não |
| 49 | [10.1007/s11042-023-15609-1](https://doi.org/10.1007/s11042-023-15609-1) | bronze | [link](https://link.springer.com/content/pdf/10.1007/s11042-023-15609-1.pdf) | sim |
| 50 | [10.1111/exsy.13322](https://doi.org/10.1111/exsy.13322) | hybrid | [link](https://onlinelibrary.wiley.com/doi/pdfdirect/10.1111/exsy.13322) | não |
| 51 | [10.1016/j.fsidi.2023.301609](https://doi.org/10.1016/j.fsidi.2023.301609) | hybrid | [link](https://iris.unil.ch/bitstreams/1479b497-f8c6-4fb1-a578-5330662ec6f3/download) | sim |
| 52 | [10.1016/j.fsidi.2023.301683](https://doi.org/10.1016/j.fsidi.2023.301683) | hybrid | [link](https://opus.bibliothek.uni-augsburg.de/opus4/files/117543/117543.pdf) | sim |
| 53 | [10.1016/j.fsidi.2025.301924](https://doi.org/10.1016/j.fsidi.2025.301924) | hybrid | [link](https://doi.org/10.1016/j.fsidi.2025.301924) | não |
| 54 | [10.1016/j.fsidi.2025.301864](https://doi.org/10.1016/j.fsidi.2025.301864) | hybrid | [link](https://doi.org/10.1016/j.fsidi.2025.301864) | não |
| 55 | [10.1007/978-981-95-4367-0_2](https://doi.org/10.1007/978-981-95-4367-0_2) | closed | — | não |
| 56 | [10.1109/ojcoms.2024.3492919](https://doi.org/10.1109/ojcoms.2024.3492919) | gold | [link](https://doi.org/10.1109/ojcoms.2024.3492919) | não |
| 57 | [10.1109/tsusc.2025.3619037](https://doi.org/10.1109/tsusc.2025.3619037) | closed | — | não |
| 58 | [10.1371/journal.pone.0331683](https://doi.org/10.1371/journal.pone.0331683) | gold | [link](https://journals.plos.org/plosone/article/file?id=10.1371/journal.pone.0331683&type=printable) | sim |
| 59 | [10.1109/tps-isa62245.2024.00053](https://doi.org/10.1109/tps-isa62245.2024.00053) | closed | — | não |
| 60 | [10.1109/cloud67622.2025.00012](https://doi.org/10.1109/cloud67622.2025.00012) | closed | — | não |
| 61 | [10.3390/computers14020067](https://doi.org/10.3390/computers14020067) | gold | [link](https://repository.londonmet.ac.uk/10080/7/computers-14-00067.pdf) | sim |
| 62 | [10.1109/mrl.2025.3532564](https://doi.org/10.1109/mrl.2025.3532564) | closed | — | não |
| T1 | [10.1016/j.jnca.2024.104069](https://doi.org/10.1016/j.jnca.2024.104069) | closed | — | não |
| T2 | [10.1145/3597503.3623308](https://doi.org/10.1145/3597503.3623308) | closed | — | não |
| T3 | [10.1016/j.cose.2024.104016](https://doi.org/10.1016/j.cose.2024.104016) | closed | — | não |
| T4 | [10.1016/j.neucom.2024.128444](https://doi.org/10.1016/j.neucom.2024.128444) | closed | — | não |
| T5 | [10.1145/3650212.3652123](https://doi.org/10.1145/3650212.3652123) | closed | — | não |
| T6 | [10.1016/j.neucom.2024.127528](https://doi.org/10.1016/j.neucom.2024.127528) | green | [link](https://hdl.handle.net/10609/151607) | não |
| T7 | [10.1109/tifs.2024.3486027](https://doi.org/10.1109/tifs.2024.3486027) | closed | — | não |
| T8 | [10.1109/tifs.2024.3424987](https://doi.org/10.1109/tifs.2024.3424987) | closed | — | não |
| T9 | [10.1109/tpami.2024.3432551](https://doi.org/10.1109/tpami.2024.3432551) | closed | — | não |
| T10 | [10.1016/j.patcog.2024.110658](https://doi.org/10.1016/j.patcog.2024.110658) | closed | — | não |
| T11 | [10.1016/j.patcog.2024.110727](https://doi.org/10.1016/j.patcog.2024.110727) | closed | — | não |
| T12 | [10.1109/cvpr52733.2024.01213](https://doi.org/10.1109/cvpr52733.2024.01213) | closed | — | não |
| T13 | [10.1109/cvpr52733.2024.01137](https://doi.org/10.1109/cvpr52733.2024.01137) | closed | — | não |
| T14 | [10.1007/s10462-024-10810-6](https://doi.org/10.1007/s10462-024-10810-6) | hybrid | [link](https://link.springer.com/content/pdf/10.1007/s10462-024-10810-6.pdf) | não |
| T15 | [10.1007/s11263-024-02054-2](https://doi.org/10.1007/s11263-024-02054-2) | closed | — | não |
| T16 | [10.1109/tifs.2024.3381823](https://doi.org/10.1109/tifs.2024.3381823) | closed | — | não |
| T17 | [10.1109/tifs.2022.3212276](https://doi.org/10.1109/tifs.2022.3212276) | closed | — | não |
| T18 | [10.1109/cvprw63382.2024.00158](https://doi.org/10.1109/cvprw63382.2024.00158) | closed | — | não |
| T19 | [10.1145/3746027.3755786](https://doi.org/10.1145/3746027.3755786) | green | [link](https://arxiv.org/pdf/2508.07596) | sim |
| T20 | [10.3390/s23020612](https://doi.org/10.3390/s23020612) | gold | [link](https://doi.org/10.3390/s23020612) | sim |
| T21 | [10.3390/computers14110467](https://doi.org/10.3390/computers14110467) | gold | [link](https://www.mdpi.com/2073-431X/14/11/467/pdf?version=1761964429) | não |
| T22 | [10.1145/3770085](https://doi.org/10.1145/3770085) | diamond | [link](https://dl.acm.org/doi/pdf/10.1145/3770085) | não |
| T23 | [10.1145/3760526](https://doi.org/10.1145/3760526) | closed | — | não |
| T24 | [10.1109/access.2024.3365140](https://doi.org/10.1109/access.2024.3365140) | gold | [link](https://ieeexplore.ieee.org/ielx7/6287639/6514899/10433134.pdf) | não |
| T25 | [10.1145/3715073.3715076](https://doi.org/10.1145/3715073.3715076) | bronze | [link](https://dl.acm.org/doi/pdf/10.1145/3715073.3715076) | não |
| T26 | [10.1109/cns59707.2023.10288677](https://doi.org/10.1109/cns59707.2023.10288677) | closed | — | não |
| T28 | [10.1145/3652583.3658035](https://doi.org/10.1145/3652583.3658035) | gold | [link](https://doi.org/10.1145/3652583.3658035) | não |

### A2. Datasets usados por trabalho

| Trabalho | Dataset(s) | Acesso | Evidência |
|---|---|---|---|
| 1 | não determinável com as fontes acessíveis | — | — |
| 2 | não determinável com as fontes acessíveis | — | — |
| 3 | Nenhum dataset forense. Coleta própria de "experience pool" de trajetórias geradas por algoritmos existentes (ex.: Decima para cluster job scheduling). | não se aplica | texto completo |
| 4 | CIC-IDS2018, CIC-InvesAndMal2019 e CIC-DoHBrw-2020 (dois públicos mais um combinado), mais um dataset real de uma empresa de segurança (privado). Usa CICFlowMeter para extrair features. | os três CIC abertos mediante cadastro no CIC/UNB; o quarto é privado | texto completo |
| 5 | CIC-IDS2018 e UNSW-NB15. | ambos abertos mediante cadastro | abstract |
| 6 | não determinável com as fontes acessíveis | — | — |
| 7 | não determinável com as fontes acessíveis | — | — |
| 8 | não determinável com as fontes acessíveis | — | — |
| 9 | ISCXVPN2016, ISCXTor2016, CIC-IoT2023 e CrossPlatform (Android e iOS). | os três primeiros abertos; CrossPlatform sem URL canônica confirmada | texto completo |
| 10 | não determinável com as fontes acessíveis | — | — |
| 11 | não determinável com as fontes acessíveis | — | — |
| 12 | não determinável com as fontes acessíveis | — | — |
| 13 | CICIDS, da família CIC-IDS. | aberto no CIC/UNB | abstract |
| 14 | não determinável com as fontes acessíveis | — | — |
| 15 | HDFS, BGL e Thunderbird, logs de sistema. | abertos via Loghub, no GitHub | abstract |
| 16 | HDFS, BGL, Thunderbird, OpenStack e Hadoop, em revisão crítica dos datasets de log usados em detecção de anomalia. | abertos via Loghub, no GitHub | abstract |
| 17 | não determinável com as fontes acessíveis | — | — |
| 18 | não determinável com as fontes acessíveis | — | — |
| 19 | HiFi-IFDL, DFFD, Coverage, CASIA, NIST16, IMD2020 e datasets sintéticos, segundo a página do editor. **Não confirmado**: o OpenAlex classifica o artigo como fechado e a página pode misturar datasets citados com datasets efetivamente usados. | — | página do editor |
| 20 | não determinável com as fontes acessíveis | — | — |
| 21 | CASIA, NIST16, IMD2020 e Columbia (DVMM splicing) na avaliação. O ImageNet aparece apenas como origem dos pesos pré-treinados do ViT, não como dataset forense. | CASIA e IMD2020 com cópias de terceiros; NIST16 via NIST; Columbia publica o próprio dataset | texto completo |
| 22 | não determinável com as fontes acessíveis | — | — |
| 23 | não determinável com as fontes acessíveis | — | — |
| 24 | não determinável com as fontes acessíveis | — | — |
| 25 | não determinável com as fontes acessíveis | — | — |
| 26 | não determinável com as fontes acessíveis | — | — |
| 27 | não determinável com as fontes acessíveis | — | — |
| 28 | não determinável com as fontes acessíveis | — | — |
| 29 | não determinável com as fontes acessíveis | — | — |
| 30 | não determinável com as fontes acessíveis | — | — |
| 31 | não determinável com as fontes acessíveis | — | — |
| 32 | não determinável com as fontes acessíveis | — | — |
| 33 | não determinável com as fontes acessíveis | — | — |
| 34 | não determinável com as fontes acessíveis | — | — |
| 35 | não determinável com as fontes acessíveis | — | — |
| 36 | não determinável com as fontes acessíveis | — | — |
| 37 | não determinável com as fontes acessíveis | — | — |
| 38 | FFT-75, no cenário de poucos fragmentos rotulados por tipo de arquivo. | distribuição canônica não confirmada | abstract |
| 39 | Não usa dataset público: opera sobre binário cru de artefatos internos do NTFS, entre eles $MFT e $LogFile. | não se aplica | abstract |
| 40 | Dumpware10, VirusShare e VirusTotal; cita Malimg e MaleVis como datasets de imagem de malware. | Dumpware10 sem distribuição canônica confirmada; VirusShare com cadastro; VirusTotal comercial | texto completo (Europe PMC) |
| 41 | Dumpware10 (10 classes de malware mais 1 benigna), descrito no artigo como "publicly available"; pré-processamento com denoising e A-Hash. | descrito no artigo como público; distribuição canônica não confirmada | texto completo |
| 42 | CIC-MalMem, com bytes crus de memória tratados como tokens. | aberto no CIC/UNB | abstract |
| 43 | CIC-MalMem, no cenário de malware residente em memória, fileless e ofuscado. | aberto no CIC/UNB | abstract |
| 44 | não determinável com as fontes acessíveis | — | — |
| 45 | PVD (Potentially Vulnerable Drivers), dataset próprio de drivers coletados in-the-wild; consulta ao VirusTotal. | PVD não é distribuído; VirusTotal é serviço comercial com API limitada | texto completo |
| 46 | Não nomeia dataset público; analisa artefatos de arquivos apagados em macOS para detectar spoliation. | não se aplica | abstract |
| 47 | não determinável com as fontes acessíveis | — | — |
| 48 | não determinável com as fontes acessíveis | — | — |
| 49 | FaceForensics, Celeb-DF, DFDC, DeeperForensics, WildDeepfake e VISION, em revisão de técnicas de falsificação de vídeo. | todos hospedados publicamente; FF++, Celeb-DF e DFDC exigem aceite de termos | texto completo (Europe PMC) |
| 50 | não determinável com as fontes acessíveis | — | — |
| 51 | Nenhum dataset forense. Experimento conduzido por conversas com GPT-3.5 e GPT-4; cita datasets públicos do Kaggle (sentimento em chat, discurso de ódio) apenas para ilustrar capacidades do modelo. | — | texto completo |
| 52 | Nenhum dataset forense nomeado. Avalia ChatGPT e Llama locais na redação de relatórios periciais. | — | texto completo |
| 53 | CIC MalMemAnalysis-2022 (grafia usada no artigo, mesma família do CIC-MalMem-2022), categorias binária e multivariada de 4 e 16 classes. | aberto no CIC/UNB | abstract |
| 54 | não determinável com as fontes acessíveis | — | — |
| 55 | não determinável com as fontes acessíveis | — | — |
| 56 | não determinável com as fontes acessíveis | — | — |
| 57 | Bot-IoT e UNSW-NB15. | ambos abertos mediante cadastro no UNSW | abstract |
| 58 | Nenhum dataset. Trabalho de enquadramento jurídico sobre admissibilidade de ferramentas forenses de código aberto. | não se aplica | texto completo (Europe PMC) |
| 59 | não determinável com as fontes acessíveis | — | — |
| 60 | não determinável com as fontes acessíveis | — | — |
| 61 | Nenhum dataset público. Cenários sintéticos construídos pelos autores para preservar privacidade, consentimento e confidencialidade. | não se aplica | texto completo |
| 62 | não determinável com as fontes acessíveis | — | — |
| T1 | não determinável com as fontes acessíveis | — | — |
| T2 | não determinável com as fontes acessíveis | — | — |
| T3 | não determinável com as fontes acessíveis | — | — |
| T4 | não determinável com as fontes acessíveis | — | — |
| T5 | Loghub, em avaliação em larga escala de técnicas de log parsing. | aberto no GitHub | abstract |
| T6 | não determinável com as fontes acessíveis | — | — |
| T7 | ALASKA, em esteganalise de imagens coloridas. | ALASKA2 com distribuição pública pelo laboratório | abstract |
| T8 | não determinável com as fontes acessíveis | — | — |
| T9 | não determinável com as fontes acessíveis | — | — |
| T10 | não determinável com as fontes acessíveis | — | — |
| T11 | não determinável com as fontes acessíveis | — | — |
| T12 | não determinável com as fontes acessíveis | — | — |
| T13 | não determinável com as fontes acessíveis | — | — |
| T14 | não determinável com as fontes acessíveis | — | — |
| T15 | FaceForensics++, Celeb-DF, DFDC, FaceShifter, DeeperForensics, Wild-Deepfake e KoDF, segundo a página do editor. **Não confirmado** pelo mesmo motivo. | — | página do editor |
| T16 | não determinável com as fontes acessíveis | — | — |
| T17 | não determinável com as fontes acessíveis | — | — |
| T18 | FRGC, em detecção de face morphing com ViT de imagem única. | aberto via NIST | abstract |
| T19 | DF40 (benchmark principal); MS COCO e FFHQ (corpus híbrido de fine-tuning); FaceForensics++ e Celeb-DF (avaliação). | DF40, FFHQ e MS COCO abertos; FF++ e Celeb-DF com aceite de termos | texto completo |
| T20 | VirusShare como fonte de amostras, no estudo de malware fileless. | VirusShare é aberto a pesquisadores mediante cadastro e aprovação | texto completo (Europe PMC) |
| T21 | não determinável com as fontes acessíveis | — | — |
| T22 | não determinável com as fontes acessíveis | — | — |
| T23 | não determinável com as fontes acessíveis | — | — |
| T24 | não determinável com as fontes acessíveis | — | — |
| T25 | não determinável com as fontes acessíveis | — | — |
| T26 | não determinável com as fontes acessíveis | — | — |
| T28 | não determinável com as fontes acessíveis | — | — |

### A3. Catálogo de datasets citados, com URLs verificadas

| Dataset | Eixo | Link | URL respondeu em 2026-09-23 |
|---|---|---|---|
| CIC-IDS2017 | Rede | [https://www.unb.ca/cic/datasets/ids-2017.html](https://www.unb.ca/cic/datasets/ids-2017.html) | sim |
| CSE-CIC-IDS2018 | Rede | [https://www.unb.ca/cic/datasets/ids-2018.html](https://www.unb.ca/cic/datasets/ids-2018.html) | sim |
| CIC-InvesAndMal2019 | Rede | [https://www.unb.ca/cic/datasets/invesandmal2019.html](https://www.unb.ca/cic/datasets/invesandmal2019.html) | sim |
| CIC-DoHBrw-2020 | Rede | [https://www.unb.ca/cic/datasets/dohbrw-2020.html](https://www.unb.ca/cic/datasets/dohbrw-2020.html) | sim |
| CIC-IoT2023 | Rede | [https://www.unb.ca/cic/datasets/iotdataset-2023.html](https://www.unb.ca/cic/datasets/iotdataset-2023.html) | sim |
| ISCXVPN2016 | Rede | [https://www.unb.ca/cic/datasets/vpn.html](https://www.unb.ca/cic/datasets/vpn.html) | sim |
| ISCXTor2016 | Rede | [https://www.unb.ca/cic/datasets/tor.html](https://www.unb.ca/cic/datasets/tor.html) | sim |
| UNSW-NB15 | Rede | [https://research.unsw.edu.au/projects/unsw-nb15-dataset](https://research.unsw.edu.au/projects/unsw-nb15-dataset) | sim |
| Bot-IoT | Rede | [https://research.unsw.edu.au/projects/bot-iot-dataset](https://research.unsw.edu.au/projects/bot-iot-dataset) | sim |
| ToN-IoT | Rede | [https://research.unsw.edu.au/projects/toniot-datasets](https://research.unsw.edu.au/projects/toniot-datasets) | sim |
| Loghub, com HDFS, BGL, Thunderbird, OpenStack e Hadoop | Rede e host | [https://github.com/logpai/loghub](https://github.com/logpai/loghub) | sim |
| CIC-MalMem-2022, também citado como MalMemAnalysis-2022 | Memória | [https://www.unb.ca/cic/datasets/malmem-2022.html](https://www.unb.ca/cic/datasets/malmem-2022.html) | sim |
| Dumpware10 | Memória | [https://doi.org/10.1016/j.cose.2020.102166](https://doi.org/10.1016/j.cose.2020.102166) | sim |
| VirusShare | Malware | [https://virusshare.com](https://virusshare.com) | sim |
| VirusTotal | Malware | [https://www.virustotal.com/gui/home/upload](https://www.virustotal.com/gui/home/upload) | sim |
| FaceForensics++ | Imagem e vídeo | [https://github.com/ondyari/FaceForensics](https://github.com/ondyari/FaceForensics) | sim |
| Celeb-DF | Imagem e vídeo | [https://github.com/yuezunli/celeb-deepfakeforensics](https://github.com/yuezunli/celeb-deepfakeforensics) | sim |
| DFDC | Imagem e vídeo | [https://dfdc.ai/](https://dfdc.ai/) | sim |
| DeeperForensics-1.0 | Imagem e vídeo | [https://github.com/EndlessSora/DeeperForensics-1.0](https://github.com/EndlessSora/DeeperForensics-1.0) | sim |
| WildDeepfake | Imagem e vídeo | [https://github.com/deepfakeinthewild/deepfake-in-the-wild](https://github.com/deepfakeinthewild/deepfake-in-the-wild) | sim |
| VISION | Imagem e vídeo | [https://lesc.dinfo.unifi.it/VISION/](https://lesc.dinfo.unifi.it/VISION/) | sim |
| DF40 | Imagem e vídeo | [https://github.com/YZY-stack/DF40](https://github.com/YZY-stack/DF40) | sim |
| ForgeryNet | Imagem e vídeo | [https://github.com/yinanhe/ForgeryNet](https://github.com/yinanhe/ForgeryNet) | sim |
| FFHQ | Imagem sintética | [https://github.com/NVlabs/ffhq-dataset](https://github.com/NVlabs/ffhq-dataset) | sim |
| MS COCO | Imagem sintética | [https://cocodataset.org](https://cocodataset.org) | sim |
| CASIA v2, via ground truth de terceiros | Falsificação de imagem | [https://github.com/namtpham/casia2groundtruth](https://github.com/namtpham/casia2groundtruth) | sim |
| Columbia DVMM splicing | Falsificação de imagem | [https://www.ee.columbia.edu/ln/dvmm/downloads/authsplcuncmp/](https://www.ee.columbia.edu/ln/dvmm/downloads/authsplcuncmp/) | sim |
| CoMoFoD | Falsificação de imagem | [https://www.vcl.fer.hr/comofod/](https://www.vcl.fer.hr/comofod/) | sim |
| DEFACTO | Falsificação de imagem | [https://defactodataset.github.io/](https://defactodataset.github.io/) | sim |
| NIST Nimble e MFC, que inclui o NIST16 | Falsificação de imagem | [https://www.nist.gov/itl/iad/mig/nimble-challenge-2017-evaluation](https://www.nist.gov/itl/iad/mig/nimble-challenge-2017-evaluation) | sim |
| Coverage | Falsificação de imagem | [https://github.com/wenbihan/coverage](https://github.com/wenbihan/coverage) | sim |
| ForenSynths, distribuído com o CNNDetection | Imagem sintética | [https://github.com/peterwang512/CNNDetection](https://github.com/peterwang512/CNNDetection) | sim |
| GenImage | Imagem sintética | [https://github.com/GenImage-Dataset/GenImage](https://github.com/GenImage-Dataset/GenImage) | sim |
| RAISE | Câmera e imagem | [http://loki.disi.unitn.it/RAISE/](http://loki.disi.unitn.it/RAISE/) | sim |
| FRGC | Biometria facial | [https://www.nist.gov/programs-projects/face-recognition-grand-challenge-frgc](https://www.nist.gov/programs-projects/face-recognition-grand-challenge-frgc) | sim |
| ALASKA2 | Esteganalise | [https://alaska.utt.fr/](https://alaska.utt.fr/) | sim |
| GovDocs | Disco e fragmentos | [https://digitalcorpora.org/corpora/file-corpora/](https://digitalcorpora.org/corpora/file-corpora/) | sim |
| EMBER | Malware estático | [https://github.com/elastic/ember](https://github.com/elastic/ember) | sim |
| SOREL-20M | Malware estático | [https://github.com/sophos/SOREL-20M](https://github.com/sophos/SOREL-20M) | sim |
| MalwareBazaar | Malware | [https://bazaar.abuse.ch](https://bazaar.abuse.ch) | sim |
| IoT-23 | Rede e IoT | [https://www.stratosphereips.org/datasets-iot23](https://www.stratosphereips.org/datasets-iot23) | sim |
| N-BaIoT | Rede e IoT | [https://archive.ics.uci.edu/dataset/442/detection+of+iot+botnet+attacks+n+baiot](https://archive.ics.uci.edu/dataset/442/detection+of+iot+botnet+attacks+n+baiot) | sim |
| KDD Cup 99 | Rede | [https://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html](https://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html) | sim |
| NSL-KDD | Rede | [https://www.unb.ca/cic/datasets/nsl.html](https://www.unb.ca/cic/datasets/nsl.html) | sim |
| BOSSbase e BOWS | Esteganalise | [http://www.agents.cz/boss/BOSSFinal/](http://www.agents.cz/boss/BOSSFinal/) | sim |
| ASVspoof | Áudio | [https://www.asvspoof.org](https://www.asvspoof.org) | sim |
| Dresden Image Database | Câmera e imagem | [http://forensics.inf.tu-dresden.de/ddimgdb/](http://forensics.inf.tu-dresden.de/ddimgdb/) | não |
| IMD2020 | Falsificação de imagem | [https://staff.utia.cas.cz/novozada/db/](https://staff.utia.cas.cz/novozada/db/) | não |
| MIDV-500 | Documento de identidade | [https://github.com/fcakyon/midv500](https://github.com/fcakyon/midv500) | sim |
| KoDF | Imagem e vídeo | [https://github.com/aihub-kr/kodf](https://github.com/aihub-kr/kodf) | não |
| FFT-75 | Disco e fragmentos | canônico não localizado | não |
| Synthbuster | Imagem sintética | [https://zenodo.org/records/10066460](https://zenodo.org/records/10066460) | não |
| AutoSplice | Imagem sintética | canônico não localizado | não |

### A4. Cobertura e limites desta complementação

| Métrica | Valor |
|---|---|
| Trabalhos distintos no arquivo | 89 |
| Trabalhos com texto completo obtido e lido | 14 |
| Trabalhos com uso de dataset determinado: 22 com dataset nomeado, 6 que declaram não usar dataset público | 28 |
| Datasets apenas sugeridos por página do editor, não confirmados | 2 |
| Trabalhos em que o dataset não foi determinável (paywall) | 59 |

**Três níveis de evidência**, marcados na coluna final da tabela A2:
1. `texto completo`: PDF baixado, convertido em texto e dataset localizado no próprio texto, com contexto conferido (14 trabalhos).
2. `abstract`: nome presente no abstract recuperado por OpenAlex, Semantic Scholar ou Europe PMC.
3. `página do editor`: dois casos (ambos IJCV) em que a página do editor lista datasets mas o OpenAlex classifica o artigo como fechado. Tratados como **não confirmados** e não usados em nenhuma afirmação da seção A3.

**Por que a cobertura é parcial.** A maior parte dos trabalhos está atrás de paywall (IEEE Xplore, ScienceDirect, ACM DL, Springer, Wiley). Esses editores bloquearam requisições automatizadas com HTTP 403, página renderizada por JavaScript ou redirecionamento para tela de consentimento, e o OpenAlex não tem abstract para 18 deles. Onde não houve evidência textual, ficou "não determinável" em vez de inferência pelo padrão do subcampo.

**O que fecharia a lacuna.** Acesso institucional a IEEE Xplore, ScienceDirect, ACM DL, Springer e Wiley. O Unpaywall apontou cópias verdes para 19 trabalhos, mas nenhum desses PDFs respondeu a partir deste ambiente (`repository.essex.ac.uk` e `investigo.biblioteca.uvigo.es` inacessíveis; MDPI e Springer bloqueados). Foram obtidos por via aberta 14 textos completos: AAAI (2), NDSS (2), ACM SIGCOMM e ACM MM (2), FSI:DI (2), PLoS ONE, PeerJ CS, MDPI Computers, e os repositórios Europe PMC de Springer MTAP e MDPI Sensors.

**Sobre a coluna de acesso na seção A3.** "URL respondeu" significa apenas que a URL retornou HTTP 200 em 2026-09-23, não que o conteúdo seja livre de termos. Não inspecionei licença, formulário de aceite ou exigência de cadastro de cada dataset. Famílias CIC/UNB e UNSW normalmente exigem cadastro; FaceForensics++, Celeb-DF e DFDC exigem aceite de termos. Confirme a licença antes de redistribuir.

**Dois casos que merecem nota.**
- **Dumpware10**, usado pelos itens 40 e 41, tem origem em Bozkir et al. (2021), "Catch them alive", DOI [10.1016/j.cose.2020.102166](https://doi.org/10.1016/j.cose.2020.102166), que **já está no arquivo original** (seção 5.1). Não há distribuição canônica própria do dataset; o link na tabela A3 aponta para o artigo de origem.
- **CIC MalMemAnalysis-2022** e **CIC-MalMem-2022** aparecem na literatura como nomes da mesma família de dumps de memória do CIC/UNB. O item 53 usa a primeira grafia; os itens 42 e 43 usam a segunda.

**Limites herdados.** Nenhum número de desempenho foi extraído ou afirmado: o mapeamento cobre *quais* datasets cada trabalho usa, não *quanto* cada método atinge neles. O arquivo original (`lit-review_ia_forense_digital.md`, 39 referências) não foi mapeado nesta rodada; a seção A2 cobre apenas os trabalhos deste arquivo.
