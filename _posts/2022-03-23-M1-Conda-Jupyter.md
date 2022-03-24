---
title:  "M1 Conda 및 Jupyter Notebook 설치"
categories: [개인 SPACE]
tags : [M1, Jupyter, Conda]
thumbnail-url: /assets/img/thumbnail/Conda-Jupyter.png
description: M1 (Apple Silicon) Conda 및 Jupyter Notebook 설치 방법

---

# M1 (Apple Silicon) Conda 및 Jupyter Notebook 설치
<br>

---

M1에 Anaconda를 설치하는 것이 조금 복잡해졌다고 한다 완벽하게 M1과 호환이 되지는 않지만 사용은 할 수 있다!

원래 설치하려는 마음이 없었는데 Google Colab ipnyb 파일을 PDF로 다운 받고 싶은데 자꾸 output 그래픽은 다 날려먹는다^^

방법은 오르지 Jupyter를 사용하는 것.. 근데 Jupyter를 사용하려다보니 Anaconda도 같이 다운 받고 싶은데 현재 M1이 지원되는건 minimal conda **miniforge**밖에 없다고 한다 (이건 그나마 희소식이다! M1은 지원 안되는 프로그램이 너무 많다..후)

---
<br>

<div class="post-subtitle">Python 설치 확인</div>

`$ python --version`<br>
M1은 python2.7.18은 이미 설치되어서 나온다고 한다 (다만 옛날 버전이다)
<br>

`$ python3 --version`<br>
Homebrew를 설치한 컴퓨터에는 python3도 같이 설치된다 (만약에 Homebrew가 없다면 설치하는 것을 추천한다)
<br>
Homebrew 설치 여부 확인 : `$ which brew`<br>
<br>

파이썬이 설치된 위치는<br>
`$ where python` 또는 `$ where python3` 로 파이썬 확인 가능<br>
보통은 /usr/bin/python..에 자리잡고 있다 <br>
<br>
<span class="highlight-red bold">주의⚠️</span> 컴퓨터 자체가 python에 의존하고 있기 때문에 지우면 망가질 가능성 99%다

---
<br>
<div class="post-subtitle">Miniforge 설치</div>

🏁 Miniforge GitHub 링크: [Miniforge Github](https://github.com/conda-forge/miniforge)다


<img src="/assets/img/SPACE/M1-Conda/f0.png" alt="Figure 1" width="560"/>

여러가지가 있는데 이 중에서 **OS X arm64(Apple Silicon)**이라고 적혀있는 프로그램을 다운로드

<br>
Terminal로 돌아와서<br>
`$ sh /Users/.../Downloads/Miniforge3-MacOSX-arm64.sh` 를 실행시키면 된다<br>
<span class="highlight-red bold">참고</span>: sh 치고 나서 다운로드 된 파일을 drag해서 터미널로 가져오면 파일 이름이 자동으로 입력된다
<br><br>
<img src="/assets/img/SPACE/M1-Conda/f1.png" style="border: 1px solid #D3D3D3; padding: 5px" alt="Figure 1" width="600"/>
<br>

이제 설치를 위해서는 조금 절차를 거쳐야하는데 차근차근 읽으면서 **ENTER**치고 [YES\|NO] 물어보면 **YES**를 입력해서 다운로드 하면 된다! **끝**
<br>
<br>
설치하고 나면 해당 <span class="highlight-red bold">Shell창을 닫고</span> 다시 새로운 Shell 창을 열어줘야한다<br>
나는 자동으로 conda가 실행되는 것이 싫기 때문에 <br>
`$ conda config --set auto_activate_base false` 도 해서 auto activate을 <span class="highlight-red bold">False</span>로 설정했다

<span class="highlight-red bold">참고</span>: 기본적으로 깔려있는 환경 이름은 **base**고**,** Conda 환경이 실행되고 있는지 확인하려면 shell 입력 맨 앞에 (base)라고 되어 있는지 보면 된다
<br><br>

---
<br>
<div class="highlight-red bold">NOTE</div>

`$ conda activate base` **: ‘base’ 환경 활성화**

`$ conda deactivate`  : **Conda 비활성화**

`$ conda create -n env python=3.8` **: python 3.8 버전을 사용하는 ‘env’라는 환경 새로 구축**

---
<br>
<div class="post-subtitle">JUPYTER 설치</div>

Conda 환경이 **활성화** 되어 있는 상태에서 

`$ pip install jupyter notebook`

설치가 완료되었다면 실행시키는 방법

`$ jupyter notebook`

---
<br>

잘 실행되는 것 보니 기분 좋아서 <span class="highlight-red bold" >인증샷 :)</span>

<img src="/assets/img/SPACE/M1-Conda/f2.png" alt="Figure 1" width="800"/>
