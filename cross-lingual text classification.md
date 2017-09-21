# Cross-lingual text classification
#### Author: Zizhuo Ren
## overview
 - Crosslingual text classification is a variant of text classification, in which we want to automatically classify documents in a language, when the only available training data is in a different language.
 - **Parallel corpora**: large pool of unlabelled data - datasets with senetences and their respective transltion from different sources.
 - **Billingual dictionary**: often ignore the dependency of word meaning
and its context, and cannot leverage domain specific disambiguation when the dictionary on hand is a general-purpose one
## Main Approaches
1. **Bilingual dictionary**: Many fancy ways to build this bilingual dictionary including a).mapping documents in source and target language into the same semantic space b). translate the classification model from source language to target language and so on
2. **Automatic Machine Translation**: Give each document a source-language and a target-language version, where one version is machine-translated
from the another one.
3. **Representation learning or the mapping of the induced representations in cross-language settings**
Finding representations of documents such that similar documents have similar representations. Having such representations, one can train a classifier in the source language, and it should work on the target language, since the representations are independent of language.
- **Cross-lingual representations starting by learning monolingual representations**: start by learning monolingual representations, and then use parallel corpora to transform them into cross-lingual representations.
- **Learn biolingual representations**: based on a parallel corpus.
## *Fasttext for multilingual(or even better embeddings-conceptNet)
The original fasttext vector are monolingual, meaning that while similar words within a language share similar vectors, translation words from different languages do not have similar vectors.
  - SVD can be used to learn a linear transformation (a matrix), which aligns monolingual vectors from two languages in a single vector space

There is another group proposed [ConceptNet Numberbatch](https://github.com/commonsense/conceptnet-numberbatch) which consists of state-of-the-art semantic vectors (also known as word embeddings) that can be used directly as a representation of word meanings or as a starting point for further machine learning.The conceptNet also get rid of bias in the training data.



## *Cross-lingual Distillation for Text Classification (parallel-corpus based approach) 
This method is focusing on the reduction of domain/distribution matches in CLTC. And we also need to know about knowledge distillation, once the cumbersome teacher network was trained, the student network was trained according to soften predictions of the teacher network.
- Firstly, train a source-language classifier with both labeled training documents and adapt it to the unlabeled documents from the source-language side of the parallel corpus.The adaptation enforces our classifier to extract features that are: **1) discriminative for the classification task** and **2) invariant with regard to the distribution shift between trainingand parallel data**.
- Secondly, use the trained source-language classifier to obtain the soft labels for a parallel corpus, and the target-language part of the parallel corpus to train a target classifier, which yields a similar category distribution over target-language documents as that over source-language documents.

The first step addresses the potential domain/distribution mismatch between the labeled data and the unlabeled data in the source language. And the second step addresses the potential mismatch between the target-domain training data (in the parallel corpus) and the test data (not in the parallel corpus).

## Parallel-Corpus based CLTC Methods
All use an unlabeled parallel corpus. These series of methods learn latent document representations in a shared lowdimensional space by performing the Latent Semantic Indexing (LSI), the Oriented Principal Component Analysis (OPCA) and a kernel (namely KCAA) for the parallel text.
- **LSI**:  An LSI analysis of these training documents results in a dualanguage semantic space in which terms from both languages ,are represented.
## MT-based CLTC Methods (MT+LR, MT+DAN)
The methods in this category all use an MT system to translate each test document in the target language to the source language in the testing phase. It will introduce a method called co-training which train different classifier on both source and target languages.The classification can be based on logistic regression or deep averaging network.
## Adversarial Deep Averaging Network (ADAN)
Exploits adversarial training for CLTC. It uses averaged bilingual embeddings of words as its input and adapts the feature extractor to produce similar features in both languages.

## Possible solutions to our data
Based on the literature review I performed. Basically, there are two main approaches we can go. I would suggest we go for parallel corpora.


[tokenizer and segmenter](https://pypi.python.org/pypi/tinysegmenter)

