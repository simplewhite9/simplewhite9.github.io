---
title:  "Machine Learning의 기초"
date:   2022-01-05 00:12:24 +0900
categories: [Deep Learning]
tags : [Supervised Learning, Overfitting, Underfitting, MSE, Regularization]
thumbnail-url: /assets/img/thumbnail/Deep-Learning-logo.png
description: this is a simple description of the post. this is a simple description of the post. this is a simple description of the post. 

---

딥러닝의 이해를 더 돕기 위해 머신 러닝의 기초를 짚고 넘어가려고 한다.

<div class="post-subtitle">Basic Mathematical Notation</div>

{% include callout-head.html %}⚠️{% include callout-body.html %}
<span class="bold">NOTE</span><br><br>

$x∈\mathbb{R}$ :  $x$는 <element class="bold highlight-red">scalar</element> <br>
$x\in\mathbb{R}^n$ : $x$ 는 <span class="bold highlight-red">column</span> vector <br>
$x = (x_1, ...., x_n)$도  <span class="bold highlight-red">column</span> vector <br>

<span class="bold highlight-red">p-norm</span>: $||x||_p = (\sum_{i}^{}|x_i|^p)^\frac{1}{p})$ , $p \geq 1$
{% include callout-bottom.html %}
<br>


<div class="post-subtitle">Supervised Learning</div>

이전에 글에서 언급 했듯이 supervised learning은 정답값이 있는 (labeled) 데이터셋을 통해 학습하는 것으로 classification (분류)와 regression(회귀)로 나뉜다.

<img src="/assets/img/post1/post1-01.png" alt="Figure 1" width="300"/>
<div class="image-caption">Figure 1: Supervised classification example</div>



위 Figure 1은  **`classification`**의 예시를 보여주고 있다. 유방암 환자들의 데이터를 가지고 양성 또는 악성 종양의 환자로 구분을 하고 있다. 여기에서는 tumor size와 나이를 가지고 양성이다 또는 악성 종양이다를 예측할 수 있다. 이와 같이 예측 값이 연속적이지 않고 정확히 0 또는 1 아니면 yes or no 등으로 나올 때는 **classification**이라고 부른다.

**`regression`**은 반대로 연속적인 실수를 예측하는 것이다. 예를 들어, 

<img src="/assets/img/post1/post1-02.png" alt="Figure 2" width=650/>
<div class="image-caption">Figure 2: Supervised regression example</div>


각 홍보 매체 TV, Radio, Newspaper에 대한 홍보비용 값이 주어졌을때 각 두 데이터를 가지고 추 세선을 그어서 예측하는데 활용하는 것이다.

Supervised learning의 process를 한눈에 보면,

<img src="/assets/img/post1/post1-03.png" alt="Figure 3" width="300"/>
<div class="image-caption">Figure 3: Supervised learning process</div>

training data로 input $X$ 와 output $Y$가 주어졌을때 예측 함수 $h(X)$ 를 통해 $y$ 값을 추측하는 것이다.

{% include callout-head.html %}⚠️{% include callout-body.html %}
<span class="bold">NOTE</span><br><br>

$X$: input, <element class="bold">feature</element>, independent variable<br>
$Y$: <element class="bold">output</element>, response, dependent variable
{% include callout-bottom.html %}

<br>
기본적으로 $h(X)$ 함수를 보면,
{% include callout-head.html %}📌{% include callout-body.html %}
<span class="bold">$Y = h(X) + \epsilon$</span><br><br>

$X$: feature vector $X = (X_1, X_2, ..., X_p)$ <br>
$h$ : unknown function <br>
$\epsilon$ : random error

{% include callout-bottom.html %}

이렇게 머신러닝의 주요 목표는 unknown function $h$를 주어진 데이터로부터 예측하는 것이다.

<br>

---
<div class="post-subtitle">Function estimation</div>

1. **Population** (모집단) : 전체 집합
2. **Sample** (표본): 모집단에서의 부분집합

함수를 학습하기 위해 사용 되는 data는 population의 부분집합인 sample을 이용한다. 여기서 sample은 population의 **특성을 99% 가지고 있다**고 추정을 하고 진행하고 1%의 오차는 허용이 된다.  

이 둘의 관계를 그림으로보면, 아래와 같다.

<img src="/assets/img/post1/post1-04.png" alt="Figure 4" width="500"/>
<div class="image-caption">Figure 4: Population and Sample relationship</div>

