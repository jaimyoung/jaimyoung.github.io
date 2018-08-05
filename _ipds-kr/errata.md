---
layout: page
title: 정오표 (Errata)
redirect_from: "/ipds-kr-errata/"
date: 2017-08-05 20:03:29.000000000 -07:00
---
- TOC
{:toc}

계속 업데이트할 예정입니다. 오류를 발견하면 저자 (dataninjame@gmail.com)에게 알려주시거나, 이 페이지에 코멘트 해 주세요. 오탈자의 최종 리스트는 출판사에서 <a href="http://jpub.tistory.com/726">다음 페이지로</a> 정리하여 다음 쇄에 반영할 예정입니다.

### (6/13/2018 김민규 독자님으로부터)

- p.183 "8.3.3 아래에 13개의 설명변수가 아닌 14개의 설명변수가 아닌지 여쭙고 싶습니다.
    adult 데이터는 wage 포함 총 15개의 변수를 포함하는 것 같은데, wage를 제외하고 또 다른 변수도 설명변수에서 제외한 것인지 잘 모르겠습니다."
    - 맞습니다. 설명변수 개수는 \\(p=14\\) 입니다. p.180의 "13개의 설명변수"도 마찬가지로 잘못입니다.
- p.185 "8.4 training, validation, test 데이터 세트로 구분하는 중에 오류가 있지 않은가 여쭙고 싶습니다.
    총 adult 데이터의 32561 개 관측치를
    `set.seed(1601)` 후 0.6 0.2 0.2 샘플링을 통해 각각
    19536 6512 6513 개의 세트로 나눕니다.
    그러나 그 후로 p.189 부터 9과glmnet 까지의 예시에는
    training 데이터세트에 training 과 validation 데이터가 함께 있는 것 같습니다.
    p.189~191의 summary(ad_glm_full) 맨 마지막의 Null deviance와 Residual deviance의 수가 training 세트보다 6512개 많습니다.
    그 때문에 제 R 에 출력된 결과물과 책의 결과물에 차이가 있는 것 같습니다.
    << validation + training 데이터로 실험 해봤으나 또 다른 것 같습니다. >>
    - 이것도 맞습니다. 지금 github 에있는 코드
    <https://github.com/jaimyoung/ipds-kr/blob/master/ch08-classification/adult/adult.R>
    를 실행해 보니 다음과 같은 결과가 나옵니다:
    ```r
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

    (Dispersion parameter for binomial family taken to be 1)

        Null deviance: 21431  on 19535  degrees of freedom
    Residual deviance: 12304  on 19437  degrees of freedom
    AIC: 12502

    Number of Fisher Scoring iterations: 15
    ```
- "그 후 9과에도 이해는 못하겠으나 ad_glmnet_fit 값들도 다르게 나옵니다."
    - 마찬가지 오류인 것 같습니다. 코드 실행 결과와 책 사이에 차이가 있으면 일단 코드 실행 결과를 믿는 것이 좋을 것 같습니다.



### (2/3/2018 장지민 독자님으로부터)

- p.150 다음 수식  
        \\( \hat y = X \hat \beta =  (X^T X)^{-1} X^T y = Hy \\)  
    에 \\(X\\) 가 빠졌습니다.
    올바른 수식은:  
        \\( \hat y = X \hat \beta =  X(X^T X)^{-1} X^T y = Hy \\)  
    입니다.

