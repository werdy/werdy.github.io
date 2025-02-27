---
title: "Astro Yi Theme에 Giscus 댓글 기능 추가 하기"
description: "Giscus를 사용한 댓글 기능 설치 방법을 설명합니다. "
date: 2025-02-27 20:20
tags: ["Astro Yi", "Giscus", "댓글"]
---


### Giscus 설치 및 설정 script 생성

- https://github.com/apps/giscus 에 접속하여 Giscus를 설치 합니다. 
![image](https://github.com/user-attachments/assets/e7588a19-b694-4980-b24a-9a0ea5039c6a)
![image](https://github.com/user-attachments/assets/3f48133d-d78d-4a62-ba19-1af05e587483)

- Settings -> General에서 스크롤을 하단으로 내려 Features내에 Discussions 항목을 체크한다.
![image](https://github.com/user-attachments/assets/15e33ef8-f22c-496c-9498-16262b72db7b)


- https://giscus.app/ko 에 접속하여 사용할 댓글 기능에 대한 설정하여 블로그에 설정할 scipt를 생성합니다. 
![image](https://github.com/user-attachments/assets/ae869ce0-e03e-4dcf-90f5-51dcc7d5bab6)

**언어를 영어로 설정해 에러가 나지 않습니다.**

```
<script src="https://giscus.app/client.js"
        data-repo="werdy/werdy.github.io"
        data-repo-id="xxxxx"
        data-category="Announcements"
        data-category-id="xxxxxx"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="preferred_color_scheme"
        data-lang="en"
        crossorigin="anonymous"
        async>
</script>
```


### Astro Yi Theme consts.ts 설정

생성한 스크립트의 내용으로 src/consts.ts 파일의 comment 설정을 활성화 하고 giscusConfig도 받아온 giscus script의 내용으로 설정합니다.
![image](https://github.com/user-attachments/assets/462f733c-37d5-4856-bbf2-11ff72ac61b3)

```
  giscusConfig: {
    'data-repo': "werdy/werdy.github.io",
    'data-repo-id': "xxxxx",
    'data-category': "Announcements",
    'data-category-id': "DIC_kwDOOATFxc4CnY9B",
    'data-mapping': "pathname",
    'data-strict': "0",
    'data-reactions-enabled': "1",
    'data-emit-metadata': "0",
    'data-input-position': "top",
    'data-theme': "preferred_color_scheme",
    'data-lang': "en",
    'crossorigin': "anonymous",
  }
```