<br>
이와 같이 주어진 데이터를 가지고,

<span class="background-yellow">$Y \approx \hat{h}(x)$</span>를 만족하는 $h(x)$와 같이 작동한다고 예측하는 $\hat{h}(x)$의 함수를 찾는 것이다.

supervised learning에서 사용되는 정답에 가까운 함수를 찾기 위해서는 해당 함수가 어떻게 표현될 것 인가의 가설을 먼저 세워야한다. 기본적으로는 linear model을 택한다.

<br>
<div class="post-subtitle">Linear model:</div>

{% include callout-head.html %}📌{% include callout-body.html %}
<span class="bold">$\hat{h}(X) = \theta_0 + \theta_1x_1 + \theta_2{x_2} + ... + \theta_p{x_p}$</span><br><br>

$X = (x_1, x_2, x_3, ..., x_p)$ <element class="bold">feature</element> <br>
$\theta =$   <element class="bold">parameters</element> ( also known as <element class="bold">weights</element>) <br>
<span class="highlight-red">*NOTE $\theta_0$는 <element class="bold">bias</element>라 부른다 <br></span>

{% include callout-bottom.html %}


{% include callout-head.html %}➕{% include callout-body.html %}
<span class="bold highlight-red">* $x_0 = 1$이라 가정할때,</span><br><br>

$\hat{h}(X) = \sum_{i = 0}^{p} \theta_ix_i = \theta^Tx$  이라고도 표현이 가능하다
{% include callout-bottom.html %}


{% include callout-head.html %}➕{% include callout-body.html %}
<span class="bold highlight-red">참고 사항</span><br><br>

$\hat{h}(X) = \theta_0 + \theta_1x_1 + \theta_2{x_2} + ... + \theta_p{x_p}$ 일때, <br>

$X = (x_0, x_1, x_2, x_3, ..., x_p)$ <br>
$\theta =$   $( \theta_1, \theta_2, \theta_3, ..., \theta_p)$와 같이 $\theta_0$이 포함되어 있지 않을때, <br>
<br>
<span class="bold">$\hat{h}(X) = \tilde{\theta}^TX$</span> 로 표현이 가능하다 이때 $\tilde{\theta}$는 $( 1, \theta) = (1, \theta_1, \theta_2, ...)$ 와 같은 의미다
{% include callout-bottom.html %}
<br>

이 외에 quadratic model 도 있다
<div class="post-subtitle">Quadratic model:</div>

{% include callout-head.html %}📌{% include callout-body.html %}
 $\hat{h}(X) = \theta_0 + \theta_1x_1 + \theta_2{x_2}^2 + ... + \theta_p{x_p}^p$

{% include callout-bottom.html %}

<span class="highlight-red">*Note:parameter 개수가 늘어나면서 **flexibility 성능은 증가되나 generalization (일반화) 성능은 감소된다**</span>

머신러닝에서 자주 사용되는 **“`data fitting`”**의 의미는 위 식에서 Y(정답)에 가장 근접한 값을 얻기 위해 함수에 활용되는  $p + 1$개의 
**<span class="background-yellow">parameters $\theta_i$ 들의 best approximation 값</span>**을 찾는 작업이다.

그렇다면, 함수 $h$를 **<span class="underline">잘 예측하는게 중요한 이유</span>**!

1. 새로운 포인트 $X = x$가 주어졌을 때, $Y$값을 예측할 수 있다 
2. 주어진 feature 중에서 어떤 feature 값이 중요한지 찾을 수 있다. 다시 말하면, $X = ( X_1, X_2, ..., X_p)$라고 할때 이 X 값들 중 어떤 요소가 Y를 설명하는데 중요한 역할을 하는지 알 수 있다.
3. $h(X)$함수의 복잡도에 따라 (차수와 연관되어 있다) 각 X의 요소 $X_j$ 들이 Y에 어떤 영향을 주는지 알 수 있다

<br>

---

아래와 같이 데이터가 주어졌을 때 3가지의 fitting을 시도해보았다고 하자,
<br>
<img src="/assets/img/post1/post1-05.png" alt="Figure 5" width="580"/>
<div class="image-caption">Figure 5: Results of fitting linear regression, quadratic regression and polynomial of 5-th order</div>


