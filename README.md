# Efficient-Frontier-Analysis
Efficient frontier의 예상(Estimate frontier)과 실제(Actual frontier) 투자곡선의 괴리는 필연적이다. 이는 과거 데이터를 통한 예측 값과 실제 투자 값의 오차에서 그 원인을 찾을 수 있다.

## 코드 설명 및 분석 순서


<!-- Output copied to clipboard! -->

<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 8.974 seconds.


Using this HTML file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β29
* Tue Jun 08 2021 22:26:49 GMT-0700 (PDT)
* Source doc: 논문 작성 준비
* Tables are currently converted to HTML tables.
* This document has images: check for >>>>>  gd2md-html alert:  inline image link in generated source and store images to your server. NOTE: Images in exported zip file from Google Docs may not appear in  the same order as they do in your doc. Please check the images!

----->


<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 0; ALERTS: 23.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>
<a href="#gdcalert6">alert6</a>
<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>
<a href="#gdcalert10">alert10</a>
<a href="#gdcalert11">alert11</a>
<a href="#gdcalert12">alert12</a>
<a href="#gdcalert13">alert13</a>
<a href="#gdcalert14">alert14</a>
<a href="#gdcalert15">alert15</a>
<a href="#gdcalert16">alert16</a>
<a href="#gdcalert17">alert17</a>
<a href="#gdcalert18">alert18</a>
<a href="#gdcalert19">alert19</a>
<a href="#gdcalert20">alert20</a>
<a href="#gdcalert21">alert21</a>
<a href="#gdcalert22">alert22</a>
<a href="#gdcalert23">alert23</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>


<p>
정규화 변수변화
</p>
<p>
로그안취하고 -> 정규화x
</p>
<p>
로그안취하고 -> 정규화o 
</p>
<p>
모두로그 -> 정규화o
</p>
<p>
부분로그 -> 정규화o
</p>
<p>
정규화 -> 부분로그 
</p>
<p>
정규화 -> 모두로그 
</p>
<p>
2. 또하나는 : 우리가 분석한것은 분석의 오류가 있는것을 
</p>
<p>
   1) 우선 앞부분인 act - est 의 차이를 진행한것을
</p>
<p>
       word 2~5페이지로 설명하는것을 목표로 하자 
</p>
<p>
   2) 지금 작성할 때는 논문형태보다는 내용을 정리
</p>
<p>
       한다는 생각으로 하면될거 같아 
</p>
<p>
   3) 오류의 유무를 잘 활용하기 위해서는 
</p>
<p>
       ~생각했는데 어떤 오류가 있었다는 것을 문서에 하면 좋을듯
</p>
<p>
Q1 ) 교수님께서 보내주신 url을 통해 얻은 데이터에는 SMB, HML, RMW, CMA. RF, mkt-rf가 있었습니다. 그 중에서 SMB, HML, RMW, CMA, RF만을 넣고 분석을 실시하였는데, mkt-rf가 더 중요한 변수인 것 같다는 생각이 들었습니다. RF를 빼고 mkt-rf를 넣는 것이 맞는지 여쭙고 싶습니다. 
</p>
<p>
 ※ mkt-rf는 return of the market portfolio - risk-free return rate 인 것 같습니다.
</p>
<ol>

<li>1975년 1월 1일 ~ 2019년 12월 1일까지의 49개의 산업군 데이터를 이용하여 6개월 간격의 Estimate Frontier와 1개월 간격의 Actual Frontier 구현(총 534개 data set)
</li>
</ol>
<ol>

<li>각각 구한 Estimate Frontier와 Actual Frontier의 거리를 Euclidean, Cosine, Frechet 방법으로 계산  
<ol>
 
<li>1975.01 - 1975.06 까지의 Estimate과 1975.07의 Actual 사이의 거리
 
<li>1975.02 - 1975.07 까지의 Estimate과 1975.08의 Actual 사이의 거리
 
<li>….
 
<li>2019.06 - 2019.11 까지의 Estimate과 2019.12의 Actual 사이의 거리  
</li> 
</ol>
</li> 
</ol>
<ol>

