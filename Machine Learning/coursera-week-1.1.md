# Linear regression with one variable. (선형회귀)

(Or Univariate linear regression)

## 학습내용

예를 들어, 아파트의 평수에 따른 가격을 예측하는 문제가 주어졌을때,
평수 x 에 대하여 가격 y 를 예측하는 것이 목표이다.

선형회귀로 풀어보면, 훈련집합의 각각의 값집합(x,y)에 가장 근접하는 직선을 구하는 것이라 할 수 있다.

이를 위해 첫번 째로, 가설(hypothesis)이란 것을 만들게 되는데, 아래 항목으로 구성된다.

* m = 훈련집합의 개수
* x = 아파트 평수(input/feature variable)
* y = 아파트 크기(output/target variable)
* ($x^1$, $y^1$) = 1 번째 훈련집합
* ($x^i$, $y^i$) = i 번째 훈련집합
* h = 가설(hypothesis)

가설은 쉽게 말해, 아파트 평수를 입력하면, 집값이 나오는 함수(function)이다. 기본적인 가설($h_x$)은 아래와 같다.

$$h_x = \theta_0 + \theta_1x$$

* $\theta_0$ 과 $\theta_1$ : 파라미터
* $x$: 아파트 평수
* $h_x$: 아파트 가격 = y

즉, 아파트 가격과 가설($h_x$)의 결과가 최대한 집값($y$)에 근접하도록 **가장 작은** $\theta_0$ 과 $\theta_1$ 값을 구하는 것이 목표인 것이다.

예를 들어, 아래와 같은 단순한 훈련집합이 있을 때:

|  x  |  y  |
| :-: | :-: |
|  1  |  1  |
|  2  |  2  |
|  3  |  3  |

계산을 단순화하기 위하여, $\theta_0 = 0$ 이라고 가정하자.

$$h_x = \theta_1x$$

위와 같이 단순화시킬 수 있다.

**가장 작은** $\theta_0$ 과 $\theta_1$ 값을 구하기 위해 서는 비용함수(Cost function, 오차요인 제곱함수라고도 불림)란 것을 사용해야 한다.

$$J(\theta_0,\theta_1) = \frac{1}{2m}\displaystyle\sum_{i=1}^m(h(x^i) - y^i)^2$$

**가장 작은** $\theta_0$ 과 $\theta_1$ 값을 구하는 것은 &rarr; **0에 가까운** $J(\theta_0,\theta_1)$ 값을 구하는 것이라 할 수 있겠다.

$\theta_0 = 0$ 이고, $\theta_1 = 1$ 일때,

J는 $0^2,0^2,..$ 계속 0이 되므로,

정답은
,
$\theta_0 = 0$,
$\theta_1 = 1$

이 된다. 이 과정을 그래프로 표현하면, 아래와 같다.
![그래프](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/fph0S5tTEeajtg5TyD0vYA_9b28bdfeb34b2d4914d0b64903735cf1_Screenshot-2016-10-26-01.09.05.png?expiry=1519344000000&hmac=DVK1BLGMQhG1k5X6eLJj0L2ZAbhlGlAi6aMxJvG7wlA)

아파트 예제로 넘어오면, $\theta_0$은 더이상 0이 아니다. 또한 위 예제와 같이 단순하지 않다.

$\theta_0$이 변하게 되면, 비용함수는 등고선 그래프가 된다.

![등고선그래프](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/hsGgT536Eeai9RKvXdDYag_2a61803b5f4f86d4290b6e878befc44f_Screenshot-2016-10-29-09.59.41.png?expiry=1519344000000&hmac=mSq9_hKbr0Pk8KoVVDmFlMboFNd_pzdpAzwX_whp7K0)

점점 복잡해진다... ㅠㅠ
어쨋든, 두번째 이미지가 등고선 그래프인데, 파란색 선이 교차하는 지점이 **가장 작은** $\theta_0$ 과 $\theta_1$ 값을 알려주는 지점이라 할 수 있다. 각각 **0.12**와 **250**정도가 되겠다.

여기서 기울기 하강 알고리즘(Gradient Descent, 높은 지점에서 가장 낮은 지점으로 하강하는 형태에서 유래)을 적용하면, 비용함수 그래프에서 **가장 작은** $\theta_0$ 과 $\theta_1$ 점을 자동으로 찾아줄 수 있다.

$$\theta_j := \theta_j - \alpha\frac{d}{d\theta_j}J(\theta_0,\theta_1)$$

여기서 j는 0과 1이 되는데, 계산하는 방식은 아래와 같다.
![그래프](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/yr-D1aDMEeai9RKvXdDYag_627e5ab52d5ff941c0fcc741c2b162a0_Screenshot-2016-11-02-00.19.56.png?expiry=1519344000000&hmac=lAE7uv9jqNXi2qjp4td2x-HzNOMxUAKtysaAQ9bl6Ng) 위와 같이 계산이 이루어진다. 저 과정을 계속 반복하게 되면 마지막에 최소값을 얻게된다.

$$\alpha\frac{d}{d\theta_j}J(\theta_0,\theta_1)$$

위 부분을 미분계수(Derivative)라 하는데, 이는 기울기를(탄젠트) 의미한다. $\alpha$는 훈련비율로서, 너무 적으면 기울기 하강 알고리즘이 느려지지만 최소값에 가까워지고, 너무 크면 최소값을 지나치게 되어, 잘못된 결과를 도출하게 된다.

![그래프](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/UJpiD6GWEeai9RKvXdDYag_3c3ad6625a2a4ec8456f421a2f4daf2e_Screenshot-2016-11-03-00.05.27.png?expiry=1519344000000&hmac=YslBFRTe2oZO8WXQUSK8mW6Zbe7RXPXl3_I-dpSB8sw)