맨 왼쪽은 linear fitting ($y = \theta_0+\theta_1x$), <br>
두번째는 quadratic fitting ($y = \theta_0+\theta_1x + \theta_2x^2$), <br>
그리고 마지막은 5-th order polynomial $y = \sum_{j = 0}^{5} \theta_jx^j$  으로 fit해본 결과이다. 

사실 오른쪽으로 가면서 점점 더 데이터를 잘 표현한다고 생각할 수 있다.  그러나 꼭 그렇지만은 않다. 이렇게 새로운 feature $x^p$를 도입시킬때에는 주의해야하는 사항들이 있다. 

<br>
<div class="post-subtitle"><span class="background-yellow">Overfitting</span></div>

맨 오른쪽 그림은 overfitting의 예시이다.

**Training data 한에서는 정확히 예측할 수 있지만, 새로운 데이터에는 정확도가 떨어진다**.

위에서 언급했듯이, flexiblity가 증가하면서 generalization이 감소하여 과적합의 가능성이 있는 것이다

보통은 validation loss와 training loss의 수치를 비교하면서 overfitting이 일어났는지의 여부를 알 수 있다. 모델 Training 과정에서 어느순간 training loss가 validation loss 보다 훨씬 작아질때 overfitting이 일어나고 있음을 의심할 수 있다. 

<br>
<div class="post-subtitle"><span class="background-yellow">Underfitting:</span></div> 

맨 왼쪽 그림은 underfitting의 예시이다.

Overfitting과 반대되는 개념으로, **Training data도 학습을 제대로 하지 못해 낮은 성능을 보이는 상태**를 말한다.

<br>
결국엔, prediction accuracy 와 interpretability의 싸움이다 <br>
모델이 단순할수록 데이터 해석은 쉬워지지만, 그만큼 예측 정확도는 떨어진다.<br>
<br>

---

<div class="post-subtitle">모델의 정확도 측정</div>

흔히 알려져 있는 방법으로는 MSE (Mean Square Error)가 있다

<br>

**`Mean Square Error`:**

{% include callout-head.html %}📌{% include callout-body.html %}
$MSE = {1 \over N} \sum{(y- \hat{f}(x))^2}$ <br><br>

<span class="highlight-red">
<span class="bold">*오차 = (실제 값 - 예측 값 )</span> <br>
오차는 양수, 음수 다양하게 나올 수 있기 때문에 해당 값을 제곱한다  <br>
* 제곱하기 때문에 <span class="bold">(예측 값 - 실제 값)</span>으로도 표현이 가능하다
</span>
{% include callout-bottom.html %}

현재 cost function으로 MSE를 사용한다고 하면 training 단계에서 optimize하고자하는 **objective function**이 바로 MSE가 된다.
<br>
즉, 모델을 training 하면서 MSE = 0이 되도록 하는 것이다.
- $MSE_{train} = {1 \over N} \sum_{i \in D_{train}}{(y_i- \hat{f}(x_i))^2}$

<br>

다만, training 단계에서 단순히 $MSE_{train}$ 만 **<span class="highlight-red">minimize</span>** 하려고 하다보면 overfitting이 일어날 수도 있다.<br>
그래서, 해당 모델을 **independent(독립된)** **test** dataset을 활용해서 validate을 한다<br>
- $MSE_{test} = {1 \over N} \sum_{i \in D_{test}}{(y_i- \hat{f}(x_i))^2}$

<br>
**Example)**
<img src="/assets/img/post1/post1-06.png" alt="Figure 6" width="580"/>
<div class="image-caption">Figure 6.1: Comparison of curves with different flexibility</div>

왼쪽에서 검은색 선이 정답이고, 오른쪽 빨간색 선은 $MSE_{test}$ 이고 회색 선은 $MSE_{train}$을 나타낸다. Flexibility는 parameter의 개수와 같은 의미일 때 노랑색 선은 flexibility가 낮음으로 오차의 범위가 크다. 반대로 초록색 선은 flexibility가 높아서 오차의 범위는 노란색보다 작지만 trainig data에서 나온 MSE값이 test data에서 나온 값보다 현저히 작은 것을 볼 수 있다. 이것은 overfitting(과적합)이 된 모습이다. 그러면 이중에서 가장 적합하게 fitting된 모델은 파란색 선이라고 할 수 있다. 

