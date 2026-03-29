---
title: "werdy.github.io 블로그 글 작성 가이드"
description: "Astro-Yi 테마 기반 werdy.github.io 사이트용 마크다운 포스트 작성 가이드와 예제"
date: 2026-03-29
---

# werdy.github.io 블로그 작성 안내

이 문서는 werdy.github.io 사이트(Astro Yi 테마)를 위한 새 블로그 포스트 작성 방법을 설명합니다. 새 파일은 `src/content/blog/` 폴더(또는 하위 폴더)에 `.md` 또는 `.mdx` 형식으로 추가하세요. 커밋(push)하면 GitHub Actions가 빌드하여 사이트를 배포합니다.

---

## 파일명과 위치

- 위치: `src/content/blog/`
- 권장 파일명: `2026-03-29-new-feature.md` 또는 `my-topic.md`처럼 설명적인 이름
- 파일 확장자는 `.md` 또는 `.mdx` 가능(레포의 기존 예시를 참고하세요)

## Frontmatter (YAML)

파일 맨 위에 YAML frontmatter 블록을 포함해야 합니다. 기존 포스트에서 사용되는 주요 필드는 다음과 같습니다:

- `title` (문자열) — 필수: 글 제목
- `description` (문자열) — 카드와 meta description에 노출되는 요약
- `date` (YYYY-MM-DD) — 필수: 게시일 또는 작성일
- `tags` (배열) — 예: `tags: [astro, feature]`
- `category` (문자열 또는 배열) — 테마에서 사용하는 분류
- `mermaid: true` — Mermaid 다이어그램 활성화(옵션)
- `mathjax: true` — MathJax 활성화(옵션)
- `ogImage` — OpenGraph 이미지용 전체 URL(옵션)

예시 frontmatter:

```yaml
---
title: "새 포스트 제목"
description: "포스트의 짧은 설명"
date: 2026-03-29
tags: [guide, astro]
mermaid: true
mathjax: true
---
```

## 콘텐츠 작성 가이드

사이트(테마)는 다양한 Markdown/MDX 기능을 지원합니다. 다음 패턴을 따르세요:

- 제목: `#`, `##`, `###` 등
- 구분선: `---`
- 강조: `**굵게**`, `_이탤릭_`, `~~취소선~~`
- 인용: `> 인용문`
- 목록: `-`, `*`, `+` (순서 있는 목록은 숫자 사용)
- 코드 블록: 트리플 백틱(```)과 언어 표기로 문법 하이라이팅

예시:

```js
```js
console.log('hello world')
```
```

- 코드 블록 제목, Expressive Code 마커 등 레포의 기존 예시를 참고하세요.

- 이미지: `![alt](url)` 형식 사용. 로컬 이미지는 `public/`에 두고 `/assets/...` 또는 `/public/...` 경로로 참조하세요.

- 링크: `[텍스트](URL)` 형식 사용

## Astro-Yi 테마 고유 기능 예시

기존 포스트에서 사용된 테마별 단축문법 예시:

- 버튼

```text
:btn[Google]{href="https://www.google.com"}
```

- GitHub 카드

```text
::github{repo="owner/repo"}
```

- 접기(collapse)

```text
:::collapse
숨겨진 내용
:::
```

- 어드모니션(admonition)

```markdown
:::tip[팁 제목]
유용한 팁 텍스트
:::
```

- Mermaid: frontmatter에 `mermaid: true` 추가 후 ```mermaid 블록 사용
- MathJax: frontmatter에 `mathjax: true` 추가 후 `$ ... $` 또는 `$$ ... $$` 사용

## 댓글 (Giscus)

Giscus 댓글을 사용하려면 `src/consts.ts`에서 설정을 활성화하고, https://giscus.app/ 에서 생성한 스크립트를 적용하세요. 포스트 자체에는 별도 마크업이 필요 없으며, 테마가 페이지 경로를 매핑해 Discussions를 연결합니다.

## 이미지 및 에셋

- 로컬 이미지는 `public/` 또는 `public/assets/` 같은 폴더에 넣고 절대 경로(`/assets/...`)로 참조하세요.
- CDN에 올려 절대 URL을 사용하면 외부 링크 차단 문제를 줄일 수 있습니다.

## MDX 주의사항

- `.mdx` 파일에서는 JSX 컴포넌트를 사용할 수 있습니다. 컴포넌트는 테마 빌드 환경에서 사용 가능한지 확인하세요.

## 커밋 및 배포 워크플로

1. `src/content/blog/`에 새 `.md` 또는 `.mdx` 파일 생성
2. 커밋: `git add src/content/blog/your-post.md && git commit -m "Add: your-post"`
3. 푸시: `git push origin main` (또는 Pages에 설정된 브랜치)
4. GitHub Actions가 빌드하고 Pages에 배포합니다.

## 레포의 예시 참고

- `250227-astro-yi-theme-setup.md` — 설치 및 이미지 사용 예
- `markdown-elements.md` — 마크다운 기능 예제
- `new-features.md` — mermaid, mathjax, admonition, expressive code 예

## 게시 전 체크리스트

- [ ] frontmatter에 title, description, date 포함
- [ ] tags, category 필요 시 추가
- [ ] 이미지 경로 확인
- [ ] mermaid/mathjax 사용 시 frontmatter 활성화
- [ ] 로컬에서 `pnpm build`로 빌드 테스트(권장)

---

원하면 제가 다음을 대신 해줄게:
- 이 가이드를 번역한 파일을 리모트에 커밋하고 푸시(SSH 인증이 설정되어 있으면 내가 푸시 가능)
- 새로운 포스트 템플릿(스크립트) 추가 또는 PR 생성
- 포스트 작성 템플릿을 자동화하는 스크립트 생성

원하시면 지금 바로 이 파일을 Git에 커밋하고 푸시해줄게. 원하나요?