<li>Estimate Frontier와 Actual Frontier의 거리에 영향을 줄 수 있을 만한 factor 수집 
<ol>
 
<li>각각의 factor는 1975.07.01 - 2019.12.01까지의 data(즉, Actual Frontier의 기간과 일치)
</li> 
</ol>
</li> 
</ol>
<ol>

<li>각 factor를 normalize 한 후 Feature Selection(forward, backward, stepwise)를 통해 feature 선정
</li>
</ol>
<ol>

<li>VIF 분석을 통해 VIF 값이 10 이하의 값을 갖도록 변수 제거
</li>
</ol>
<ol>

<li>사용한 라이브러리
</li>
</ol>
<p>


<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image1.png" width="" alt="alt_text" title="image_tooltip">

</p>
<ol>

<li>데이터 불러오기(49개 산업군에 대한 일일 수익률) 및 Estimate & Actual 을 위한 데이터 분류(6개월, 1개월)
</li>
</ol>
<p>


<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image2.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image3.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image4.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
평균적으로 한 달에 근무하는 일은 22일이지만, 모든 달이 22일을 근무한다고 할 수 없기 때문에 groupby 함수를 통해 연도, 월 별로 구분했습니다. (이렇게 해야 월 별로 딱 떨어지기 때문에 추후에 데이터 처리하기가 더 편하다고 판단하였습니다. 상단에 존재하는 데이터는 해당 년도, 해당 월의 평균 수익률입니다.)
</p>
<p>
6개월 가량의 데이터를 통해 구해야하는 Estimate Frontier를 위해 1975.01-2019.12의 데이터를 6개월 기간으로 분할하였습니다. Actual Frontier를 위한 데이터(1개월)도 마찬가지로 진행하였습니다.
</p>
<ol>

<li>6개월치 데이터의 후반 6개 데이터 삭제 & 1개월치 데이터의 초반 6개 데이터 삭제
</li>
</ol>
<p>


<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image5.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
6개월 단위로 데이터를 나누다 보면 2019.07-2019-12, 2019.08-2019.12, 2019.09-2019.12, 2019.10-2019.12,
</p>
<p>
2019.11-2019.12, 2019.12-2019.12 등의 상위 6개 항목은 그에 해당되는 Actual Frontier의 기간이 존재하지 않는 것을 알 수 있습니다. 때문에 6개월 단위로 나눈 데이터 중 후반부에 존재하는 6개의 데이터는 삭제하였습니다. 마찬가지로 1개월 단위로 분할한 데이터 중 초반부에 존재하는 6개의 데이터는 그에 대응하는 Estimate Frontier 기간이 존재하지 않기 때문에 삭제하였습니다.
</p>
<ol>

<li>Estimate Data와 Actual Data가 잘 대응하는지 점검
</li>
</ol>
<p>


<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image6.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image7.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image7.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
Estimate Data와 Actual Data의 개수 동일 & 기간의 대응도 완벽히 되어있는 것을 볼 수 있습니다.
</p>
<ol>

<li>Efficient Frontier를 그리기 위한 portfolio opt 함수 작성
</li>
</ol>
<p>


<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image8.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image9.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
“CPLEX”를 solver로 하여, 최소의 risk로 최대의 return을 나타내는 Efficient Frontier를 나타내기 위한 함수입니다.
</p>
<ol>

<li>Actual Frontier를 구현하는 과정
</li>
</ol>
<p>


<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image10.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image11.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image11.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
Efficient Frontier를 구하고 난 후, 그 때 사용하였던 weight, Actual 기간의 mu와 variance를 이용하여 Actual Frontier를 구현하는 과정입니다. Estimate Frontier, Actual Frontier에 사용되는 mu와 variance를 리스트에 따로 저장하였습니다.
</p>
<ol>

<li>csv 파일로 저장하는 부분
</li>
</ol>
<p>


<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image12.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image12.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
리스트에 저장한 데이터를 거리 계산하는 코드에 쉽게 사용하기 위해 csv 파일로 옮겨 저장하는 과정입니다.
</p>
<p>
11.  est-act frontier의 차이를 유클리드 거리로 계산 
</p>
<p>


