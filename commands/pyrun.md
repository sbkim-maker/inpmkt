# /pyrun — Python UTF-8 실행 래퍼

Windows 환경에서 cp949 인코딩 오류 없이 Python 스크립트를 실행합니다.
`PYTHONUTF8=1`과 `-X utf8` 플래그를 자동으로 적용합니다.

## Usage
/pyrun [script] [args...]

## Examples
/pyrun main.py
/pyrun test_api.py
/pyrun ad_setup.py

## Behavior

인수가 없으면 `main.py`를 기본 대상으로 사용합니다.
현재 프로젝트 디렉토리에서 실행합니다.

```bash
PYTHONUTF8=1 python -X utf8 $ARGUMENTS
```
