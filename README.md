# td-gtm-test-page

AE Operation GTM 템플릿을 실제 페이지에서 E2E 검증하고, 고객에게 배포하기 전에 동작을 확인하기 위한 **공개 테스트 페이지**.

**배포 URL**: https://wo123kr.github.io/td-gtm-test-page/

## 사용 방법

### 1. 본인 GTM 컨테이너 ID로 교체

`index.html` 을 fork 후 **두 곳**의 `GTM-W2BDBW4Q` 를 본인 컨테이너 ID로 교체:

```html
})(window,document,'script','dataLayer','GTM-W2BDBW4Q');  // ← 여기

<iframe src="https://www.googletagmanager.com/ns.html?id=GTM-W2BDBW4Q" ...>  // ← 여기
```

### 2. 분석 SDK (`ta`) App ID 설정

URL 쿼리 파라미터로 전달:

```
https://wo123kr.github.io/td-gtm-test-page/?appId=YOUR_APP_ID
```

필요 시 `serverUrl`도 지정:

```
?appId=YOUR_APP_ID&serverUrl=https://custom.server.url/sync_js
```

### 3. GTM에서 AE Operation 템플릿 Import

1. https://github.com/wo123kr/td-mcp/blob/main/gtm/ 에서 `TE Operation_KR.tpl` 다운로드
2. GTM → Templates → Tag Templates → New → ⋮ → Import

### 4. 태그 생성

1. GTM → Tags → New → Tag Configuration → **AE Operation** 선택
2. 태그 타입: **🚀 운영 초기화 (opsInit)**
3. App ID, Server URL 입력
4. Trigger: `Consent Initialization - All Pages`
5. Save

### 5. Preview 모드에서 이 페이지 테스트

GTM Preview → 이 URL 입력 → Connect → 페이지에서 각 tagType 버튼 클릭

## 테스트 항목

| 섹션 | 검증 내용 |
|---|---|
| 1. 환경 상태 | GTM 설치 / 분석 SDK 초기화 / 운영 SDK 4종(TDApp·TDRemoteConfig·TDStrategy·thinkingdata) 로드 |
| 2. Custom Event 발화 | 9개 tagType별 `dataLayer.push` → GTM 트리거 연결 동작 |
| 3. triggerListener 수신 | TE 운영 백엔드에서 클라이언트 채널 테스트 발송 → `td_ops_trigger` 이벤트 수신 |
| 4. 콘솔 검증 스크립트 | 콘솔에서 각 SDK API 직접 호출 |
| 5. 네트워크 검증 | `sync_js` 중복 전송 여부 — autoTrack off 설계 검증 |

## 관련 레포

- **GTM 템플릿 본체**: https://github.com/wo123kr/td-mcp (`gtm/TE Operation_*.tpl`)
- **CDN 미러**: https://github.com/wo123kr/td-gtm-sdk (`@v1.3.0`)

## 라이선스

Test 페이지 자체는 MIT. GTM 템플릿과 SDK는 각자의 라이선스를 따름.