<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image13.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image13.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
-> 위에서 도출한, evols : , erets : , avols : ,  arets :  를 E_D함수에 넣어서 유클리드 거리를 도출한다.  
</p>
<p>


<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image14.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image14.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
Estimate-Actual Frontier간 거리를 계산하기 위한 데이터는 위와 같은데,  1개월 간격으로 Estimate Frontier와 Actual Frontier 구현한 것을 데이터로 만든것입니다.
</p>
<p>
위에서 1열은 0~509개의 번호로 이뤄져 있는데 이는 각각 월을 뜻하며, (1975년 1월 1일 ~ 2019년 12월 1일 데이터 사용했으며 Ex) 첫번째 데이터를 예시로보면  75년01월~75년06월 데이터를 사용하여 곡선을 그린것이 0행입니다.) 
</p>
<p>
 0행을 기준으로 볼때, 앞선 단계에서 Estimate 곡선 한개를 30개의 점으로 만들어 erets(y축 return), evols(x축 volatility)로 만들었고, Actual 곡선또한 마찬가지로  arets(y축 return), avols(x축 volatility)좌표로 만들었습니다. 
</p>
<p>
 0행을 기준으로 본다면(나머지 행도 같습니다), 한 투자곡선당(한 행) 30개의 좌표순서쌍이 있고 1. (evols, erets) 2. (avols, arets), 이 좌표순서쌍 각각을 유클리도 거리로 거리를 구한뒤 30개의 거리를 모두더한 값이 좌측의 0행의 값으로 도출 되었습니다.
</p>
<p>
각각의 좌표순서쌍은 
</p>
<p>
dist += distance.euclidean(  [evols[i], erets[i]]    ,   [avols[i], arets[i]]  )를 통해 계산되었습니다.
</p>
<p>
https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.euclidean.html
</p>
<p>
distance.euclidean의 설명은 위와 같습니다. 
</p>
<p>
12.  est-act frontier의 차이를 코사인 거리로 계산
</p>
<p>


<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image15.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image15.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
위의 유클리드 거리와 같은 input data를 사용했으며, 좌표쌍이 들어가는 방법 또한 같습니다. 코사인 거리를 사용한 이유는, ~인데 ~이유에서인지 결과가 잘 나오지 않았습니다.
</p>
<p>
<a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cosine.html">https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cosine.html</a>
</p>
<p>
12.  est-act frontier의 차이를 프레쉐 거리로 계산 
</p>
<p>
프레쉐거리의 경우 교수님이 고쳐주신 코드를 그대로 사용하고 있습니다.
</p>
<h3>## 모두 유클리드를 Y변수로 하였습니다.</h3>


<p>
기존 log 취하기전 
</p>
<p>
forward
</p>
<p>
 Housing + NFCI + RF + CPIAUCSL
</p>
<p>
backward
</p>
<p>
SP500 + BUSLOANS + CPIAUCSL + Housing + NFCI + RF
</p>
<p>
stepwise
</p>
<p>
Housing + NFCI + RF + CPIAUCSL
</p>
<p>
log 적용 후
</p>
<p>
forward
</p>
<p>
Housing + NFCI + RF+SP500 + BUSLOANS + long_term + Month_3 + SMB
</p>
<p>
backward
</p>
<p>
SP500 + BUSLOANS + Month_3 +Inflation + Housing + long_term + NFCI + M3 + SMB + RF
</p>
<p>
stepwise
</p>
<p>
Housing + NFCI + RF + SP500 + BUSLOANS + long_term
</p>
<p>
### distance ~ regression
</p>
<p>
 
</p>
<p>
12.  데이터에 대한 설명 독립변수 
</p>
<p>
독립변수로 사용된 지표이며 모두 월별데이터입니다.
</p>

