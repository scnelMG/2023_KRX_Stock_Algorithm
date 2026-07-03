# 공개 안전성 검토

## 현재 공개 저장소 기준

KRX 대회 원본 데이터와 제출 CSV는 GitHub 공개 브랜치에서 제외합니다.

제외 대상:

- `data/train.csv`
- `data/X_1st_year.csv`
- `data/sample_submission.csv`
- `data/test_sample_submission.csv`
- `data/try_submission.csv`
- `data/try_final_2_submission.csv`
- `try_final_3_submission.csv`

## 제외 이유

금융 시계열 대회 데이터와 제출 파일은 재배포 가능 여부가 명확하지 않을 수 있습니다. 포트폴리오에서는 원본 데이터 자체보다 시계열 window 구성, baseline 비교, 제출 흐름을 설명하는 문서를 평가 대상으로 둡니다.

## 재현 안내

노트북을 재실행하려면 대회에서 제공한 데이터를 로컬에 별도로 배치해야 합니다. 공개 저장소는 README, 노트북, 재현 가능성 메모를 통해 실험 구조를 설명합니다.
