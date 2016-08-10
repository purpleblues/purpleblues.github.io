---
layout: post
title:  "crashsql에 대한 연구"
---

`crashsql`이라는 sqlite 테스트에 쓰이는 기존에 만들어진 tcl 함수가 있다.
이는 file sync가 일어나는 도중에 crash를 시켜서 corrupted file을 만들어준다.
이 함수의 인자에 대한 연구이다.

- `delay` : `fsync()` 가 몇 번 정상적으로 일어난 후에 크래쉬를 시킬지에 대한 인자이다. 예를들어 `4`이면 5번째 `fsync()`에서 크래쉬가 일어난다.

- `file` : 크래쉬를 일으킬 파일이다.

- `seed` : `SELECT RANDOMBLOB($SEED)`를 실행하여 PRNG 에 random seed값을 넣어주는 것 같다. 자세한건 불명

- `sql` : 실행시킬 sql
