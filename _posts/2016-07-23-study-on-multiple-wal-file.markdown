---
layout: post
title:  "multiple wal file 연구"
---

- `sqlite3WalOpen()`에서 wal파일을 연다. 이 함수 이전에 `sqlite3PagerSharedLock()`에서 이 함수를 실행한다.
