---
title: "[오라클] ajax로 date를 받아올 때 날짜 format 변경"
subtitle: "millisecond를 YYYY/MM/DD&nbsp;HH24:MI:SS 포맷으로..."
categories: [ajax, oracle]
tags:
  - ajax
  - oracle [오라클]
published: true
---
제가 프로젝트를 진행하면서 부딫힌 문제에 대해서 나누고 싶습니다.

ajax 통신으로 오라클에서 date를 받아오면 날짜 형식이 millisecond로 나오는 경우가 있습니다.

이를 해결하기 위해서는 자바스크립트에서 날짜 format을 바꿔주는 방식 또는 DB상에서 바꿔주는 방식이 있는데 저는 아래의 **DB에서 formatting을 하는 코드**로 대체해서 이 문제를 해결했습니다.



```html
{% raw %}
TO_CHAR(DATE_COLUMN_NAME, 'YYYY/MM/DD HH24:MI:SS') AS 별칭
{% endraw %}
```