<br>
<img src="/assets/img/post1/post1-07.png" alt="Figure 6" width="580"/>
<div class="image-caption">Figure 6.2: Comparison of curves with different flexibility ( but with less noise)</div>

이번에는 위에 그림을 보면, 데이터 자체가 앞전 Figure 6.1에 비해서 noise가 훨씬 적다. 검은색 truth curve를 크게 벗어나는 데이터가 없다는 뜻이다.<br>
이런 경우, 모델 자체는 복잡한데 noise가 적기 때문에 flexibility 가 훨씬 높을 때 더 높은 성능을 보인다.<br>
즉, 파란색 또는 초록색 선이 적합하다 볼 수 있다.<br>


<br><br>
위에서 본 **notation을 조금 바꿔서** MSE($L(X)$ **`loss function`**)을 나태내면,

{% include callout-head.html %}📌{% include callout-body.html %}
$L(X) = {1 \over N} \sum_{i = 1}^{N}{(\hat{f}(a_i;  x) - b_i)^2}$
<br><br>
$a = (a_1, a_2, a_3,..., a_m)$ <element class="bold">feature</element> <br>
$\hat{f}(a_i; x)$ = parameter $x$를 가지고 $a_i$를 표현한다는 뜻  $= ( \tilde{a_i}^Tx)$ <br>
$b =$  <element class="bold">output</element> 실제 값 
{% include callout-bottom.html %}


{% include callout-head.html %}➕{% include callout-body.html %}
 혹은 $L(X) = {1 \over N} ||Ax - b||_2^2$ <br><br>

$A = [ \tilde{a_1}^T; \tilde{a_2}^T; \tilde{a_3}^T; , ...; \tilde{a_m}^T]$
{% include callout-bottom.html %}

 모델의 성능을 높이기 위해서 **loss를 minimize**한다는 것은 <span class="highlight-red">$L(X)$**에서의 오차 거리를 최소화**</span>하고자하는 것과 같다.

<br>

---

<div class="post-subtitle">Overfitting 방지 방법</div>

1. **`Regularization`** (정규화)
2. Cross Validation (교차 검증)
3. 더 많은 데이터 입력하기

<br>
**`Regularization`**:

해당 포스트에서는 regularization에 대해서만 다룰 것이다. Regularization은 overfitting을 방지하는 방법으로 주어진 training data와 noise를 외우는(memorizing) 현상을 방지하는 것이다.

주 목적은 complexity를 줄이면서, generalization ability는 높이는 것이고, 해당 방법으로는 **parameter(weight)**의 크기를 작게하는 것이 있다. 

<br>
즉, 위에서 언급했듯이 <span class="highlight-gray">(L2 regularization의 예시이다)</span> <br>
(1) minimize $\|\|Ax - b\|\|_2^2$ 하면서 동시에 <br>
(2) minimize $\|\|x\|\|_2^2$ 를 하는 것이다 (magnitude of coefficients)

<span class="highlight-red">* NOTE: (1), (2)는 둘다 **convex** **함수**임으로 min 또는 max를 구하는 것이 가능하다</span>
<br><br>

이와같이 두개를 동시에 optimize하는 것을 ***multi-objective optimization*** 이라고 한다. 결국엔,

{% include callout-head.html %}📌{% include callout-body.html %}
 minimize $||Ax - b||_2^2$ + $\lambda ||x||_2^2$
<br><br>
$\lambda$ 는 hyperparameter로 모델을 최소화하거나 조율할때 쓰는 변수이다
{% include callout-bottom.html %}

<br>
<img src="/assets/img/post1/post1-08.png" alt="Figure 7" width="580"/>
<div class="image-caption">Figure 7: Ridge regression; Regression depending on the variation of  lambda</div>
위와 같이 $\lambda$의 값에 따라 regression이 바뀌는 것을 볼 수 있다.

<br>
L1 regularization의 예시를 보면,<br>
minimize $\|\|Ax - b\|\|_2^2$ + $\lambda \|\|x\|\|_1$으로, $x$가 0 이 많은 벡터 **`sparse vector`**를 만들고자 할때 사용한다.

예를 들면 $x = (0, 0,..., 0, 1, 0.5)$.<br>
이와 같은걸 **`Lasso regression`**라고 부르기도 한다<br>


<br><br>

---

**참고**:<br>
고려대학교 COSE474 딥러닝 <br>
Stanford University CS230 Deep Learning <br>
Stanford University CS229 Machine Learning <br>