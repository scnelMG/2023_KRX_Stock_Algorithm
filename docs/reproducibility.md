# 재현성 메모

## 재현 가능한 범위

이 저장소는 Python 3.9.x와 `requirements.txt`의 고정된 직접 의존성을 기준으로 작성했습니다. `window_slicing.ipynb`는 필요한 파일을 먼저 확인하고, 모든 셀을 위에서 아래로 실행할 수 있도록 정리돼 있습니다.

## 재현할 수 없는 범위

동일한 리더보드 결과를 재현한다고 주장할 수는 없습니다.

- 대회 원본 데이터와 생성 제출물은 공개 저장소에 포함하지 않습니다.
- Notion에 보관된 대회 데이터 이용 조건은 목적 달성 후 파기를 요구합니다. 데이터 보유 권한이 없는 경우 실행하면 안 됩니다.
- `pykrx` 같은 외부 조회는 시점·네트워크·제공 데이터 변화에 따라 달라질 수 있습니다.
- 과거의 모델 선택 검증 수치가 보존되지 않았습니다.

## 실행 조건

유효한 데이터 이용 권한이 있을 때만 다음 파일을 `data/`에 둡니다.

```text
train.csv
X_1st_year.csv
sample_submission.csv
fundamentals_snapshot.csv
```

`fundamentals_snapshot.csv`는 `일자`, `종목코드`, `PER`, `PBR` 컬럼을 가져야 합니다. 스냅샷의 생성 날짜·출처·해시를 별도 실험 기록에 남겨야 합니다.

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

그 후 `[Baseline]_ARIMA.ipynb`와 `window_slicing.ipynb`를 순서대로 실행합니다.
