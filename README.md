# Efficient-Frontier-Analysis
Efficient frontier의 예상(Estimate frontier)과 실제(Actual frontier) 투자곡선의 괴리는 필연적이다. 이는 과거 데이터를 통한 예측 값과 실제 투자 값의 오차에서 그 원인을 찾을 수 있다.

## 코드 설명 및 분석 순서


## 1. 사용한 라이브러리
![image](https://user-images.githubusercontent.com/80387630/121300367-b740f480-c931-11eb-8163-1d9cfad2be45.png)
## 2. 데이터 불러오기(49개 산업군에 대한 일일 수익률) 및 Estimate & Actual 을 위한 데이터 분류(6개월, 1개월)
![image](https://user-images.githubusercontent.com/80387630/121300382-bc05a880-c931-11eb-8211-fd4cbb46f22f.png)

![image](https://user-images.githubusercontent.com/80387630/121300401-c1fb8980-c931-11eb-99bb-d9b9067c284c.png)

![image](https://user-images.githubusercontent.com/80387630/121300416-c627a700-c931-11eb-803d-66a3ebd15baa.png)

평균적으로 한 달에 근무하는 일은 22일이지만, 모든 달이 22일을 근무한다고 할 수 없기 때문에 groupby 함수를 통해 연도, 월 별로 구분했습니다. 이렇게 해야 월 별로 딱 떨어지기 때문에 추후에 데이터 처리하기가 더 편하다고 판단하였습니다. 상단에 존재하는 데이터는 해당 년도, 해당 월의 평균 수익률입니다.

## 3. 6개월 가량의 데이터를 통해 구해야하는 Estimate Frontier를 위해 1975.01-2019.12의 데이터를 6개월 기간으로 분할하였습니다. Actual Frontier를 위한 데이터(1개월)도 마찬가지로 진행하였습니다.
![image](https://user-images.githubusercontent.com/80387630/121300433-ca53c480-c931-11eb-893c-93d0f7158474.png)

6개월치 데이터의 후반 6개 데이터 삭제 & 1개월치 데이터의 초반 6개 데이터 삭제
6개월 단위로 데이터를 나누다 보면 2019.07-2019-12, 2019.08-2019.12, 2019.09-2019.12, 2019.10-2019.12,
2019.11-2019.12, 2019.12-2019.12 등의 상위 6개 항목은 그에 해당되는 Actual Frontier의 기간이 존재하지 않는 것을 알 수 있습니다. 때문에 6개월 단위로 나눈 데이터 중 후반부에 존재하는 6개의 데이터는 삭제하였습니다. 마찬가지로 1개월 단위로 분할한 데이터 중 초반부에 존재하는 6개의 데이터는 그에 대응하는 Estimate Frontier 기간이 존재하지 않기 때문에 삭제하였습니다.

## 4. Estimate Data와 Actual Data가 잘 대응하는지 점검
![image](https://user-images.githubusercontent.com/80387630/121300445-ce7fe200-c931-11eb-9fa7-dbb116cc44f0.png)

![image](https://user-images.githubusercontent.com/80387630/121300456-d3449600-c931-11eb-9258-edee4e6be0b2.png)


Estimate Data와 Actual Data의 개수 동일 & 기간의 대응도 완벽히 되어있는 것을 볼 수 있습니다.





## 5. Efficient Frontier를 그리기 위한 portfolio opt 함수 작성
![image](https://user-images.githubusercontent.com/80387630/121300473-d9d30d80-c931-11eb-8969-ec7de5874b62.png)

![image](https://user-images.githubusercontent.com/80387630/121300485-db9cd100-c931-11eb-88ae-ede3f2b5c5d4.png)

“CPLEX”를 solver로 하여, 최소의 risk로 최대의 return을 나타내는 Efficient Frontier를 나타내기 위한 함수입니다.

## 6. Actual Frontier를 구현하는 과정
![image](https://user-images.githubusercontent.com/80387630/121300494-de97c180-c931-11eb-9a63-24b89e83ca92.png)

![image](https://user-images.githubusercontent.com/80387630/121300499-e0618500-c931-11eb-8230-8a0c0818272a.png)

Efficient Frontier를 구하고 난 후, 그 때 사용하였던 weight, Actual 기간의 mu와 variance를 이용하여 Actual Frontier를 구현하는 과정입니다. Estimate Frontier, Actual Frontier에 사용되는 mu와 variance를 리스트에 따로 저장하였습니다.





## 7. csv 파일로 저장하는 부분
![image](https://user-images.githubusercontent.com/80387630/121300506-e35c7580-c931-11eb-808e-fd1af7880d4d.png)

리스트에 저장한 데이터를 거리 계산하는 코드에 쉽게 사용하기 위해 csv 파일로 옮겨 저장하는 과정입니다.

## 8. est-act frontier의 차이를 유클리드 거리로 계산 
![image](https://user-images.githubusercontent.com/80387630/121300514-e5becf80-c931-11eb-8999-0cebcce0f42d.png)

-> 위에서 도출한, evols : , erets : , avols : ,  arets :  를 E_D함수에 넣어서 유클리드 거리를 도출한다.  ![image](https://user-images.githubusercontent.com/80387630/121300519-e7889300-c931-11eb-965a-a13904194369.png)


Estimate-Actual Frontier간 거리를 계산하기 위한 데이터는 위와 같은데,  1개월 간격으로 Estimate Frontier와 Actual Frontier 구현한 것을 데이터로 만든것입니다.
위에서 1열은 0-509개의 번호로 이뤄져 있는데 이는 각각 월을 뜻하며, (1975년 1월 1일 ~ 2019년 12월 1일 데이터 사용했으며 Ex) 첫번째 데이터를 예시로보면  75년01월-75년06월 데이터를 사용하여 곡선을 그린것이 0행입니다.) 
 0행을 기준으로 볼때, 앞선 단계에서 Estimate 곡선 한개를 30개의 점으로 만들어 erets(y축 return), evols(x축 volatility)로 만들었고, Actual 곡선또한 마찬가지로  arets(y축 return), avols(x축 volatility)좌표로 만들었습니다. 
![image](https://user-images.githubusercontent.com/80387630/121300543-ed7e7400-c931-11eb-8f85-75f5b5b13f53.png)

 0행을 기준으로 본다면(나머지 행도 같습니다), 한 투자곡선당(한 행) 30개의 좌표순서쌍이 있고 1. (evols, erets) 2. (avols, arets), 이 좌표순서쌍 각각을 유클리도 거리로 거리를 구한뒤 30개의 거리를 모두더한 값이 좌측의 0행의 값으로 도출 되었습니다.

각각의 좌표순서쌍은 
dist += distance.euclidean(  [evols[i], erets[i]]    ,   [avols[i], arets[i]]  )를 통해 계산되었습니다.

https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.euclidean.html
distance.euclidean의 설명은 위와 같습니다. 

## 9.  est-act frontier의 차이를 코사인 거리로 계산
![image](https://user-images.githubusercontent.com/80387630/121300551-f111fb00-c931-11eb-866e-e591966bf016.png)

![image](https://user-images.githubusercontent.com/80387630/121300565-f7a07280-c931-11eb-8875-61252f152d95.png)

위의 유클리드 거리와 같은 input data를 사용했으며, 좌표쌍이 들어가는 방법 또한 같습니다. 

https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cosine.html





## 10.  est-act frontier의 차이를 프레쉐 거리로 계산 
![image](https://user-images.githubusercontent.com/80387630/121300573-fcfdbd00-c931-11eb-9225-2adfe1c20620.png)


## 11. 모두 유클리드를 Y변수로 하였습니다.

기존 log 취하기전 
forward
 Housing + NFCI + RF + CPIAUCSL
backward
SP500 + BUSLOANS + CPIAUCSL + Housing + NFCI + RF
stepwise
Housing + NFCI + RF + CPIAUCSL


log 적용 후
forward
Housing + NFCI + RF+SP500 + BUSLOANS + long_term + Month_3 + SMB
backward
SP500 + BUSLOANS + Month_3 +Inflation + Housing + long_term + NFCI + M3 + SMB + RF
stepwise
Housing + NFCI + RF + SP500 + BUSLOANS + long_term


### distance ~ regression
 
## 12.  데이터에 대한 설명 독립변수 

독립변수로 사용된 지표이며 모두 월별데이터입니다.


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

## 13. Forward Selection
![image](https://user-images.githubusercontent.com/80387630/121300623-0d159c80-c932-11eb-9ac2-cf60857d5305.png)

processSubset은 앞으로 더 좋은 결과의 변수집합을 업데이트 하기위해, 각 변수의 Modeling 결과를 반환하는 역할을 하며, 반환되는 정보는 OLS의 결과인 ‘model’과 AIC결과이다
![image](https://user-images.githubusercontent.com/80387630/121300651-17d03180-c932-11eb-9a15-e68411d26ffb.png)

변수 전진선택법은 “AIC”기준 가장 낮은 값을 선택한다.  함수는 두가지인데

### 첫번째로, forward 함수는 아래와 같은 값을 반환함 

 1) remaining_predictors = [p for p in X.columns if p not in predictors] forward_model 함수에서 전달받은 predictors( 기존 선택변수 ) 에 포함되지 않은 변수를 remaining_predictors에 저장한다.

 2) for문을 통해 추가되지 않은 변수를 processSubset 변수에 넣어보고 그 결과를 result에 append를 통해 저장한다.  /  models에 결과를 데이터프레임 형태로 저장한다.

 3) best_model = models.loc[models['AIC'].argmin()]   <-  argmin을 통해 AIC값이 가장 작은 결고를 선택해서 저장한다. 이후 이값을 반환함

### 두번째로, forward_model 함수는 
 1) 우선 forward_model 함수 안에 X(독립변수), y(종속변수)를 대입
 2) for i in range(1, len(X.columns) + 1):  에 의해 독립변수의 개수만큼 for문이 돌아간다
 3) 우선 아무것도 변수집합 predictors = [] 을 forward함수로 줘서 결과를 Forward_result에 반환받는다.
 4) if i >1 에서, 두번째 for문 시행부터 AIC가 기존보다 큰지 검사를 하며, 클 경우 break
  Fmodels.loc[i] = Forward_result              <- 결과를 Fmodels.loc에 담는다.
  predictors = Fmodels.loc[i]["model"].model.exog_names <-  담긴 결과를 predictors에 업데이트 
  Fmodel_before = Fmodels.loc[i]["AIC"]           <-  다음 for문에서 AIC비교를 위해 담아준다.
  predictors = [ k for k in predictors if k != 'const']  <-  업데이트된 변수중 상수는 걸러낸다
 5) 이후 독립변수의 개수( len(X.columns)  ) 만큼 for문을 반복하며,  더 좋은결과의 변수로 업데이트 하기전 if문을 통해 AIC가 개선되지 않았다면 업데이트 하지 않고 break


## 14. Backward Elimination
![image](https://user-images.githubusercontent.com/80387630/121300682-1f8fd600-c932-11eb-9edf-81af6cd17f19.png)

 1) backward함수도 forward와 마찬가지로 AIC값이 가장낮은 변수조합을 찾는것이 목표다.

 2) AIC와 model 열을 가진 데이터프레임 Bmodels을 만든다.  predictors는 계속해서 줄어들며 업데이트가 되는데  backward 이기에 모든 변수인 X.columns 부터 시작한다. 

 3) while문을 통해 변수셋이 1개 이하로 떨어지기 전까지는 AIC값이 낮은 변수셋을 찾는 과정을 반복하게 된다.

 4) backward 함수를 통해 변수셋이 하나씩 줄어든 값을 반환받으므로,  Bmodels.loc[]에 순차적으로 backward함수의 결과인Backward_result를 기입합니다.

 5) Bmodel_before에 업데이트된 AIC값을 넣어, if, break의 비교에 사용합니다. 

 6) 좌측의 사진과 같이, 16 -> 1개의 변수를 향해 업데이트를 합니다. 만약 다음 업데이트의 AIC값이 기존보다 크다면 멈춥니다. 
![image](https://user-images.githubusercontent.com/80387630/121300692-24548a00-c932-11eb-9e65-f9c4f00df5a4.png)





## 15.Stepwise Selection

![image](https://user-images.githubusercontent.com/80387630/121300856-5534bf00-c932-11eb-8969-8bd43cbb568b.png)



## 16. 모든 변수 적용시 회귀분석 

![image](https://user-images.githubusercontent.com/80387630/121300861-5960dc80-c932-11eb-86fb-1cd3df8722f8.png)

![image](https://user-images.githubusercontent.com/80387630/121300871-5b2aa000-c932-11eb-9082-0df629c9ddea.png)

![image](https://user-images.githubusercontent.com/80387630/121300909-641b7180-c932-11eb-8019-2bca34b24f34.png)

## 17. forward, backward, stepwise 결과
## 18. VIF 결과 및 수치가 높은 변수 제거 ( >10 )




