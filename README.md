# Spanish-HateSpeech-FeatureEvaluation
## Evaluating Linguistic, Negation-Based and Modern Features for Hate Speech Detection in Spanish  

### TL;DR: Highlights

- We perform a **systematic evaluation of feature sets** for Spanish hate-speech detection across multiple datasets.  
- We assess:
  - **UMUTextStats**: a suite of linguistic features designed at the University of Murcia.
  - **Negation-aware features**, tailored to Spanish morphosyntax.
  - **Modern embeddings and representations** (FastText, sentence embeddings, transformer-based features).
- Experiments demonstrate that **linguistic features remain highly competitive**, especially in low-data or noisy-domain scenarios.
- Negation features show strong discriminative power on datasets containing sarcasm or implicit abuse.
- Best results are obtained by **combining LFs + modern features**, outperforming individual feature families.

### Authors

- **José Antonio García-Díaz** — University of Murcia (UMUTeam)  
  [Google Scholar](https://scholar.google.com/citations?user=ek7NIYUAAAAJ) · [ORCID](https://orcid.org/0000-0002-3651-2660)

- **Salud María Jiménez-Zafra** — University of Jaén (SINAI Research Group)  
  [Google Scholar](https://scholar.google.com/citations?user=MWoIiqgAAAAJ) · [ORCID](https://orcid.org/0000-0003-3274-8825)  

- **Miguel Ángel García Cumbreras** — University of Jaén (SINAI Research Group)  
  [Google Scholar](https://scholar.google.es/citations?user=SZy5QHQAAAAJ) · [ORCID](https://orcid.org/0000-0003-3274-8825)  

- **Rafael Valencia-García** — University of Murcia  
  [Google Scholar](https://scholar.google.com/citations?user=GLpBPNMAAAAJ) · [ORCID](https://orcid.org/0000-0003-1867-9587)

> Collaboration between **UMUTeam (University of Murcia)** and **SINAI (University of Jaén)**.

### Abstract

The rise of social networks has allowed misogynistic, xenophobic, and homophobic people to spread their hate-speech to intimidate individuals or groups because of their gender, ethnicity or sexual orientation. The consequences of hate-speech are devastating, causing severe depression and even leading people to commit suicide. Hate-speech identification is challenging as the large amount of daily publications makes it impossible to review every comment by hand. Moreover, hate-speech is also spread by hoaxes that requires language and context understanding. With the aim of reducing the number of comments that should be reviewed by experts, or even for the development of autonomous systems, the automatic identification of hate-speech has gained academic relevance. However, the reliability of automatic approaches is still limited specifically in languages other than English, in which some of the state-of-the-art techniques have not been analysed in detail. In this work, we examine which features are most effective in identifying hate-speech in Spanish and how these features can be combined to develop more accurate systems. In addition, we characterize the language present in each type of hate-speech by means of explainable linguistic features and compare our results with state-of-the-art approaches. Our research indicates that combining linguistic features and transformers by means of knowledge integration outperforms current solutions regarding hate-speech identification in Spanish.

### Publication

**Feature engineering for hate speech and offensive language detection in Spanish: an extensive evaluation using linguistic features and modern text representations**  
*Complex & Intelligent Systems*, 2023  
https://doi.org/10.1007/s40747-022-00693-x

---


### Feature Sets Evaluated
#### **1. UMUTextStats (Linguistic Features)**  
A suite of **lexical, morphosyntactic, stylistic and readability metrics** extracted with UMUTextStats tool.

Includes features such as:
- Syllable patterns  
- Word-length distributions  
- POS-based ratios  
- Transitivity markers  
- Colloquialism density  
- Readability indices  
- Average sentence complexity  

These features are lightweight and fast to compute, making them ideal for low-resource environments.

#### **2. Negation-Based Features**

Spanish negation expresses polarity through:
- "no" + verb  
- double negation (“nunca”, “jamás”, “tampoco”)  
- clitic interactions (e.g., “no me lo creo”)  
- negative determiners (“ningún”, “ninguna”)  

We extract:
- negation frequency  
- negated-verb ratios  
- distance-based negation scores  
- negation-as-scope indicators  

These features improve disambiguation of **implicit hate** and **sarcastic formulations**.

#### **3. Modern Representations**

We also evaluate:
- **FastText Embeddings (Spanish Wikipedia + CC)**
- **Sentence Embeddings** (SBERT-like models)
- **Transformer-based contextual embeddings**  
  (e.g., BETO hidden states, pooled representations)

These are used either directly or concatenated with LFs.


### Corpora Evaluated

### Corpus Statistics (Size Overview)

Spanish MisoCorpus 2020 (https://github.com/NLP-UMUTeam/Spanish-MisoCorpus-2020)
| Label         | Train | Development | Test | Total |
|---------------|------:|------------:|-----:|------:|
| non-misogyny  | 2797  | 948         | 945  | 4690  |
| misogyny      | 2237  | 730         | 733  | 3700  |
| **total**     | **5034** | **1678** | **1678** | **8390** |

AMI 2018 (https://ceur-ws.org/Vol-2150/overview-AMI.pdf)
| Label         | Train | Development | Test | Total |
|---------------|------:|------------:|-----:|------:|
| non-misogyny  | 1253  | 422         | 416  | 2074  |
| misogyny      | 1227  | 405         | 415  | 2064  |
| **total**     | **2480** | **827** | **831** | **4138** |

HaterNET (https://zenodo.org/records/2592149)
| Label        | Train | Development | Test | Total |
|--------------|------:|------------:|-----:|------:|
| non-hateful  | 2667  | 875         | 891  | 3600  |
| hateful      | 933   | 325         | 309  | 1567  |
| **total**    | **3600** | **1200** | **1200** | **6000** |

HatEval 2019 (https://aclanthology.org/S19-2007/)
| Label        | Train | Development | Test | Total |
|--------------|------:|------------:|-----:|------:|
| non-hateful  | 2643  | 278         | 939  | 3860  |
| hateful      | 1857  | 222         | 660  | 2739  |
| **total**    | **4500** | **500** | **1599** | **6599** |


### Evaluation
Next, we provide accuracy (Acc), F1-score of the hate-speech class (F1_HS), and Macro F1-score (M_F1) for each dataset using feature-combination strategies and compared with external approaches. Please, check the original manuscript for the references.

#### Spanish MisoCorpus 2020

| Approach                                                        | Acc     | F1_HS   | M_F1   |
|-----------------------------------------------------------------|--------:|--------:|-------:|
| SVM, LF, AWE (external)                                         | 85.2    | -       | -      |
| **Knowledge integration (LF-BF)**                               | **90.4** | **88.9** | **90.2** |
| Ensemble Learning (LF-BF, logistic regression)                  | 89.7    | 88.2    | 89.6   |

#### AMI 2018

| Approach                                                        | Acc     | F1_HS   | M_F1   |
|-----------------------------------------------------------------|--------:|--------:|-------:|
| SVM, bag-of-words, lexicons (external)                          | 81.5    | -       | -      |
| SVM, LF, AWE (external)                                         | 81.5    | -       | -      |
| **Knowledge integration (LF-BF)**                               | **83.3** | **83.4** | **83.3** |
| Ensemble Learning (LF-BF, logistic regression)                  | 82.5    | 82.8    | 82.5   |

#### HaterNET

| Approach                                                        | Acc     | F1_HS   | M_F1   |
|-----------------------------------------------------------------|--------:|--------:|-------:|
| LSTM & MLP (external)                                           | -       | 61.1    | -      |
| BETO (external)                                                 | -       | 65.8    | 77.2   |
| **Knowledge integration (LF-BF)**                               | **84.3** | 65.9    | 77.9   |
| Ensemble Learning (LF-BF, logistic regression)                  | 82.9    | **68.3** | **78.3** |


#### HatEval 2019 (Spanish)

| Approach                                                        | Acc     | F1_HS   | M_F1   |
|-----------------------------------------------------------------|--------:|--------:|-------:|
| SMO, n-grams, LF, PoS features (external)                       | -       | -       | 73.0   |
| SMO, LF, AWE                                                    | -       | -       | 75.4   |
| BETO [[4]](#ref4)                                               | -       | **77.6** | 75.5   |
| **Knowledge integration (LF-BF)**                               | **77.1** | 76.8    | **76.8** |
| Ensemble Learning (LF-BF, logistic regression)                  | 76.5    | 74.6    | **76.5** |



### Citation
```
@article{garcia2023evaluating,
  title={Evaluating feature combination strategies for hate-speech detection in spanish using linguistic features and transformers},
  author={Garc{\'\i}a-D{\'\i}az, Jos{\'e} Antonio and Jim{\'e}nez-Zafra, Salud Mar{\'\i}a and Garc{\'\i}a-Cumbreras, Miguel Angel and Valencia-Garc{\'\i}a, Rafael},
  journal={Complex \& Intelligent Systems},
  volume={9},
  number={3},
  pages={2893--2914},
  year={2023},
  publisher={Springer}
}
```
