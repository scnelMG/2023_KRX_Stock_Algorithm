# 공개 안전성 검토

## 현재 공개 저장소 기준

KRX 대회 원본 데이터와 생성 제출 CSV는 현재 공개 트리에서 제외합니다.

제외 대상:

- `data/train.csv`
- `data/X_1st_year.csv`
- `data/sample_submission.csv`
- `data/fundamentals_snapshot.csv`
- `data/test_sample_submission.csv`
- `data/try_submission.csv`
- `data/try_final_2_submission.csv`
- `try_final_3_submission.csv`

## 근거

Notion에 남은 대회 데이터 이용 조건은 이용 목적 달성 후 제공 자료를 파기하도록 명시합니다. 이 저장소의 MIT 라이선스는 원본 코드와 문서에만 적용되며, 대회 데이터·제출 산출물·외부 시장 데이터에 대한 재배포 권한을 부여하지 않습니다.

## 과거 Git 객체

공개 브랜치와 현재 의도된 이력에서는 데이터 파일을 제거했습니다. 다만 GitHub API에서 과거 SHA `3766b565d504faf5a1f3c98198d97058f31ad15c`가 캐시 객체로 접근될 수 있습니다. 완전한 인프라 삭제는 GitHub Support만 처리할 수 있으며, 요청 초안은 [여기](github-support-purge-request.md)에 있습니다.
