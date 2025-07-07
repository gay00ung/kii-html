
# 🎯 얼굴인식 통합 분석 대시보드

CSV로 저장된 Liveness, Matching, Sensor 데이터를 통합하여 시각적으로 분석할 수 있는 웹 기반 대시보드입니다. 사용자는 CSV 파일을 업로드하고, 분석 버튼을 클릭하면 자동으로 통계, 최적 조건, 성공률 차트 등을 확인할 수 있습니다.

---

## 📁 기능 요약

- ✅ **CSV 다중 업로드 및 병합 분석**
- ✅ **Liveness / Matching / Sensor 데이터 자동 파싱**
- ✅ **성공률 및 완전 성공률 계산**
- ✅ **조도, 얼굴 방향 등 최적 조건 추출**
- ✅ **Chart.js 기반 인터랙티브 차트**
- ✅ **파일별 통계 및 시각화**

---

## 📂 파일 구조

```text
index.html         # 대시보드 메인 HTML + CSS + JS 포함
```

> *All-in-One 구조로 하나의 HTML 파일 안에 모든 로직 포함.*

---

## ⚙️ 사용법

1. 브라우저에서 `index.html`을 엽니다.
2. Liveness, Matching, Sensor 데이터를 포함한 CSV 파일들을 선택합니다.
3. `📊 분석 시작` 버튼을 클릭하면 분석이 진행됩니다.
4. 성공률, 최적 인증 조건, 다양한 차트가 자동 생성됩니다.

---

## 🧪 CSV 형식 예시

각 CSV 파일은 아래와 같이 구분된 섹션을 포함해야 합니다:

```
Table: Liveness History
ID,Result,Score
123,1,99.4
...

Table: Matching History
ID,Result,Score,Threshold Score,Message
123,1,4105,4100,"Success"
...

Table: Sensor Data
ID,Euler Angles (X,Y,Z),Ambient Light
123,"0.2,-1.1,5.5",140.3
```

> `Table:` 구분자 기준으로 자동 분할 및 파싱됩니다.

---

## 📊 통계 분석 로직

### ✅ 병합 기준

- `ID`를 기준으로 `liveness`, `matching`, `sensor` 데이터를 병합

### ✅ 통계 항목

| 항목 | 설명 |
|------|------|
| 전체 시도 횟수 | 병합된 고유 ID 개수 |
| Liveness 성공률 | Liveness result가 1인 비율 |
| Matching 성공률 | Matching result가 1인 비율 |
| 완전 성공률 | Liveness + Matching 모두 성공한 비율 |

### ✅ 최적 인증 조건 계산

- **조도 (Ambient Light)**: 성공 케이스의 1사분위수 ~ 3사분위수 범위
- **Euler 각도 (Pitch, Yaw, Roll)**: 절댓값 기준 75% 분위수 → 권장 최대 범위 `±x°`

---

## 📈 시각화 구성 (Chart.js 사용)

1. **조명별 성공률**  
   - 조도를 구간별로 나누어 liveness / matching 성공률 시각화 (막대 차트)

2. **얼굴 방향 분포**  
   - Euler Yaw vs Pitch 산점도  
   - 성공과 실패 구분하여 시각화

3. **매칭 점수 분포**  
   - 매칭 성공/실패 별 평균 점수 비교  
   - 기준 임계값 (threshold) 표시선 포함

4. **센서 상관관계 분석**  
   - 조도 vs 정면응시 점수 (얼굴 방향 편차 기반 추정) 버블 차트

---

## 🧠 주요 로직 함수

| 함수명 | 설명 |
|--------|------|
| `finalizeAnalysis()` | 전체 분석 시작 지점. 병합, 분석, 차트 호출 |
| `mergeAndAnalyze()` | liveness/matching/sensor 데이터 병합 |
| `calculateStatistics()` | 성공률 계산 및 표시 |
| `calculateOptimalConditions()` | 성공 사례 기반 최적 조도/각도 계산 |
| `drawCharts()` | 모든 시각화 차트 생성 |

---

## 🔗 외부 라이브러리

| 라이브러리 | 용도 |
|------------|------|
| [Chart.js](https://www.chartjs.org/) | 데이터 시각화 차트 |
| [PapaParse](https://www.papaparse.com/) | CSV 파싱 |

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.2/papaparse.min.js"></script>
```

---

## 🎨 디자인 요소

- **CSS 그라디언트와 카드형 디자인**
- **로딩 스피너 애니메이션**
- **반응형 그리드 레이아웃**
- **hover 애니메이션 및 버튼 효과**

---


## 📜 라이선스

MIT License
