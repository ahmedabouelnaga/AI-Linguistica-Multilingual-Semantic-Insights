AI-Linguistica-Multilingual-Semantic-Insights

## Abstract
This project explores **Semantic Textual Relatedness (STR)** in low-resource African and Asian languages, contributing to SemEval 2024 Task 1. By fine-tuning the **XLM-RoBERTa** multilingual model on the SemRel2024 dataset, we aim to investigate multilingual language model generalization, language-specific impacts, and cross-lingual transfer. The project highlights the challenges of NLP for underrepresented languages and provides valuable insights into developing inclusive systems.

## Table of Contents
- [Introduction](#introduction)
- [Methods](#methods)
  - [Dataset](#dataset)
  - [Model Architecture](#model-architecture)
  - [Experiments](#experiments)
- [Results and Analysis](#results-and-analysis)
  - [Overall Performance](#overall-performance)
  - [Language-Specific Performance](#language-specific-performance)
  - [Cross-Lingual Transfer](#cross-lingual-transfer)
  - [Challenges in Low-Resource Languages](#challenges-in-low-resource-languages)
- [Limitations and Future Directions](#limitations-and-future-directions)
- [References](#references)

---

## Introduction
Understanding the **semantic relationships** between texts across multiple languages remains a core challenge in NLP, especially for **low-resource languages**. This project addresses that gap by leveraging the SemRel2024 dataset and focuses on analyzing STR across **14 African and Asian languages**.

Our objectives:
1. Evaluate the generalization ability of **multilingual models** for STR tasks.
2. Investigate the impact of language-specific characteristics like morphology and syntax.
3. Assess the potential for **cross-lingual transfer** in fine-tuned models.

---

## Methods

### Dataset
The **SemRel2024 dataset** contains 26,257 examples across 14 languages, where each example has a pair of sentences and a semantic relatedness score between 0 and 1. 
- Training data is available for only some languages, while others are tested for generalization.
- Examples include:
  - **High Relatedness**: "A brown dog is jumping." vs. "A black dog is running through water."
  - **Low Relatedness**: "Actor Ben Gazzara dead at 81." vs. "A man is pouring rice into a pan."
  
For details on dataset subsets and splits, refer to **Table 1** (page 2).

### Model Architecture
We fine-tune the **XLM-RoBERTa base model** with the following modifications:
1. Add a **regression layer** to map embeddings to relatedness scores (0-1).
2. Train using **Mean Squared Error (MSE)** as the loss function.
3. Implement **learning rate scheduling** using AdamW optimizer.

### Experiments
- Batch Size: 16
- Epochs: 8
- Early Stopping: Patience of 3 epochs
- Learning Rate: 2e-5
- Evaluation metrics: **MAE**, **Pearson correlation**, **Spearman correlation**

---

## Results and Analysis

### Overall Performance
The model achieves a moderate performance:
- Mean Absolute Error (MAE): **0.2248**
- Pearson Correlation: **0.3754**
- Spearman Correlation: **0.6208**

### Language-Specific Performance
#### High Performance (MAE < 0.15, Correlation > 0.83):
- **Amharic**: MAE = 0.0873, Pearson = 0.8382
- **Marathi**: MAE = 0.1024, Pearson = 0.8615
- **Telugu**: MAE = 0.1405, Pearson = 0.8531

#### Moderate Performance:
- **English**: MAE = 0.1111, Pearson = 0.8403
- **Hindi (unseen)**: MAE = 0.1113, Pearson = 0.8046

#### Low Performance (MAE > 0.2, Correlation < 0.4):
- **Punjabi**: MAE = 0.2273, Pearson = 0.0143
- **Indonesian**: MAE = 0.2732, Pearson = 0.3983

### Cross-Lingual Transfer
The model demonstrates **effective transfer** for languages like Afrikaans and Hindi, validating its generalization ability.

### Challenges in Low-Resource Languages
Languages like Punjabi and Indonesian present difficulties due to:
- Complex morphology (e.g., noun/adjective agreement, verb conjugations).
- Lack of sufficient training data.

---

## Limitations and Future Directions
1. **Data Scarcity**: Insufficient data for some languages limited performance. Future work could explore **data augmentation** and **zero-shot learning**.
2. **Architecture**: Testing **ensemble models** or alternate architectures may improve results.
3. **Error Analysis**: A deeper investigation into **linguistic features** could yield better tailored solutions.
4. **Transfer Mechanisms**: Optimizing **cross-lingual transfer** is a promising area for future exploration.

---

## References

1. Alexis Conneau, Kartikay Khandelwal, Naman Goyal, Vishrav Chaudhary, Guillaume Wenzek, Francisco Guzmán, Edouard Grave, Myle Ott, Luke Zettlemoyer, and Veselin Stoyanov. 2019a. *Unsupervised cross-lingual representation learning at scale*. CoRR, [arXiv:1911.02116](https://arxiv.org/abs/1911.02116).

2. Alexis Conneau, Kartikay Khandelwal, Naman Goyal, Vishrav Chaudhary, Guillaume Wenzek, Francisco Guzmán, Edouard Grave, Myle Ott, Luke Zettlemoyer, and Veselin Stoyanov. 2019b. *Xlm-roberta: Unsupervised cross-lingual representation learning at scale.* [HuggingFace Model](https://huggingface.co/FacebookAI/xlm-roberta-base).

3. Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova. 2019. *Bert: Pre-training of deep bidirectional transformers for language understanding.* In *Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies*, pages 4171–4186.

4. Sharvi Endait, Srushti Sonavane, Ridhima Sinare, Pritika Rohera, Advait Naik, and Dipali Kadam. 2024. *Multilingual evaluation of semantic textual relatedness.* Preprint, [arXiv:2404.09047](https://arxiv.org/abs/2404.09047).

5. Nedjma Ousidhoum, Shamshuddeen Hassan Muhammad, Mohamed Abdalla, Idris Abdulmuminu, Ibrahim Said Ahmad, Sohaib Ahuja, Alham Fikri Aji, Vladimir Araujo, Abinew Ali Ayele, Pawan Baswani, Meryem Beloucif, Chris Biemann, Sofia Bohurin, Christine De Kock, Genet Shanko Dekebo, Oumaima Hourrane, Gopichand Kanumolu, Lokesh Madasu, Samuel Rutunda, Manish Shrivastava, Thamar Solorio, Nirmal Surange, Hailegnaw Getaneh Tilaye, Krishnapriya Vishnubhotla, Genta Winata, Seid Muhe Yimam, and Saif M. Mohammad. 2024a. *Semrle2024: A collection of semantic textual relatedness datasets for 14 languages.* Preprint, [arXiv:2402.08638](https://arxiv.org/abs/2402.08638).

6. Nedjma Ousidhoum et al. 2024b. *SemEval-2024 task 1: Semantic textual relatedness for African and Asian languages.* In *Proceedings of the 18th International Workshop on Semantic Evaluation*. Association for Computational Linguistics.

7. Sebastian Ruder, Ivan Vulić, and Anders Søgaard. 2021. *A survey of cross-lingual word embedding models.* *Journal of Artificial Intelligence Research*, 71:757–815.
