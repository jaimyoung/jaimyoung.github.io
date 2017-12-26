---
layout: page
title: 정오표 (Errata)
permalink: /ipds-kr-errata/
date: 2017-08-05 20:03:29.000000000 -07:00
---
<p>* 계속 업데이트할 예정입니다. 오류를 발견하면 저자 (dataninjame@gmail.com)에게 알려주시거나, 이 페이지에 코멘트 해 주세요. 오탈자의 최종 리스트는 출판사에서 <a href="http://jpub.tistory.com/726">다음 페이지로</a> 정리하여 다음 쇄에 반영할 예정입니다.</p>
<div>(2017/9/9 김형석 독자님으로부터)</div>
<div></div>
<div>
<div>
<div>p.126: "여기서 z*와 t*는..." 바로 위 부분의 2개의 수식중 처음 수식은 t*가 아닌 z*입니다.</div>
<div></div>
<div>
<div>p.113: "다양한 가설검정 상황에서 비전문들을 이해하기 쉽게" -&gt; "다양한 가설검정 상황에서 비전문가들이 이해하기 쉽게"</div>
</div>
</div>
<div>
<div class="gmail_extra">
<div>p.140: "가장 오차한계가 큰 경우인 p-hat이 ..." -&gt; "p^" (수식)</div>
<div>p.157: 페이지 위의 수식의 "yhat" -&gt; "y^" (수식)</div>
<div>
<div class="gmail_extra">p.212: 하단 코드 마지막 부분에 "performance(pred_tr, ... )" =&gt; "performance(pred_rf, ... )"</div>
</div>
</div>
</div>
</div>
<p>(2017/9/29 조재근 교수님으로부터)</p>
<p>30쪽 그림 2-7이 그냥 까맣게 인쇄되었습니다. 올바른 그림은 다음과 같습니다:</p>
<p><img class="alignnone wp-image-691" src="{{ site.baseurl }}/assets/2-7.png" alt="2-7" width="1440" height="250" /></p>
<p>36쪽 아래에서 5째줄 boston house price data 주소로 찾아가면 데이터가 나타나지 않습니다.책에 나타난 https://archive.ics.uci.edu/ml/datasets/housing 가 올바른 주소인 것 같지만 현재 UCI 웹사이트가 문제인 것 같습니다. 다음 주소를 방문하면 자료 폴더를 볼 수 있습니다: https://archive.ics.uci.edu/ml/machine-learning-databases/housing/</p>
<p>56쪽 7째 줄, 8째 줄: "sample_n() 함수는 열을 랜덤 샘플링한다." -&gt; "행을 랜덤 샘플링한다"</p>
<p>111쪽 3째 줄 : "두 번째 분포는 표본표준편차의 분산이다." -&gt; "두 번째 그림은 표본표준편차의 분포이다"<br />
5째 줄 : "이론적으로는 카이제곱 분포를 따른다." -&gt; "참고로, 이론적으로는 표본표준편차의 제곱인 표본분산  s^2의 함수  (n-1)*s^2/\sigma^2 는 카이제곱분포 \chi^2(n-1) 를 따른다. 여기서 n=10은 표본크기, \sigma^2 = 1.789^2 은 참분산 값이다. https://en.wikipedia.org/wiki/Variance#Distribution_of_the_sample_variance 를 참조하라."</p>
<p>116쪽 본문 첫 문장: "예를 들어, 위의 수면제 사람들에게 P-값의 의미를 질문하면 ..." -&gt; "위의 수면제 데이터 분석 결과에 대해 사람들에게 P-값의 의미를 질문하면....."</p>
<p>126쪽 본문 첫째 줄: "95% 신뢰구간의 크기는 1/sqrt(n)이다." -&gt; "95% 신뢰구간의 크기는 1/sqrt(n)에 비례한다"</p>
<p>145쪽 회귀모형 식: "Y_i \sim \beta_0 +\beta_1 x_{1i} + ... + \beta_p x_{pi} + \epsilon_i, \epsilon_i \sim iid N(0, \sigma^2)"<br />
-&gt; "Y_i \sim \beta_0 +\beta_1 x_<strong>{i1}</strong> + ... + \beta_p x_<strong>{ip}</strong> + \epsilon_i, \epsilon_i \sim iid N(0, \sigma^2)" (첨자의 순서가 바뀌었습니다)</p>
<p>145쪽: 두 회귀식에서 오차항 엡실론 의 모양이 서로 다릅니다. 의미는 동일합니다. 둘 다 $\epsilon$ 입니다.</p>
<p>146쪽 네 번째 줄: "표준편차(Standard Error)"-&gt; "표준오차(Standard Error)"</p>
<p>146쪽 다섯째 줄: "P-값(Pr(&gt;|t|))" -&gt; "P-값(Pr(T &gt; |t|))" (통계량 T가 빠졌습니다)</p>
