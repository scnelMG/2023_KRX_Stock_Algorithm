# 2023 KRX Stock Algorithm

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Finance](https://img.shields.io/badge/Finance-Stock%20Algorithm-0F766E)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![Time Series](https://img.shields.io/badge/Time%20Series-ARIMA%20%7C%20Windowing-2563EB)
![Portfolio](https://img.shields.io/badge/Portfolio-Financial%20Data-111827)

> 2023 제2회 KRX 주식 투자 알고리즘 경진대회에서 주가 시계열 데이터를 활용해 예측 제출 파일을 생성한 금융 데이터 분석 프로젝트입니다.

## 프로젝트 개요

| 항목 | 내용 |
| --- | --- |
| 대회 | 2023 제2회 KRX 주식 투자 알고리즘 경진대회 |
| 대회 링크 | [DACON 리더보드](https://dacon.io/competitions/official/236117/leaderboard) |
| 도메인 | 금융 데이터, 주식 시계열 |
| 문제 유형 | 종목별 시계열 예측 및 제출 파일 생성 |
| 주요 접근 | ARIMA baseline, window slicing, feature window 구성 |
| 핵심 산출물 | 예측 노트북, 제출 CSV, 데이터 공개 경계 문서 |

## 문제 정의

주식 예측 프로젝트는 모델 복잡도보다 **데이터를 시간 순서에 맞게 다루는 방식**이 중요합니다. 미래 정보를 학습에 섞으면 리더보드 성능은 좋아 보여도 실제 운용 관점에서는 의미가 없어집니다.

이 저장소는 경진대회 당시 실험을 바탕으로 다음 질문을 다뤘습니다.

- 과거 가격 구간을 어떤 window로 잘라 예측 입력으로 만들 것인가?
- 단순 baseline과 window 기반 접근의 차이를 어떻게 비교할 것인가?
- 제출 파일 형식을 안정적으로 생성하기 위해 어떤 후처리 흐름이 필요한가?

## 접근 방식

### 1. Baseline 확인

`[Baseline]_ARIMA.ipynb`에서 전통적인 시계열 baseline을 확인했습니다. baseline은 복잡한 모델보다 먼저 데이터 구조와 예측 대상의 형태를 이해하기 위한 기준점 역할을 했습니다.

### 2. Window Slicing

`window_slicing.ipynb`에서 과거 구간을 고정 길이 window로 변환해 모델 입력 형태를 만들었습니다. 금융 시계열에서는 임의 shuffle보다 시간 순서 보존이 중요하므로, window 생성 기준과 제출 대상 기간을 분리하는 데 중점을 뒀습니다.

### 3. 제출 파일 생성

`sample_submission.csv` 형식에 맞춰 예측 결과를 `try_submission.csv`, `try_final_2_submission.csv`, `try_final_3_submission.csv`로 정리했습니다. 제출 파일은 모델 결과 자체보다 대회 형식과 컬럼 정합성을 확인하는 산출물입니다.

## 저장소 구성

```text
.
|-- README.md
|-- [Baseline]_ARIMA.ipynb
|-- window_slicing.ipynb
|-- test.ipynb
|-- try_final_3_submission.csv
|-- docs/
|   `-- reproducibility.md
`-- data/
    `-- README.md
```

## 실행 방법

```bash
pip install pandas numpy scikit-learn statsmodels jupyter
jupyter notebook
```

권장 확인 순서:

1. `[Baseline]_ARIMA.ipynb`
2. `window_slicing.ipynb`
3. 제출 CSV 형식 확인

## 데이터 공개 기준

대회 원본 데이터와 제출 산출물은 재배포 조건이 명확하지 않을 수 있어 공개 저장소에 포함하지 않았습니다. 따라서 이 저장소는 노트북, 실행 방법, 재현 가능성 문서를 중심으로 분석 흐름을 설명합니다.

자세한 기준은 [data/README.md](data/README.md)와 [docs/public-safety.md](docs/public-safety.md)를 참고하세요.

## 이 프로젝트에서 다룬 역량

- 금융 시계열 데이터의 시간 순서와 검증 경계를 고려한 실험 경험
- baseline부터 제출 파일 생성까지 이어지는 경진대회 파이프라인 이해
- 공개 가능한 설명과 재배포가 불명확한 데이터의 경계 구분
- 데이터 처리, 검증, 산출물 관리 경험

## 한계와 개선 방향

- 원본 대회 데이터의 재배포 가능성이 명확하지 않아 완전 공개형 재현성은 제한됩니다.
- 노트북 중심 구조라 실무형 파이프라인으로 보려면 `src/` 모듈화가 필요합니다.
- 후속 개선 시 walk-forward validation, transaction cost, risk-adjusted return 지표를 추가하면 금융 도메인 완성도가 높아집니다.
