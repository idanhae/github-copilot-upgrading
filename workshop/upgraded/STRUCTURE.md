# upgraded 폴더 파일 구조 설명

`upgraded` 폴더는 `legacy` 폴더의 전체 파일 및 디렉터리 구조를 그대로 복사한 폴더입니다.

## 최상위 파일 및 폴더
- MANIFEST.in
- README.rst
- distribute-0.6.10.tar.gz
- distribute_setup.py
- setup.py
- docs/ (문서 관련 폴더)
- guachi/ (파이썬 모듈 폴더)
- guachi.egg-info/ (패키지 정보 폴더)

## docs/
- Makefile
- build/
  - doctrees/
  - html/
    - .buildinfo
    - _sources/
    - _static/
    - changelog.html
    - example_usage.html
    - genindex.html
    - getting_started.html
    - index.html
    - objects.inv
    - other_uses.html
    - search.html
    - searchindex.js
- source/
  - _static/
  - changelog.rst
  - conf.py
  - example_usage.rst
  - getting_started.rst
  - index.rst
  - other_uses.rst

## guachi/
- __init__.py
- config.py
- database.py
- tests/
  - test_configmapper.py
  - test_configurations.py
  - test_database.py
  - test_integration.py

## guachi.egg-info/
- PKG-INFO
- SOURCES.txt
- dependency_links.txt
- top_level.txt

각 파일 및 폴더는 Python 패키지, 문서, 테스트, 배포 관련 파일로 구성되어 있습니다.