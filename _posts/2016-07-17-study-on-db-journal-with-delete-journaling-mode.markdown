---
layout: post
title:  "delete mode journal의 recovery 연구"
date:   2016-07-17 18:47:49 +0900
---

- crash.test에 있는 crash-2.~ 이용
- splited/sqlite3-9.c에 있는 `pager_playback()`이 이용 되는 것을 확인
- 이때 마스터 저널 이름도 확인을 하는데, 이 경우 db 한개만 사용했으므로 `zMaster` 가 "" 인 것을 확인 함
- `pager_end_transaction()`에서 db-journal 파일을 삭제하는 것을 확인함
- `sqlite3_config(SQLITE_CONFIG_LOG,sql_log);` 를 이용해 sqlite3 전역 설정을 바꿀 수 있었다. 이를 이용해 소스의 로그를 변경이 가능했음
- `sqlite3PagerSharedLock()` 에서 `SHARED_LOCK`을 obtain 한 후 `hasHotJournal()`로 hot journal의 유무를 확인한다. 있으면 playback 한다.
- `pager_playback()`에서 journal에서 master journal name을 읽어들이는데 이때 이 master journal name은 있는데 실제 파일은 없을 경우 그 journal은 hot 하지 않은것으로 간주하고 롤백 하지 않는다. 이는 롤백이 끝나고 나서 저널 파일을 지우려고 할때 크래쉬가 나는 경우를 말하는 것 같다.
