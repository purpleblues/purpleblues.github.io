# delete mode journal의 recovery 연구
## 7월 16일

- crash.test에 있는 crash-2.~ 이용
- splited/sqlite3-9.c에 있는 `pager_playback()`이 이용 되는 것을 확인
- 이때 마스터 저널 이름도 확인을 하는데, 이 경우 db 한개만 사용했으므로 `zMaster` 가 ""  인 것을 확인 함
- `pager_end_transaction()`에서 db-journal 파일을 삭제하는 것을 확인함
- `sqlite3_config(SQLITE_CONFIG_LOG,sql_log);` 를 이용해 sqlite3 전역 설정을 바꿀 수 있었다. 이를 이용해 소스의 로그를 변경이 가능했음


