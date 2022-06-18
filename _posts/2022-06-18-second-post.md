---
title: "두 번째 포스팅"
excerpt: "두 번째 글"

categories:
    - Blog
tags:
    - [Blog]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2022-06-18
last_modified_at: 2022-06-18
---
# 작성한 글이 사이트에 표시되지 않는 문제
오늘 갑자기 작성 후 푸쉬한 글이 보이지 않는 현상이 생겼다.  
깃허브 로그에도 올라갔고  
127.0.0.1:4000 에서도 정상적으로 나오는데  
웹사이트 에서만 보이지가 않는다!  

그래서 해결 방법들을 찾다가  
아래의 링크에서 해결 방법을 찾았다.  

<https://stackoverflow.com/questions/30625044/jekyll-post-not-generated>  

_config.yml 에서 `future: true`를 추가해 줬더니  
정상적으로 글이 보이게 되었다.

기준 시간보다 앞선 상태에서 글을 작성하면  
날짜가 맞지않아 생기는 문제였다.


