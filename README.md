# Efficient-Frontier-Analysis
Efficient frontier의 예상(Estimate frontier)과 실제(Actual frontier) 투자곡선의 괴리는 필연적이다. 이는 과거 데이터를 통한 예측 값과 실제 투자 값의 오차에서 그 원인을 찾을 수 있다.

## 코드 설명 및 분석 순서


## 1. 사용한 라이브러리

## 2. 데이터 불러오기(49개 산업군에 대한 일일 수익률) 및 Estimate & Actual 을 위한 데이터 분류(6개월, 1개월)



평균적으로 한 달에 근무하는 일은 22일이지만, 모든 달이 22일을 근무한다고 할 수 없기 때문에 groupby 함수를 통해 연도, 월 별로 구분했습니다. 이렇게 해야 월 별로 딱 떨어지기 때문에 추후에 데이터 처리하기가 더 편하다고 판단하였습니다. 상단에 존재하는 데이터는 해당 년도, 해당 월의 평균 수익률입니다.
## 3. 6개월 가량의 데이터를 통해 구해야하는 Estimate Frontier를 위해 1975.01-2019.12의 데이터를 6개월 기간으로 분할하였습니다. Actual Frontier를 위한 데이터(1개월)도 마찬가지로 진행하였습니다.
6개월치 데이터의 후반 6개 데이터 삭제 & 1개월치 데이터의 초반 6개 데이터 삭제

6개월 단위로 데이터를 나누다 보면 2019.07-2019-12, 2019.08-2019.12, 2019.09-2019.12, 2019.10-2019.12,
2019.11-2019.12, 2019.12-2019.12 등의 상위 6개 항목은 그에 해당되는 Actual Frontier의 기간이 존재하지 않는 것을 알 수 있습니다. 때문에 6개월 단위로 나눈 데이터 중 후반부에 존재하는 6개의 데이터는 삭제하였습니다. 마찬가지로 1개월 단위로 분할한 데이터 중 초반부에 존재하는 6개의 데이터는 그에 대응하는 Estimate Frontier 기간이 존재하지 않기 때문에 삭제하였습니다.

## 4. Estimate Data와 Actual Data가 잘 대응하는지 점검



Estimate Data와 Actual Data의 개수 동일 & 기간의 대응도 완벽히 되어있는 것을 볼 수 있습니다.





## 5. Efficient Frontier를 그리기 위한 portfolio opt 함수 작성


“CPLEX”를 solver로 하여, 최소의 risk로 최대의 return을 나타내는 Efficient Frontier를 나타내기 위한 함수입니다.

## 6. Actual Frontier를 구현하는 과정


Efficient Frontier를 구하고 난 후, 그 때 사용하였던 weight, Actual 기간의 mu와 variance를 이용하여 Actual Frontier를 구현하는 과정입니다. Estimate Frontier, Actual Frontier에 사용되는 mu와 variance를 리스트에 따로 저장하였습니다.





## 7. csv 파일로 저장하는 부분

리스트에 저장한 데이터를 거리 계산하는 코드에 쉽게 사용하기 위해 csv 파일로 옮겨 저장하는 과정입니다.

## 8. est-act frontier의 차이를 유클리드 거리로 계산 

-> 위에서 도출한, evols : , erets : , avols : ,  arets :  를 E_D함수에 넣어서 유클리드 거리를 도출한다.  

Estimate-Actual Frontier간 거리를 계산하기 위한 데이터는 위와 같은데,  1개월 간격으로 Estimate Frontier와 Actual Frontier 구현한 것을 데이터로 만든것입니다.
위에서 1열은 0~509개의 번호로 이뤄져 있는데 이는 각각 월을 뜻하며, (1975년 1월 1일 ~ 2019년 12월 1일 데이터 사용했으며 Ex) 첫번째 데이터를 예시로보면  75년01월~75년06월 데이터를 사용하여 곡선을 그린것이 0행입니다.) 
 0행을 기준으로 볼때, 앞선 단계에서 Estimate 곡선 한개를 30개의 점으로 만들어 erets(y축 return), evols(x축 volatility)로 만들었고, Actual 곡선또한 마찬가지로  arets(y축 return), avols(x축 volatility)좌표로 만들었습니다. 

 0행을 기준으로 본다면(나머지 행도 같습니다), 한 투자곡선당(한 행) 30개의 좌표순서쌍이 있고 1. (evols, erets) 2. (avols, arets), 이 좌표순서쌍 각각을 유클리도 거리로 거리를 구한뒤 30개의 거리를 모두더한 값이 좌측의 0행의 값으로 도출 되었습니다.

각각의 좌표순서쌍은 
dist += distance.euclidean(  [evols[i], erets[i]]    ,   [avols[i], arets[i]]  )를 통해 계산되었습니다.

https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.euclidean.html
distance.euclidean의 설명은 위와 같습니다. 

## 9.  est-act frontier의 차이를 코사인 거리로 계산

위의 유클리드 거리와 같은 input data를 사용했으며, 좌표쌍이 들어가는 방법 또한 같습니다. 

https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cosine.html





## 10.  est-act frontier의 차이를 프레쉐 거리로 계산 


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