<table>
  <tr>
   <td>변수명
   </td>
   <td>설명
   </td>
   <td>단위
   </td>
   <td>평균
   </td>
   <td>최소
   </td>
   <td>최대
   </td>
   <td>출처
   </td>
  </tr>
  <tr>
   <td>Real_Effective 
   </td>
   <td>Real effective exchange rates are calculated as weighted averages of bilateral exchange rates adjusted by relative consumer prices.
   </td>
   <td>Index 2010=100,
<p>
Seasonally Adjusted
   </td>
   <td>110.13
   </td>
   <td>92.94
   </td>
   <td>147.05
   </td>
   <td><a href="https://fred.stlouisfed.org/series/RNUSBIS">https://fred.stlouisfed.org/series/RNUSBIS</a>
   </td>
  </tr>
  <tr>
   <td>SP500
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>911.33
   </td>
   <td>83.87
   </td>
   <td>3230.78
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>BUSLOANS 
   </td>
   <td>View data of the value of loans issued by all commercial banks for commercial and industrial purposes each month.
   </td>
   <td>Billions of U.S. Dollars, Seasonally Adjusted
   </td>
   <td>5.065
   </td>
   <td>0.110
   </td>
   <td>18.650
   </td>
   <td><a href="https://fred.stlouisfed.org/series/BUSLOANS">https://fred.stlouisfed.org/series/BUSLOANS</a>
   </td>
  </tr>
  <tr>
   <td>Month_3 
   </td>
   <td>3-Month or 90-day Rates and Yields: Interbank Rates for the United States
   </td>
   <td>Percent,
<p>
Not Seasonally Adjusted
   </td>
   <td>5.065
   </td>
   <td>0.110
   </td>
   <td>18.650
   </td>
   <td><a href="https://fred.stlouisfed.org/series/IR3TIB01USM156N">https://fred.stlouisfed.org/series/IR3TIB01USM156N</a>
   </td>
  </tr>
  <tr>
   <td>CPIAUCSL 
   </td>
   <td>The Consumer Price Index for All Urban Consumers: All Items (CPIAUCSL) is a measure of the average monthly change in the price for goods and services paid by urban consumers between any two time periods. It can also represent the buying habits of urban consumers.
   </td>
   <td>Index 1982-1984=100,
<p>
Seasonally Adjusted
   </td>
   <td>160.3
   </td>
   <td>54
   </td>
   <td>258.4
   </td>
   <td><a href="https://fred.stlouisfed.org/series/CPIAUCSL">https://fred.stlouisfed.org/series/CPIAUCSL</a>
   </td>
  </tr>
  <tr>
   <td>CCI 
   </td>
   <td>indicator provides an indication of future developments of households’ consumption and saving, based upon answers regarding their expected financial situation, their sentiment about the general economic situation, unemployment and capability of savings. 
   </td>
   <td><strong>Amplitude adjusted, Long-term average = 100</strong>
   </td>
   <td>99.93
   </td>
   <td>96.2
   </td>
   <td>102.6
   </td>
   <td>https://data.o
<p>
ecd.org
   </td>
  </tr>
  <tr>
   <td>Inflation 
   </td>
   <td>The <strong><em>Inflation rate</em></strong> is calculated from the Consumer Price Index (<a href="https://inflationdata.com/Inflation/Consumer_Price_Index/CPI.asp">CPI-U</a>) which is compiled by the <a href="http://stats.bls.gov/news.release/cpi.t01.htm">U.S. Bureau of Labor Statistics</a> and is based upon a 1982-84 Base of 100.
   </td>
   <td>
   </td>
   <td>0.00294
   </td>
   <td>-0.0192
   </td>
   <td>0.0152
   </td>
   <td><a href="https://inflationdata.com/Inflation/Inflation_Rate/HistoricalInflation.aspx#table">https://inflationdata.com/Inflation/Inflation_Rate/HistoricalInflation.aspx#table</a>
   </td>
  </tr>
  <tr>
   <td>Housing 
   </td>
   <td>미국 주택 가격 지수
   </td>
   <td>
   </td>
   <td>20.01
   </td>
   <td>6.79
   </td>
   <td>123.73
   </td>
   <td>http://www.m
