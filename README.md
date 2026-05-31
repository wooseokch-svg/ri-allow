# realtime-interpreter 허용 스위치 (allow.json)

`RealtimeInterpreter.exe` 가 시작 시 이 `allow.json` 을 확인합니다.

- `enabled: false` → **모든 사본 즉시 정지 (킬 스위치)**
- `allowed: []` (비움) → enabled 만으로 통제 (활성 시 모든 PC 허용)
- `allowed: ["<머신ID>", ...]` → **그 PC들만 허용** (머신ID = `RealtimeInterpreter.exe id` 로 확인)

편집(커밋) 후 약 5분(GitHub CDN 캐시) 내 반영. 인터넷 끊기면 마지막 상태로 24시간 유예.
