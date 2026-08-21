# 인증했무아? 시작 안내

아래 순서대로 딱 한 번만 설정하면 됩니다.

## 1. GitHub 저장소 만들기

1. https://github.com 접속 후 로그인
2. 오른쪽 위 `+` → `New repository`
3. 이름에 `moare-auth` 입력 → `Create repository`
4. 저장소 화면에서 `Add file` → `Upload files`
5. 이 폴더의 파일 5개를 모두 끌어다 놓기
6. 아래 `Commit changes` 클릭

## 2. 웹사이트 공개하기

1. 저장소의 `Settings` 클릭
2. 왼쪽 `Pages` 클릭
3. `Deploy from a branch` 선택
4. Branch를 `main`, 폴더를 `/ (root)`로 선택
5. `Save` 클릭

잠시 후 `https://내아이디.github.io/moare-auth/` 주소가 생깁니다.

## 3. Firebase 만들기

1. https://console.firebase.google.com 접속
2. `Create a project` 클릭
3. 프로젝트 이름 입력
4. 프로젝트 화면에서 웹 아이콘 `</>` 클릭
5. 앱 이름 입력 → `Register app`
6. 화면의 `firebaseConfig` 값을 복사
7. `firebase-config.js` 파일의 `PASTE_...` 부분을 복사한 값으로 교체
8. 수정한 파일을 GitHub에 다시 업로드

## 4. Google 로그인 켜기

Firebase에서 `Build → Authentication → Get started → Sign-in method → Google → Enable → Save`를 누릅니다.

그리고 `Authentication → Settings → Authorized domains`에 아래 주소를 추가합니다.

```text
내아이디.github.io
```

## 5. 확인

GitHub Pages 주소를 열고 `Google로 계속하기`를 눌러 로그인합니다.

네이버 로그인은 별도 네이버 개발자 앱과 Firebase OIDC 설정이 필요하므로 Google 로그인부터 확인하는 것을 권장합니다.

## 제가 이어서 해드릴 수 있는 것

Firebase 설정값을 아래 형식으로 보내주면 코드에 연결해드릴 수 있습니다. 이 값에는 비밀번호가 포함되지 않습니다.

```js
{
  apiKey: "...",
  authDomain: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "..."
}
```

GitHub 비밀번호, 네이버 Client Secret, Firebase 서비스 계정 키는 보내지 마세요.