<p>
ultpl.com
   </td>
  </tr>
  <tr>
   <td>long_term 
   </td>
   <td>Long-Term Government Bond Yields: 10-year: Main (Including Benchmark) for the United States
   </td>
   <td>Percent,
<p>
Not Seasonally Adjusted
   </td>
   <td>6.252
   </td>
   <td>1.5
   </td>
   <td>15.32
   </td>
   <td><a href="https://fred.stlouisfed.org/series/IRLTLT01USM156N">https://fred.stlouisfed.org/series/IRLTLT01USM156N</a>
   </td>
  </tr>
  <tr>
   <td>NFCI 
   </td>
   <td>The Chicago Fed's National Financial Conditions Index (NFCI) provides a comprehensive weekly update on U.S. financial conditions in money markets, debt and equity markets and the traditional and "shadow" banking systems. Positive values of the NFCI indicate financial conditions that are tighter than average, while negative values indicate financial conditions that are looser than average.
   </td>
   <td>Index, Not Seasonally Adjusted
   </td>
   <td>-0.1170
   </td>
   <td>-0.98
   </td>
   <td>3.79
   </td>
   <td><a href="https://fred.stlouisfed.org/series/NFCI#0">https://fred.stlouisfed.org/series/NFCI#0</a>
   </td>
  </tr>
  <tr>
   <td>M3
   </td>
   <td>총유동성, 전체 통화에 증권, 보험 등 제2금융권의 예금까지 모두
<p>
포함한 통화지표
<p>
Copyright, 2016, OECD. Reprinted with permission.
   </td>
   <td>National Currency,
<p>
Seasonally Adjusted
   </td>
   <td>5.562e+12
   </td>
   <td>9.750e+11
   </td>
   <td>1.530e+13
   </td>
   <td><a href="https://fred.stlouisfed.org/series/MABMM301USM189S">https://fred.stlouisfed.org/series/MABMM301USM189S</a>
   </td>
  </tr>
  <tr>
   <td>Unemployment_Rate 
   </td>
   <td>The unemployment rate represents the number of unemployed as a percentage of the labor force. Labor force data are restricted to people 16 years of age and older, who currently reside in 1 of the 50 states or the District of Columbia, who do not reside in institutions (e.g., penal and mental facilities, homes for the aged), and who are not on active duty in the Armed Forces.
   </td>
   <td>Percent, Seasonally Adjusted
   </td>
   <td>6.265
   </td>
   <td>3.5
   </td>
   <td>10.8
   </td>
   <td><a href="https://fred.stlouisfed.org/series/UNRATE">https://fred.stlouisfed.org/series/UNRATE</a>
   </td>
  </tr>
  <tr>
   <td>SMB
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>0.2079
   </td>
   <td>-14.91
   </td>
   <td>18.32
   </td>
   <td><a href="https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/f-f_5_factors_2x3.html">https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/f-f_5_factors_2x3.html</a>
   </td>
  </tr>
  <tr>
   <td>HML
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>0.262
   </td>
   <td>-11.18
   </td>
   <td>12.87
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>RMW
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>0.3243
   </td>
   <td>-18.33
   </td>
   <td>13.33
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>CMA
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>0.2635
   </td>
   <td>-6.86
   </td>
   <td>9.56
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>mkt - RF
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>0.3667
   </td>
   <td>0.00
   </td>
   <td>1.35
   </td>
   <td>
   </td>
  </tr>
</table>


<p>
13. Forward Selection
</p>
<p>


<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image16.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image16.png" width="" alt="alt_text" title="image_tooltip">

</p>
<ol>

<li>processSubset은 앞으로 더 좋은 결과의 변수집합을 업데이트 하기위해, 각 변수의 Modeling 결과를 반환하는 역할을 하며, 반환되는 정보는 OLS의 결과인 ‘model’과 AIC결과이다
</li>
</ol>
<p>


<p id="gdcalert17" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image17.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert18">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image17.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
변수 전진선택법은 “AIC”기준 가장 낮은 값을 선택한다.  함수는 두가지인데
</p>
<p>
첫번째로, forward 함수는 아래와 같은 값을 반환함 
</p>
<p>


