# 인증했무아? (Moiré Authentication Prototype)

개인별 줄무늬 간격을 가진 실물 무아레 카드를 이용하는 2차 인증 웹 프로토타입입니다. 정적 사이트라서 GitHub Pages에 바로 배포되며, 현재는 즉시 시연 가능한 로컬 데모 인증을 포함합니다.

## 실행과 배포

이 폴더에서 `index.html`을 브라우저로 열거나 VS Code Live Server를 사용하세요. GitHub 저장소에 올린 뒤 **Settings → Pages → Deploy from a branch → main / root**를 선택하면 배포됩니다.

데모 계정은 `student@moa.test` / `moa2026!` 입니다. **카드 발급받기**로 만든 계정은 이 브라우저의 Local Storage에만 저장됩니다.

## 실제 인증으로 전환하기

GitHub Pages에는 서버 비밀값을 넣을 수 없습니다. 실제 사용자 인증에는 Supabase를 연결해야 합니다.

1. Supabase 프로젝트를 만들고 Email/Password 인증을 활성화합니다.
2. `cards` 테이블에 `user_id`, `card_id`, `stripe_spacing`, `card_secret`을 둡니다. `card_secret`은 서버(Edge Function)에서만 접근합니다.
3. Edge Function이 로그인 후 6자리 임시 코드, 만료 시각(60초), 시도 횟수를 `challenges` 테이블에 저장하고, 화면용 무아레 데이터만 돌려줍니다.
4. 코드 검증도 같은 Edge Function에서 합니다. 브라우저에는 정답이나 카드 비밀값을 보내지 않습니다.

> 현재 데모의 코드는 브라우저에 있으므로 보안 용도로 사용할 수 없습니다. 전시·발표용이며, 실제 서비스에서는 반드시 위 서버 검증 구조로 교체해야 합니다.

## Firebase 소셜 로그인 설정

1. Firebase 프로젝트를 만들고 Web 앱을 추가합니다.
2. Authentication → Sign-in method에서 Google을 활성화합니다.
3. `outputs/firebase-config.js`에 Firebase Web 앱 설정값을 붙여 넣습니다.
4. Authentication → Settings → Authorized domains에 GitHub Pages 도메인(예: `아이디.github.io`)을 추가합니다.
5. 네이버는 Firebase Authentication with Identity Platform을 활성화한 뒤 OIDC 공급자로 등록하고 provider ID를 `oidc.naver`로 설정합니다. 네이버 Client ID/Secret과 redirect URI는 Firebase Console에서 발급·등록합니다.

Google 버튼은 Firebase의 `signInWithPopup`을 사용합니다. 네이버 버튼은 Firebase OIDC provider(`oidc.naver`)를 사용하므로, 네이버 설정 전에는 안내 메시지가 표시됩니다.

## 인쇄 카드 규격

일반 신용카드 크기: **85.60 × 53.98 mm (ISO/IEC 7810 ID-1)**. 실제 인쇄 전에는 모니터 배율과 인쇄 오차를 위한 기준 마커 및 사용자별 보정 단계를 추가하세요.

## 관리자 화면 (프로토타입)

상단의 `관리자`를 누르고 데모 비밀번호 `admin2026!`을 입력하면 사용자 카드 ID·고유 간격을 확인하고 인쇄용 카드 창을 열 수 있습니다. 현재 목록은 브라우저 Local Storage를 읽습니다. 실제 운영에서는 Firebase Auth Custom Claims와 Firestore Security Rules로 관리자 권한을 보호해야 합니다.

관리자 목록의 `투명 필름 인쇄` 버튼은 카드 배경을 투명으로 만든 뒤 브라우저의 기본 인쇄 대화상자를 호출합니다. 인쇄 설정에서 실제 투명 필름 용지를 선택하고 `배경 그래픽`은 끄는 것을 권장합니다.

\n\n<!-- pages refresh -->
