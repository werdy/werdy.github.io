---
title: "Astro Yi Theme로 Github.io 설정하기 "
description: "Astro Yi theme 설치 및 git actions 설정하여 content commit pages 발행 하는 방법을 설명합니다.  "
date: 2025-02-27
tags: ["Astro Yi", "Setup"]
---

### 저장소 생성 및 테마 설치

- Github IO에 사용할 repository를 생성합니다. 
![image](https://github.com/user-attachments/assets/f701db4f-df6b-4bd0-8f66-5f8137e734d2)

- 저장소 이름을 입력하고,  Public, Add a README file을 선택합니다.
![image](https://github.com/user-attachments/assets/34ab71c9-eeb2-476d-b80a-a6f2eb4705d6)

- [Astro Yi](https://github.com/cirry/astro-yi) 를 다운로드 받고 소스를 저장소에 push 합니다.

- push된 소스에서 consts.ts 파일을 열고 페이지 설정을 변경합니다. 
![image](https://github.com/user-attachments/assets/7abe04c8-5491-4a01-94e1-cb85a4597fb6)


### Github Actions 설정

- Settings -> Pages 설정에서 Source를 Github Actions로 설정합니다. 설정하고 나면 바로 아래에 Github Pages JekyII 항목이 표시가됩니다. 
![image](https://github.com/user-attachments/assets/c2ae76be-9f57-44fc-8c44-db7ec0708f41)

- Github Pages JekyII -> Configure 버튼을 눌럭 actions YML파일을 생성합니다. 

- 이름을 astro-yi-pages.yml 로 변경합니다.  
![image](https://github.com/user-attachments/assets/d17d60b5-c67e-40c0-adf0-91a2fc1fa3c8)

- jobs 부분을 아래 내용으로 변경하고 오른쪽 상단의 commit changes.. 버튼을 눌러 저장합니다. 
```yml
jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v5

      - uses: pnpm/action-setup@v4
        name: Install pnpm
        with:
          version: 10
          run_install: false

      - name: Install Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'pnpm'

      - name: Install dependencies
        run: pnpm install

      - name: Build Astro site
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dist  
```

- actions 로 이동하여 빌드가 잘 되었는지 확인 합니다. 
![image](https://github.com/user-attachments/assets/f99951ea-f654-4259-b66d-3b922e0b2bcb)

- 빌드가 잘되었다면 userid.github.io 로 접속하면 기본 화면이 표시 됩니다. 
![image](https://github.com/user-attachments/assets/0eb2c9c2-5e6d-4c46-a1cf-57e06913775f)


### 블로그 글쓰기
- src/content 로 이동하여 원하는 카테고리 폴더 아래에 md 파일을 생성합니다.
![image](https://github.com/user-attachments/assets/e5602423-6a0f-4504-b78b-5f50633c68e0)

- 파일명을 입력하고(확장자는 .md 로) astro yi에서 정한 방식에 맞게 header 정보를 작성 하고, 그 아래에 블로그 글을 작성하고 저장합니다. 
![image](https://github.com/user-attachments/assets/db475244-adcb-48f5-a405-861c5e274040)

- 저장 하면, git action가 실행 되면서 github.io pages가 업데이트 됩니다.
![image](https://github.com/user-attachments/assets/66a04af5-4ef1-4532-a6c7-7ac0d8ae72f2)

  