<p id="gdcalert18" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image18.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert19">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image18.png" width="" alt="alt_text" title="image_tooltip">

</p>
<ol>

<li>remaining_predictors = [p for p in X.columns if p not in predictors] 
<p>

    forward_model 함수에서 전달받은 predictors( 기존 선택변수 ) 에 포함되지 않은 변수를 remaining_predictors에 저장한다.
</p>
<ol>

<li>for문을 통해 추가되지 않은 변수를 processSubset 변수에 넣어보고 그 결과를 result에 append를 통해 저장한다.  /  models에 결과를 데이터프레임 형태로 저장한다.

<li>best_model = models.loc[models['AIC'].argmin()]   &lt;-  argmin을 통해 AIC값이 가장 작은 결고를 선택해서 저장한다. 이후 이값을 반환함
</li>
</ol>
</li>
</ol>
<p>
두번째로, forward_model 함수는 
</p>
<ol>

<li>우선 forward_model 함수 안에 X(독립변수), y(종속변수)를 대입

<li>for i in range(1, len(X.columns) + 1):  에 의해 독립변수의 개수만큼 for문이 돌아간다

<li>우선 아무것도 변수집합 predictors = [] 을 forward함수로 줘서 결과를 Forward_result에 반환받는다.

<li>if i >1 에서, 두번째 for문 시행부터 AIC가 기존보다 큰지 검사를 하며, 클 경우 break

<li>  Fmodels.loc[i] = Forward_result              &lt;- 결과를 Fmodels.loc에 담는다.
</li>
</ol>
<p>
  predictors = Fmodels.loc[i]["model"].model.exog_names &lt;-  담긴 결과를 predictors에 업데이트 
</p>
<p>

      Fmodel_before = Fmodels.loc[i]["AIC"]           &lt;-  다음 for문에서 AIC비교를 위해 담아준다.
</p>
<p>

      predictors = [ k for k in predictors if k != 'const']  &lt;-  업데이트된 변수중 상수는 걸러낸다
</p>
<ol>

<li>이후 독립변수의 개수( len(X.columns)  ) 만큼 for문을 반복하며,  더 좋은결과의 변수로 업데이트 하기전 if문을 통해 AIC가 개선되지 않았다면 업데이트 하지 않고 break
</li>
</ol>
<p>
14. Backward Elimination
</p>
<p>


<p id="gdcalert19" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image19.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert20">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image19.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
backward함수도 forward와 마찬가지로 AIC값이 가장낮은 변수조합을 찾는것이 목표다.
</p>
<ol>

<li>AIC와 model 열을 가진 데이터프레임 Bmodels을 만든다.  predictors는 계속해서 줄어들며 업데이트가 되는데  backward 이기에 모든 변수인 X.columns 부터 시작한다. 

<li>while문을 통해 변수셋이 1개 이하로 떨어지기 전까지는 AIC값이 낮은 변수셋을 찾는 과정을 반복하게 된다.

<li>backward 함수를 통해 변수셋이 하나씩 줄어든 값을 반환받으므로,  Bmodels.loc[]에 순차적으로 backward함수의 결과인Backward_result를 기입합니다.

<li>Bmodel_before에 업데이트된 AIC값을 넣어, if, break의 비교에 사용합니다. 
</li>
</ol>
<p>
좌측의 사진과 같이, 16 -> 1개의 변수를 향해 업데이트를 합니다. 만약 다음 업데이트의 AIC값이 기존보다 크다면 멈춥니다. 
</p>
<p>
15.Stepwise Selection
</p>
<p>


<p id="gdcalert20" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image20.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert21">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image20.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
16. 모든 변수 적용시 회귀분석 
</p>
<p>


<p id="gdcalert21" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image21.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert22">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image21.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert22" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image22.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert23">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image22.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>


<p id="gdcalert23" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image23.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert24">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image23.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
17. forward, backward, stepwise 결과
</p>
<p>
18. VIF 결과 및 수치가 높은 변수 제거 ( >10 )
</p>
