---
name: sonner-toast
description: React 애플리케이션에서 sonner 라이브러리를 사용해 세련된 토스트(팝업) 알림을 표시하는 스킬
version: "2.0.8"
source: https://github.com/emilkowalski/sonner
tags:
  - react
  - toast
  - ui
  - notification
---

# 스킬: sonner 토스트 알림 사용법

> **출처:** https://github.com/emilkowalski/sonner  
> **버전:** 2.0.8  
> **용도:** React 애플리케이션에서 세련된 토스트(팝업) 알림 표시

---

## 개요

**sonner**는 React용 간결하고 세련된 토스트 알림 컴포넌트입니다.  
설치가 간단하고, 다양한 알림 유형(성공, 오류, 경고, 로딩 등)을 지원합니다.

---

## 설치

```bash
npm install sonner
```

---

## 기본 사용법

### 1. 레이아웃에 `<Toaster>` 추가

```jsx
// app/layout.jsx (Next.js) 또는 루트 컴포넌트
import { Toaster } from 'sonner';

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {children}
        <Toaster />
      </body>
    </html>
  );
}
```

### 2. 토스트 호출

```jsx
import { toast } from 'sonner';

// 기본 알림
toast('메시지가 전송되었습니다.');

// 성공
toast.success('예약이 완료되었습니다!');

// 오류
toast.error('연결에 실패했습니다.');

// 경고
toast.warning('잔여 좌석이 5석 미만입니다.');

// 정보
toast.info('새로운 상품이 등록되었습니다.');

// 로딩 → 완료 전환
const id = toast.loading('처리 중...');
// 작업 완료 후
toast.success('완료!', { id });
```

---

## 주요 옵션

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `position` | 위치 (`top-right`, `bottom-center` 등) | `bottom-right` |
| `duration` | 표시 시간 (ms) | `4000` |
| `richColors` | 색상 강조 활성화 | `false` |
| `closeButton` | 닫기 버튼 표시 | `false` |
| `theme` | 테마 (`light`, `dark`, `system`) | `light` |

### 예시

```jsx
<Toaster
  position="top-center"
  richColors
  closeButton
  duration={3000}
  theme="system"
/>
```

---

## 액션 버튼 포함 토스트

```jsx
toast('예약을 취소하시겠습니까?', {
  action: {
    label: '취소',
    onClick: () => cancelBooking(),
  },
  cancel: {
    label: '닫기',
    onClick: () => {},
  },
});
```

---

## Promise 처리

```jsx
toast.promise(fetchBookingData(), {
  loading: '예약 정보를 불러오는 중...',
  success: '예약 정보 로드 완료!',
  error: '예약 정보를 불러오지 못했습니다.',
});
```

---

## (주)서진항공 · (주)서진월드투어 활용 예시

```jsx
// 예약 완료 알림
toast.success('예약이 확정되었습니다! 이메일을 확인해 주세요.', {
  duration: 5000,
});

// 비자 처리 진행 중
const id = toast.loading('무사증 비자 신청 처리 중...');
await processVisa();
toast.success('비자 신청이 접수되었습니다.', { id });

// 오류 처리
toast.error('결제 처리 중 오류가 발생했습니다. 고객센터에 문의해 주세요.', {
  duration: 8000,
  closeButton: true,
});
```

---

## 주의사항

- `<Toaster>`는 앱 전체에서 **한 번만** 렌더링합니다.
- React 18 이상, Next.js 13 이상 권장.
- SSR(서버사이드 렌더링) 환경에서는 클라이언트 컴포넌트로 지정 필요.

---

**작성일:** 2026-09-08  
**참고:** https://sonner.emilkowal.ski