### (05/12/2018 이동희 독자님으로부터)
- "p.61 Chapter3 연습문제 4번에 캐글 IMDB 영화 정보 데이터 링크가 404로 뜹니다.(이 부분은 다음 쇄 때 수정할 필요가 있을 것 같습니다.)
    "4 (IMDB 자료 분석)
    캐글 웹사이트에서 다음 IMDB(Internet Movie Database) 영화 정보 데이터를 다운로드하도록 하자
    (<https://goo.gl/R08lpm> or <https://www.kaggle.com/deepmatrix/imdb-5000-movie-dataset> 무료 캐글 계정이 필요하다). 
    dplyr 패키지를 이용하여 다음 질문에 답하라." 
    페이지가 사라진것 같습니다. 그래서 데이터 다운을 못받고 있는데 혹시 보내주실 수 있나요?"
    - 링크가 내려진 것 같습니다. 구글에서 'imdb 5000 movie dataset' 을 검색하셔서 찾으셔야 할 것 같습니다.
        [구글검색링크](https://www.google.com/search?q=imdb+5000+movie+dataset&oq=imdb+5000+movie+dataset&aqs=chrome..69i57j69i60l2j69i64.11014j0j1&sourceid=chrome&ie=UTF-8)
        2018년 5월 현재 다음 링크에 자료가 있습니다만 앞으로 링크가 내려질 수 있으니 다시 검색하셔서 찾아야 할 것 같습니다.
        (혹시나 저작권 문제가 있을 수 있기 때문에 제 사이트에 호스트하기는 어렵습니다. 너그러운 양해 바랍니다.)
        - <https://www.kaggle.com/carolzhangdc/imdb-5000>




### (01/04/2018 양승화 독자님으로부터)
- p.71   예시 코드가 있는 두번째 box
    ```r
    df<- data.frame((gp = factor(rep(letters[1:3], each = 10)), y = rnorm(30)))
    ```
    불필요한 괄호가 들어가 있습니다.
    해당 괄호를 제거해야 정상적으로 데이터프레임이 생성됩니다.
    -->
    ```r
    df <- data.frame(gp = factor(rep(letters[1:3], each = 10)), y = rnorm(30))
    ```
- p.146
    네 번째 줄 표준편차 --> 표준오차 로 수정되어야 하는 내용이 정오표에 표시되어 있는데요.
    동일한 오류가 끝에서 다섯번째 줄에도 있습니다.  (표준편차 --> 표준오차)
- p.157
    7번째 줄
    "쉽게 픽업(classpickup)과 (classsuv)가"  --> "쉽게 픽업(classpickup)과 SUV(classsuv)"
- 11번째 줄 (오타라고 보기 좀 애매하긴 합니다만, plus-minus 를 쓰는 게 좀 더 자연스러울 것 같습니다)
    $$- 7.92 + - 1.96 * 1.62$$
    -->
    $$- 7.92 \pm 1.96 * 1.62$$
- p.185 
    예시 코드가 있는 box의 6번째 줄
    기능상 문제는 없습니다만, 이 책 전체에서 유일하게(?) "<-" 가 아닌 "="로 변수가 할당된 부분입니다.
    ```r
    validate_idx = sample(idx, n * .20)
    ```
    --> 
    ```r
    validate_idx <- sample(idx, n * .20)
    ```


### (09/09/2017 김형석 독자님으로부터)
- p.126: "여기서 \\(z^\ast\\)와 \\(t^\ast\\)는..." 
    바로 위 부분의 2개의 수식중 처음 수식은 \\(t^\ast\\)가 아닌 \\(z^\ast\\)입니다.
- p.113: "다양한 가설검정 상황에서 비전문들을 이해하기 쉽게" ->  "다양한 가설검정 상황에서 비전문가들이 이해하기 쉽게"
- p.140: "가장 오차한계가 큰 경우인 p-hat이 ..." ->  \\(\hat p\\) (수식)
- p.157: 페이지 위의 수식의 yhat ->  \\(\hat y\\) (수식)
- p.212: 하단 코드 마지막 부분에 
    `performance(pred_tr, ... )` => `performance(pred_rf, ... )`

### (09/29/2017 조재근 교수님으로부터)
- 30쪽 그림 2-7이 그냥 까맣게 인쇄되었습니다. 올바른 그림은 다음과 같습니다:
    <img src="{{ site.baseurl }}/assets/2-7.png" />
- 36쪽 아래에서 5째줄 boston house price data 주소로 찾아가면 데이터가 나타나지 않습니다.
    책에 나타난 <https://archive.ics.uci.edu/ml/datasets/housing>가 올바른 주소인 것 같지만 
    현재 UCI 웹사이트가 문제인 것 같습니다. 다음 주소를 방문하면 자료 폴더를 볼 수 있습니다: 
    <https://archive.ics.uci.edu/ml/machine-learning-databases/housing/>

- 56쪽 7째 줄, 8째 줄: "`sample_n()` 함수는 열을 랜덤 샘플링한다." ->  "행을 랜덤 샘플링한다"

- 111쪽 3째 줄 : "두 번째 분포는 표본표준편차의 분산이다." ->  "두 번째 그림은 표본표준편차의 분포이다"

- 5째 줄 : "이론적으로는 카이제곱 분포를 따른다." ->  
    "참고로, 이론적으로는 표본표준편차의 제곱인 표본분산 
    \\(s^2\\)의 함수  \\((n-1)*s^2/\sigma^2\\) 는 카이제곱분포 
    \\( \chi^2(n-1) \\)를 따른다. 여기서 \\(n=10\\)은 표본크기, 
    \\(\sigma^2 = 1.789^2\\) 은 참분산 값이다. 
    <https://en.wikipedia.org/wiki/Variance#Distribution_of_the_sample_variance>를 참조하라."
- 116쪽 본문 첫 문장: "예를 들어, 위의 수면제 사람들에게 P-값의 의미를 질문하면 ..." ->  "위의 수면제 데이터 분석 결과에 대해 사람들에게 P-값의 의미를 질문하면....."

- 126쪽 본문 첫째 줄: "95% 신뢰구간의 크기는 1/sqrt(n)이다." ->  "95% 신뢰구간의 크기는 \\(1/\sqrt(n)\\)에 비례한다"

- 145쪽 회귀모형 식: 
    - \\( Y_i \sim \beta_0 +\beta_1 x_{1i} + ... + \beta_p x_{pi} + \epsilon_i, \epsilon_i \sim iid N(0, \sigma^2) \\)
    - -> \\( Y_i \sim \beta_0 +\beta_1 x_{i1} + ... + \beta_p x_{ip} + \epsilon_i, \epsilon_i \sim iid N(0, \sigma^2) \\)
    - (첨자의 순서가 바뀌었습니다)

- 145쪽: 두 회귀식에서 오차항 엡실론 의 모양이 서로 다릅니다. 의미는 동일합니다. 둘 다 \\(\epsilon\\) (epsillon) 입니다.

- 146쪽 다섯째 줄 "`P-값(Pr(>|t|))`" 
    -> "`P-값(Pr(T > |t|)))`" (통계량 T가 빠졌습니다)

- 146쪽 네 번째 줄: "표준편차(Standard Error)" -> "표준오차(Standard Error)".

