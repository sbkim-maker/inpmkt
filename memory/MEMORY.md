# MEMORY.md

Claude Code 세션 간 유지되는 핵심 지식 베이스.

---

## Meta Marketing API

### Instagram 소재 생성 — 영상/이미지 공통 파라미터

`source_instagram_media_id`로 Instagram 포스트를 광고 소재로 참조할 때
반드시 `instagram_actor_id`(Instagram 비즈니스 계정 ID)를 **함께** 전달해야 한다.

```python
account.create_ad_creative(
    fields=[AdCreative.Field.id],
    params={
        AdCreative.Field.name:       name,
        "source_instagram_media_id": media_id,
        "instagram_actor_id":        ig_account_id,  # 필수! 없으면 영상에서 1815279 에러
    },
)
```

- 이미지는 없어도 동작할 수 있지만, 영상(Reel/Video)은 반드시 필요
- error_subcode `1815279` = instagram_actor_id 누락 시그널
- 프로젝트: `github.krafton.com/sbkim/meta-ads-bot`

---

## GitHub Enterprise

- Krafton 사내 인스턴스: `github.krafton.com`
- API 엔드포인트: `https://github.krafton.com/api/v3/`
- 저장소 목록: `GET /api/v3/users/{user}/repos` + `Authorization: token {PAT}`
- 공개 GitHub(`api.github.com`)과 URL 형식이 다름

---

## Windows Python 인코딩

Windows에서 Python 실행 시 한글 출력이 깨지거나 `UnicodeEncodeError` 발생 시:

```bash
PYTHONUTF8=1 python -X utf8 script.py
```

- 시스템 환경변수에 `PYTHONUTF8=1` 등록하면 영구 적용
- `/pyrun` 커맨드로 자동화됨

---

## facebook-business SDK Cursor 주의

`get_campaigns()` 등 SDK 메서드는 Cursor 객체 반환 → **한 번만 소비 가능**.
반드시 즉시 `list()`로 변환 후 사용:

```python
campaigns = list(account.get_campaigns(...))  # 먼저 변환
```

---

## 보안 원칙

- AI 채팅(Claude, ChatGPT 등)에 API 키, PAT, 비밀번호 **절대 입력 금지**
- 실수로 입력했다면 즉시 해당 토큰 revoke
- `.env` 파일은 저장소 초기화 시 가장 먼저 `.gitignore`에 등록
- GitHub Secret Scanning: push된 코드에서 토큰 패턴 자동 감지 → 즉시 무효화
