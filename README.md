# 2023 KRX Stock Algorithm

> 2023 제2회 KRX 주식 투자 알고리즘 경진대회에서 종목별 가격·재무 피처로 Long–Short 순위 제출 파일을 만든 금융 시계열 프로젝트입니다.

## 결과

| 항목 | 내용 |
| --- | --- |
| 대회 | 2023 제2회 KRX 주식 투자 알고리즘 경진대회 |
| 최종 결과 | 121위 / 1,323팀 |
| 리더보드 점수 | 0.133529 |
| 팀 | 이게뭐시당 |
| 팀원 | 이성 · 벌꿀오소리맨 · 푸바오의대나무 |
| 공식 기록 | [DACON 리더보드](https://dacon.io/competitions/official/236117/leaderboard) |

> 리더보드 점수는 대회가 계산한 결과입니다. 보관된 기록에는 모델 선택을 위한 독립 검증 RMSE·샤프 지수 비교표가 없으므로, 이 저장소는 해당 수치를 주장하지 않습니다.

## 내 역할

보관된 Git 커밋과 노트북을 기준으로, 박민규는 제출 파이프라인의 다음 구현을
작성·정리했습니다.

- 종목별 ARIMA 기준선을 구현한 [`[Baseline]_ARIMA.ipynb`]([Baseline]_ARIMA.ipynb)
- OHLCV·PER·PBR·군집 feature를 window로 구성하고 기대수익률 순위를 만드는
  [`window_slicing.ipynb`](window_slicing.ipynb)
- 제출 형식 점검과 최종 제출 파일 생성 흐름

팀 전체의 모델 선택 근거나 독립 검증 수치는 보관된 자료만으로 확정할 수 없어,
이 저장소에서는 개인 구현 범위를 위 코드와 커밋 이력으로 제한해 설명합니다.

## 문제 정의

2,000개 종목의 순위를 산출해 상위 200개에는 Long, 하위 200개에는 Short 전략을 적용하는 대회였습니다. 예측 시점 이후 15거래일의 Long–Short 성과를 기준으로 평가됐습니다.

이 프로젝트는 다음 흐름을 구현했습니다.

1. 종목별 OHLCV 시계열과 PER·PBR, 군집 피처를 결합합니다.
2. 최근 3거래일을 하나의 feature window로 펼칩니다.
3. 종목별 선형 회귀로 1일·15일 뒤 종가를 각각 예측합니다.
4. 두 예측값의 기대수익률을 내림차순으로 정렬해 제출 순위를 만듭니다.

평가 규칙과 당시 의사결정의 근거는 [포트폴리오 근거 정리](docs/portfolio-evidence.md)에서 분리해 확인할 수 있습니다.

## 구현 구성

```text
.
|-- [Baseline]_ARIMA.ipynb       # 종목별 ARIMA(2, 1, 2) 기준선
|-- window_slicing.ipynb         # 순차 실행 가능한 최종 제출 파이프라인
|-- scratch/
|   `-- random_rank_scratch.ipynb # 제출 규격 확인용 비포트폴리오 실험
|-- docs/
|   |-- portfolio-evidence.md    # Notion·Drive·코드 기반 사실 정리
|   |-- validation-protocol.md   # 대회 규칙과 향후 검증 방법
|   |-- reproducibility.md       # 재현 가능한 범위와 제한
`-- data/README.md               # 비공개·파기 대상 데이터 경계
```

## 실행 전제

대회 원본 데이터와 제출 산출물은 공개 저장소에 포함하지 않습니다. 대회 규정의 데이터 이용 조건을 확인한 뒤, 보유가 허용되는 경우에만 아래 파일을 로컬 `data/`에 준비하세요.

```text
data/train.csv
data/X_1st_year.csv
data/sample_submission.csv
data/fundamentals_snapshot.csv
```

`fundamentals_snapshot.csv`에는 `일자`, `종목코드`, `PER`, `PBR` 컬럼이 필요합니다. 원래 구현의 실시간 `pykrx` 조회 대신 시점이 고정된 로컬 스냅샷을 사용해, 외부 데이터 갱신이 feature를 바꾸는 문제를 드러내고 통제합니다.

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

권장 순서:

1. `[Baseline]_ARIMA.ipynb`로 기준선 구조 확인
2. `window_slicing.ipynb`를 위에서 아래로 실행
3. 생성된 `try_final_3_submission.csv`의 컬럼과 순위 유일성 확인

## 공개 범위와 한계

- 이 저장소는 **역사적 경진대회 구현 기록**입니다. 비공개 대회 데이터와 외부 시장 데이터 때문에 같은 점수 재현을 보장하지 않습니다.
- 공개: 코드, 재현 절차, 대회 규칙에 저촉되지 않는 문서
- 제외: NH 원천 데이터·제출 파일·제한 자료·비밀값
- 실제 서비스 화면 또는 발표 자료가 보관돼 있지 않아, 생성 이미지나 오류가 섞인 차트를 넣지 않았습니다.

세부 내용은 [모델링 메모](docs/modeling-notes.md), [검증 프로토콜](docs/validation-protocol.md), [재현성 메모](docs/reproducibility.md), [데이터 공개 기준](data/README.md)을 참고하세요.

## 민감 데이터 정리

대회 제공 원본 데이터와 제출 산출물은 저장소의 전체 Git 히스토리와 연결된 포크 참조에서 제거했으며, GitHub Support의 서버 측 가비지 컬렉션 및 캐시 정리까지 완료했습니다.

이 저장소에는 재현에 필요한 코드와 비민감 문서만 보관합니다. 대회 데이터나 생성된 제출 파일을 새 커밋에 추가하지 마세요. 데이터의 이용·보관 조건은 [데이터 공개 기준](data/README.md)을 따릅니다.

## 개선 포인트

후속 실험을 수행할 수 있는 권한 있는 데이터가 생긴다면, 시점 고정 스냅샷과 walk-forward validation을 사용해 ARIMA·선형 회귀·다른 후보 모델을 같은 기간에서 비교하고, 대회 규칙에 맞는 Sharpe 지수와 거래비용 민감도를 기록하는 것이 다음 단계입니다.

## 이용 안내

이 저장소는 포트폴리오·학습 기록 열람을 위해 공개합니다. 코드·문서·이미지의 재사용, 수정, 배포는 사전 문의가 필요합니다.
