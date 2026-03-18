---
name: Game Research Viewer - 디자인 시스템 현황
description: index.html + style.css 기반 vanilla JS SPA의 디자인 토큰, 컴포넌트 구조, 라우팅 방식
type: project
---

이 뷰어는 프레임워크 없는 vanilla JS SPA로, marked.js CDN으로 마크다운을 렌더링한다.

## 파일 위치
- `/Users/kcy/Works/Game-Design/Game-Research/index.html` — 마크업 + 인라인 JS 전체
- `/Users/kcy/Works/Game-Design/Game-Research/style.css` — 전체 스타일

## 디자인 토큰 (CSS 변수)
- 배경: `--color-bg` (#fff / #0f0f1a), `--color-bg-secondary` (#f8f9fb), `--color-bg-tertiary` (#f1f3f5)
- 텍스트: `--color-text` (#1a1a2e), `--color-text-secondary` (#5a5a72), `--color-text-muted` (#8e8ea0)
- 강조: `--color-accent` (#4f46e5 라이트 / #818cf8 다크), `--color-accent-light` (#eef2ff)
- 배지: genre=파란계열, platform=핑크계열, default=회색
- `--radius: 8px`, `--transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1)`
- 다크모드: `@media (prefers-color-scheme: dark)` 자동 전환

## 레이아웃
- CSS Grid 2열 (`--sidebar-width: 280px` + 나머지)
- 헤더 높이: `--header-height: 56px`
- 모바일(<768px): 사이드바 fixed + slide-in, 해머거 버튼 표시
- 문서 본문 max-width: `--content-max-width: 800px`

## 라우팅 방식
- 해시 기반(`#doc-id`). 해시 없으면 대시보드, 있으면 문서 로드
- `state.docs`, `state.current`, `state.filter` 전역 객체로 관리
- `docs.json`에서 문서 목록 fetch. `id`는 path에서 자동 생성

## 대시보드 구조 (2026-03-18 추가)
- `main__inner--dashboard` 클래스 추가 시 max-width 해제 → 3열 그리드
- 컴포넌트: dashboard-heading → dashboard-stats (stat-chip) → dashboard-filters (filter-tab) → doc-grid (doc-card)
- path 없는 문서는 카드 disabled 처리 (opacity 0.45)
- 카테고리 색상: game=인디고, player=에메랄드, market=앰버, liveops=바이올렛, funnel=레드

**Why:** 웰컴 메시지 대신 문서 목록을 카드 그리드로 즉시 보여주기 위해 추가됨.
**How to apply:** 추가 컴포넌트 설계 시 기존 CSS 변수와 BEM 클래스 네이밍 패턴을 따를 것.
