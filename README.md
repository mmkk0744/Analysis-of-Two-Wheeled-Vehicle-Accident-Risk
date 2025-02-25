# 이륜차 교통사고 위험도 분석 : 대구광역시 교통 대시보드 구축

<br>

> ## 1. 분석개요
<img width="1000" alt="Image" src="https://github.com/user-attachments/assets/94df55e3-d02b-4b5e-b41e-012732640ff4" />

### 1. 사고 위험도 분석

#### "어떤 상황에서 이륜차 사고가 발생할 가능성이 높은가?"

- 이륜차 교통사고를 예방하기 위해서는 사고 발생의 주요 원인을 파악하고, 위험 요인을 분석하는 것이 필수적이다. 특히, 심각한 인명 피해 예방을 위해 이륜차 교통사고의 패턴과 위험도를 면밀히 분석해야 한다.

- 사고 피해 지수를 활용한 EPDO(Equivalent Property Damage Only) 지표를 산출하여 사고 위험성을 평가
- 최적의 모델을 적용하여 사고가 빈번히 발생하는 위험한 환경을 식별
- SHAP(Shapley Additive Explanations) 분석을 활용하여 사고에 영향을 미치는 요인을 정량적으로 평가

<br>

### 2. 위험 지역 선정
#### "이륜차 사고 발생 위험이 높은 지역은 어디인가?"

- 이륜차 사고를 효과적으로 예방하려면 사고 발생 가능성이 높은 지역을 선별하는 것이 중요하다. 이를 위해 사고 데이터를 기반으로 이륜차 교통사고 위험 지역을 선정한다.
- 기존 사고 예측 모델을 활용하여 특정 지역이 사고 위험도가 높은 사고 고위험 지역인지 분석
- 예측된 고위험 지역이 실제 사고가 빈번하게 발생하는 지역과 일치하는 경우, 중점 관리 지역으로 선정
- PSI(Performance-based Safety Indicator) 절차를 적용하여 도로교통지표와 사고 위험도를 종합적으로 검토

<br>

### 3. 위험 지역 특성 분석 및 개선 방안
#### "이륜차 사고 발생을 줄이기 위해 위험 지역을 어떻게 개선할 것인가?"

- 이륜차 사고 예방을 위해 위험 지역의 주요 특성을 파악하고, 이에 대한 적절한 개선 방안을 마련해야 한다.
- 상위 위험 지역의 도로 환경 및 사고 유형을 분석하여 사고 발생에 영향을 미치는 주요 요인을 도출
- 사고가 자주 발생하는 지역이 어떤 원인으로 인해 위험지역으로 선정되었는지 상세 분석
- SHAP 값을 활용하여 각 위험 요인이 사고 발생에 미치는 영향 평가

<br>

> ## 2. 분석 프로세스
<img width="1000" alt="Image" src="https://github.com/user-attachments/assets/2591888e-7220-4c66-9025-2527d8c6cb7a" />

<br>

> ## 3. EPDO 산출 예시

<table border="1">
    <thead>
        <tr>
            <th>사고 위치</th>
            <th>시점</th>
            <th>사망자수</th>
            <th>중상자수</th>
            <th>경상자수</th>
            <th>부상자수</th>
            <th style="background-color: #FFD700;">EPDO</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>대구광역시 북구 a동</td>
            <td>2019년 1월 1일 02시</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>3</td>
            <td style="background-color: #FFD700;">20</td>
        </tr>
        <tr>
            <td>대구광역시 북구 b동</td>
            <td>2019년 1월 1일 04시</td>
            <td>0</td>
            <td>0</td>
            <td>2</td>
            <td>0</td>
            <td style="background-color: #FFD700;">6</td>
        </tr>
        <tr>
            <td>대구광역시 달서구 c동</td>
            <td>2019년 1월 1일 07시</td>
            <td>3</td>
            <td>0</td>
            <td>0</td>
            <td>2</td>
            <td style="background-color: #FFD700;">38</td>
        </tr>
        <tr>
            <td>대구광역시 달서구 d동</td>
            <td>2019년 1월 2일 15시</td>
            <td>0</td>
            <td>1</td>
            <td>2</td>
            <td>1</td>
            <td style="background-color: #FFD700;">12</td>
        </tr>
    </tbody>
</table>

### EPDO(Equivalent Property Damage Only)란?
EPDO(대물피해환산계수) = 사망자수 x 12 + 중상자수 x 5 + 경상자수 x 3 + 부상신고자수

