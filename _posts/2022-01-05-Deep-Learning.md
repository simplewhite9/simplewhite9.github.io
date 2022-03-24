---
title:  "딥러닝이란?"
categories: [Deep Learning]
tags : [ML, ANN]
thumbnail-url: /assets/img/thumbnail/Deep-Learning-logo.png
description: 딥러닝 Introduction

---


# 딥러닝 Deep Learning Introduction

학교에서 딥러닝 전공을 듣고 나서 어려우면서 헷갈리는 부분도 있고 복습을 하고 싶어서 블로그에 정리하려고 한다!

---

<br>

### **`딥러닝(Deep Learning)`**이란,
**여러 층의 인공신경망 (Artificial Neural Network, ANN)을 활용한 머신러닝 학습**이다

<img src="/assets/img/Deep-Learning/Post1/1.png" alt="Figure 1" width="520"/>

개념 구성을 보면, 인공지능의 구현 방법 중 하나가 머신러닝이고, 머신러닝은 딥러닝을 포괄하고 있다. <br>
즉, 딥러닝은 머신러닝과 같은 개념이 아닌 머신러닝의 구현 방법 중 하나이다.


이제 딥러닝에 대해서 더 자세히 알아보기 위해서 간단하게 머신러닝과 인공신경망의 개념도 살펴보자!

---

<br>

<div class="post-subtitle">Machine Learning(기계 학습)</div>

**데이터를 활용해 결정 또는 예측을 할 수 있도록 모델을 학습 시키는 것**이다.

머신러닝의 학습 종류에는 두가지가 존재하는데, supervised learning (지도 학습)과 unsupervised learning(비지도 학습)이 존재한다.

<br>

`supervised learning`은 이미 정답값이 있는 (labeled) 데이터셋을 통해 학습하는 것으로<br>
classification (분류)와 regression(회귀)로 나뉘고,

<br>
`unsupervised learning`은 정답값이 주어지지 않은 데이터 셋을 통해 학습하는 것으로 <br>
clustering(군집)이 있다.
---

<br>

<div class="post-subtitle">Artificial Neural (인공 신경 세포)</div>
<img src="/assets/img/Deep-Learning/Post1/2.png" alt="Figure 1" width="450"/>


인공 신경은 말 그대로 인간의 **신경 세포(neuron)**와 같은 구조와 방식을 띈다. <br>
실제 인간의 신경 세포를 보면, 수상 돌기를 통해 전기신호를 받아서 각 신호에 가중치를 더하고, 세포체에 저장을 하고 있다가 입력된 신호의 용량이 일정량을 넘어서면 축색돌기(Axon)을 통해 다른 뉴런으로 신호를 전달한다. 

<br>
마찬가지로 (사진을 참고)<br>
인공 신경에서는 input 값들과 weights 부분이 수상돌기를 통해 전달되는 전기신호와 대응되고, output으로 출력될 수 있게 해주는 일정량을 결정하는 부분이 **activation function**의 역할이다. 

<br>
이런 구조를 머신러닝에서는 `perceptron`이라고 부르기도 한다.


<br>

<div class="post-subtitle">Artificial Neural Network (인공 신경망)</div>
인공 신경망은 앞서 본 perceptron을 여러 층으로 쌓아 수많은 뉴런들을 연결해주는 구조이다.

<img src="/assets/img/Deep-Learning/Post1/3.png" alt="Figure 1" width="450"/>


가장 흔히 볼 수 있는 구조는 위에 보이는 two layer neural network으로,<br>
input layer 입력층, output layer 출력층 그리고 그 사이에 하나의 hidden layer(은닉층)으로 이루어진 신경망이다.

<br>
끝✌🏻

---

**참조**:

고려대학교 COSE474 딥러닝<br>
Stanford University CS230 Deep Learning