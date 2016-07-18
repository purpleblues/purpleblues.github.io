---
layout: post
title:  "delete journaling mode의 multiple database transaction recovery에 대한 연구"
---

- `test.db`에 `test2.db`를 attach시키고 `test2.db-journal`에 크래쉬를 일으켜보았다.
- `test.db`는 `pager_playback()`이 정상적으로 이루어지고 `test2.db`의 `pager_playback()`에서는 `readJournalHdr()`로 journal file이 정상적인지 확인하였는데, 이때 `SQLITE_OK`가 아닌 `SQLITE_DONE`을 리턴함으로써 `end_playback:` 으로 goto 하는 것을 확인할 수 있었다. 
- 두 경우 다 저널 파일을 삭제 하였다.
