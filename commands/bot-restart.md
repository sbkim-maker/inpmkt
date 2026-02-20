# /bot-restart — Meta Ads Bot 재시작

실행 중인 Meta PPA Ads Bot을 종료하고 재시작합니다.

## Usage
/bot-restart [mode]

- 인수 없음: 백그라운드 재시작 (운영용, 작업 스케줄러)
- `dev`: 전경 실행 (개발/디버그용, 로그 출력)

## Behavior

### 공통 — 기존 프로세스 정리
```bash
schtasks /end /tn "MetaAdsBot" 2>/dev/null || true
taskkill /f /im pythonw.exe 2>/dev/null || true
sleep 3
```

### 운영 모드 (기본)
```bash
schtasks /run /tn "MetaAdsBot"
sleep 5
tasklist | grep pythonw
```

### 개발 모드 (dev)
```bash
cd C:/Users/win10.DESKTOP-60AIITA/projects/meta-ads-bot
PYTHONUTF8=1 python -X utf8 main.py
```

## Notes
- 운영 모드는 `start_bot.vbs`를 통해 창 없이 백그라운드 실행
- `MetaAdsBot` 작업 스케줄러 태스크가 등록되어 있어야 운영 모드 사용 가능
- 봇 경로: `C:/Users/win10.DESKTOP-60AIITA/projects/meta-ads-bot`
