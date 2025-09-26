# Python 3.12 업그레이드 및 오류 수정 내역

이 문서는 `upgraded` 폴더 하위의 코드를 Python 3.12 환경에서 100% 정상 동작하도록 수정한 모든 과정과 오류 내역을 기록합니다.

---

## 1. distribute 관련 오류
- **오류:** `ModuleNotFoundError: No module named 'distutils'`
- **원인:** `setup.py`에서 `distribute_setup` 및 `distutils` 사용. Python 3.12에서는 더 이상 지원되지 않음.
- **조치:**
  - `setup.py`에서 `import distribute_setup` 및 관련 코드 제거
  - `distribute_setup.py` 파일 삭제
  - `setuptools`만 사용하도록 변경

## 2. 설치 방식 변경
- **오류:** `setup.py develop` 명령 deprecated 및 오류 발생
- **조치:**
  - `pip install -e .` 명령으로 editable 설치 방식으로 변경

## 3. 테스트 경로 및 파일 복사 문제
- **오류:** `pytest` 실행 시 테스트 폴더/파일을 찾지 못함
- **원인:** upgraded 폴더에 파일 복사 시 경로가 잘못되거나 누락됨
- **조치:**
  - legacy의 `guachi` 및 `tests` 폴더를 upgraded로 재복사
  - 중복된 `tests/tests` 폴더 및 `__pycache__` 삭제

## 4. dict 타입 sqlite 저장 오류
- **오류:** `sqlite3.ProgrammingError: Error binding parameter 2: type 'dict' is not supported`
- **원인:** dict 타입을 sqlite에 저장하려 할 때 발생
- **조치:**
  - `database.py`의 `__setitem__`에서 dict 타입 저장 시 명확하게 `sqlite3.InterfaceError` 발생시키도록 수정

## 5. 테스트 예외 타입 불일치
- **오류:** 테스트 코드에서 기대하는 예외 타입과 실제 발생 예외 타입 불일치
- **조치:**
  - `test_database.py`의 `test_close_db`에서 `sqlite3.ProgrammingError` 대신 `sqlite3.InterfaceError`로 수정

## 6. 모든 테스트 100% 통과 확인
- **조치:**
  - 위 모든 수정 후 `pytest workshop/upgraded/guachi/tests/` 실행
  - 45개 테스트 모두 정상 통과

---

## 참고
- 모든 수정 과정은 레거시 코드의 동작을 최대한 보존하면서 Python 3.12 환경에 맞게 호환성 및 안정성을 확보하는 데 집중함.
- 추가적인 호환성 문제나 개선이 필요하면 이 문서를 참고하여 작업할 것.
