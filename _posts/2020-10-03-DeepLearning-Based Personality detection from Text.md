---
layout: post
categories: text-mining
title:  "Deep Learning-Based Document Modeling for Personality Detection from Text"
date:   2020-10-03
author: HaeYong JOUNG
tags: text-mining
comments: true
---

Deep Learning-Based Personality Detection from Text
===============

​

​	이번 포스팅은 CNN을 활용하여 Text 저자의 Personality를 판별하는 감성 분석 논문에 대해 리뷰해보겠습니다.

*Deep Learning-Based Document Modeling for Personality Detection from Text (N. Majumder, S. Poria and A. Gelbukh and E. Cambria)* 의 논문을 기초로 리뷰하였으며 해당 논문은 2017년에 IEEE Computer Society에 발표된 논문입니다. 본 포스팅에서 논문에서 소개하는 프로세스와 CNN 아키텍처에 대해 살펴보고 다음 포스팅에서는 이 논문을 활용하여 실제 실습 프로젝트를 진행해보겠습니다.



***

### Objective
 본 논문의 목표는 주어진 Text에서 저자의 Personality를 detection하는 것입니다. 일종의 감성 분석이라고 볼 수 있는데요. 논문의 저자는 찾아내고자 하는 특성으로 5가지 Personality traits를 제안합니다. 따라서 **5-level classification** 문제라고 정의할 수 있습니다.
​
![PNG](https://hyj0103.github.io/assets/traits.png)



### Process
Classification을 진행하는 절차는 다음과 같습니다. 하나하나 차근차근 살펴보겠습니다.

> **1. Data Input**
> **2. Preprocessing & Filtering**
> **3. Modeling**
> **4. Output**


#### 1. Data Input
분석을 진행하기 위해 Text data를 확보합니다. 여기서 중요한 것은 각 Text data마다 5 class에 대한 **label**이 붙어있어야 한다는 것입니다. 이는 뒤에서 소개할 모델링이 Supervised learning으로 구성되어 있기 때문인데, 본 논문의 아쉬운 점 중 하나라고 생각합니다. (새로운 text data를 구할 때마다 5가지 특성에 대한 class를 새로 달아주어야 하기 때문이죠.) 저자는 *James Pennebaker and Laura King’s stream-of-consciousness essay dataset*을 사용하였고 2,467개의 essay data가 포함되어 있습니다.


#### 2. Preprocessing & Filtering
Data를 받고나면 전처리 과정을 거쳐서 model에 넣어주어야 합니다. 본 방법론은 단어 수준의 vector에서부터 패턴을 파악하여 전체 글의 특성을 파악하는 bottom-up 분석 방법이기 때문에 text data를 word level로 분해해주어야 합니다. 주로 ., ?, ! 등의 문장부호를 기준으로 하거나 띄어쓰기를 기준으로 분해해줍니다.

이후에는 Filtering단계를 거칩니다. 저자는 생성된 단어 벡터들 중 emotion이 포함되지 않은 단어는 분석에서 제외합니다. Emotion이 포함된 단어 벡터를 저자는 "Emotionally Charged Vector"라고 합니다. 이러한 ECV를 찾기 위해서 *NRC Emotion Lexicon*을 참고합니다. Lexicon에는 10개의 emotion으로 tagging된 6,468개의 단어가 포함되어 있습니다. 저자는 단어 벡터들 중 이 lexicon에 포함되지 않은 단어들은 분석 대상에서 제거합니다. 이러한 Filtering 작업은 모델의 성능을 높혀준다고 밝혀져 있습니다.


#### 3. Modeling
![PNG](https://hyj0103.github.io/assets/model architecture.png)

이제 본격적으로 CNN Model의 Architecture에 대해 살펴보겠습니다.  
Model에서 중요한 layer는 다음과 같습니다.

* **Input layer**
* **Convolution layer**
* **Max-pooling layer**
* **Concatenation layer**
* **1-max pooling layer**
* **Fully connected layer**
* **Output layer**

이 중에서 Input, Convolution, Max-pooling layer는 Word-level에서 분석이 진행되고 Concatenation layer는 Sentence-level에서 진행됩니다. 마지막 1-max pooling, Fully connected, Output layer는 Document-level에서 최종적으로 classification을 수행합니다. 이제 각각에 대해 알아보도록 하겠습니다.

* **Input layer**
Input layer에 투입되는 text data는 4-dimensional array로 구성됩니다. 
\
$$ \R^{D\times S\times W\times E}\\
\textit{where}\ D = \textit{Number of documents}\\
S = \textit{Maximum number of sentences}\\
W = \textit{Maximum number of words}\\
E = \textit{Length of word embeddings} $$











​
