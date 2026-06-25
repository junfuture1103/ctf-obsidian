# Intro to Hacking

**Module:** Linux Luminarium → Hello Hackers  
**Challenge:** #1  
**Tags:** `first-run`, `basics`

---

## 문제 설명

pwn.college에서 처음으로 챌린지 바이너리를 실행하는 문제.  
`/challenge/run`을 실행하면 flag를 출력한다.

---

## 풀이

```bash
hacker@hello-hackers~intro-to-hacking:~$ /challenge/run
```

**출력:**
```
Yahaha, you found me! Here is your flag:
pwn.college{...}
```

---

## 핵심 개념

- 챌린지 바이너리는 항상 `/challenge/` 디렉토리에 있음
- 절대 경로(`/challenge/run`)로 실행
- SUID 설정으로 root 권한 실행 → `/flag` 파일 읽기 가능

---

## 관련 문제

- [[02-Catting-Absolute-Paths]] - 절대 경로로 파일 읽기