<br>

### 즉, 단순히 사고횟수를 파악하기 보단 해당 사고의 심각성을 파악할 수 있다.

<br>

> ## 4. 데이터 수집
<img width="1000" alt="Image" src="https://github.com/user-attachments/assets/510fa5c0-e509-4f62-bbbc-c3feb2f9d9d2" />


<body>

<table>
    <thead>
        <tr>
            <th>데이터</th>
            <th>제공 플랫폼</th>
            <th>데이터 상세</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>단속 카메라 데이터</td>
            <td><a href="#">공공데이터포털</a></td>
            <td>경찰청_무인교통단속카메라_20220819.csv</td>
        </tr>
        <tr>
            <td>어린이 보호구역 데이터</td>
            <td><a href="#">공공데이터포털</a></td>
            <td>전국어린이보호구역표준데이터.csv</td>
        </tr>
        <tr>
            <td>버스 정류장 데이터</td>
            <td><a href="#">공공데이터포털</a></td>
            <td>국토교통부_전국 버스정류장 위치정보</td>
        </tr>
        <tr>
            <td>부문별 교통사고 현황</td>
            <td><a href="#">TAAS</a></td>
            <td>16~21년도 교통사고 유형별 현황</td>
        </tr>
        <tr>
            <td>이륜차 사고 데이터</td>
            <td><a href="#">TAAS</a></td>
            <td>19~21년도 가해차종-이륜차 또는 피해차종-이륜차 사고 정보</td>
        </tr>
        <tr>
            <td>이륜차 데이터</td>
            <td><a href="#">KOSIS</a></td>
            <td>이륜차신고현황_시도별</td>
        </tr>
        <tr>
            <td>인구 데이터</td>
            <td><a href="#">KOSIS</a></td>
            <td>행정구역(시군구)별 인구수</td>
        </tr>
    </tbody>
</table>

</body>
</html>

<br>

> ## 5. 최적 모델 선정

<body>
<table>
    <thead>
        <tr>
            <th class="diagonal-header" rowspan="2">평가지표</th>
            <th colspan="4">모델</th>
        </tr>
        <tr>
            <th>Random Forest</th>
            <th>LGBM</th>
            <th>XGB</th>
            <th class="catboost">CatBoost</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>RMSE_test</td>
            <td>27.15</td>
            <td>27.08</td>
            <td>28.02</td>
            <td class="catboost">26.89</td>
        </tr>
        <tr>
            <td>RMSLE_test</td>
            <td>0.35</td>
            <td>0.36</td>
            <td>0.36</td>
            <td class="catboost">0.34</td>
        </tr>
    </tbody>
</table>

</body>
</html>


### RMSE가 가장 낮고 RMSLE가 두번째로 낮은 `CatBoost` 모델 선정
- CatBoost 최적 파라미터 : 'depth': 3, 'iterations': 100, 'learning_rate': 0.1, 'subsample': 1

    - <b> Under Estimation에 더 큰 패널티를 부여하는 RMSLE 평가 지표도 고려
    - RMSE는 실제 값 20이고 예측 값이 10 혹은 30인 경우에 같은 평가 지표 값을 가지지만, 
    - RMSLE는 실제 값 보다 더 낮게 예측한 경우가 더 높은 RMSLE(더 높은 패널티)를 가한다. 
    - 이륜차 위험도 예측 모델은 실제 값을 더 낮게 예측하는 것이 더 치명적이다. </b>

<br>

> ## 6. 모델 결과 해석
<img width="1000" alt="Image" src="https://github.com/user-attachments/assets/439631c6-b59e-4b61-8b88-03328633579e" />

<br>

<img width="1000" alt="Image" src="https://github.com/user-attachments/assets/5c45097c-b7a4-40a6-b4af-8c069c8b9e39" />

### 단속 카메라가 많은 지역에서 이륜차의 EPDO를 억제하지 못하고 있음


> ## 7. 정책적 제언
<img width="700" alt="Image" src="https://github.com/user-attachments/assets/888ebd2d-6af1-4576-99e9-7a375e67b2bc" />

### 이륜차는 후면 번호판만 부착되어 있는 특성상 <br> 이륜차의 신호, 속도 위반은 일반 무인 단속 카메라 적발이 어려움

### -> 이에 후면을 단속할 수 있는 CCTV 설치가 필요하다고 판단됨

