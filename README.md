# 마음 기록 — 감정 일기

오늘의 감정과 생각을 남기고, Supabase에 저장된 일기를 여러 기기에서 확인하는 반응형 웹앱입니다. 감정을 선택해 일기를 작성하고 삭제하거나 감정별로 모아볼 수 있습니다. 일기 목록은 페이지를 열 때 조회하며, 작성·삭제 후 다시 불러옵니다. Realtime 구독은 사용하지 않습니다.

## 실행

1. Supabase 프로젝트에 `public.diaries` 테이블과 `anon` 역할의 select/insert/delete 권한 및 RLS 정책을 준비합니다. 테이블은 `id`, `content`, `emotion`, `created_at` 컬럼을 사용합니다.
2. `.env.example`을 참고해 `.env.local`을 만들고 Supabase URL과 Publishable Key를 설정합니다.
3. 의존성을 설치하고 개발 서버를 실행합니다.

```sh
npm install
npm run dev
```

코드 검사는 `npm run lint`, 배포용 빌드는 `npm run build`로 실행합니다.

## 데이터와 보안

일기는 브라우저의 로컬 저장소가 아닌 Supabase `diaries` 테이블에 저장됩니다. 따라서 같은 Supabase 프로젝트를 사용하는 다른 기기와 브라우저에서도 조회할 수 있습니다.

이 앱은 로그인 없이 `anon` 권한을 사용합니다. 현재 실습 정책이 모든 익명 사용자에게 읽기·추가·삭제를 허용한다면, 일기와 삭제 권한도 모든 방문자에게 공유됩니다. Supabase Publishable Key는 브라우저에 전달되므로 비밀 키로 취급하면 안 됩니다. 실제 사용 전에는 인증, 사용자별 RLS 정책, 권한 범위를 별도로 설계하세요. 환경 변수 파일은 저장소에 커밋하지 마세요.
