---
layout: post
title:  "single wal db recovery on crash"
---

`walcrash.test` 를 이용하여 단일 wal db 파일을 크래쉬 시켜보았다.

- `pagerBeginReadTransaction()`까지는 non-WAL과 동일하지만 그 안에서 WAL을 쓰는지 여부에 따라 함수가 분기하여 `pagerBeginReadTransaction()`으로 들어가서 WAL의 read transaction을 시작한다.

- `pagerBeginReadTransaction()`을 시작하자마자 `sqlite3WalEndReadTransaction()`을 실행하는데, 위에 주석이 있긴 한데 이해가 잘 되지 않는다. 그 전에 끝나지 않은 트랜잭션이 있다면 끝내는 것?
- 함수 콜을 따라가다보면 WRITE LOCK 을 붙잡고도 wal-index header가 malformed 돼있으면 그건 header가 corrupted됐다고 판단이 되어 recovery를 수행한다. 이때 recovery하는 함수가 `walIndexRecover()`이다.
