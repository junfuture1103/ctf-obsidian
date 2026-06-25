# More Catting Practice

**Module:** Linux Luminarium → Hello Hackers  
**Challenge:** #3  
**Tags:** `cat`, `absolute-path`, `file-system`

---

## 문제 설명

flag가 예상치 못한 위치에 있다. 챌린지 바이너리가 알려주는 임의의 경로에서 flag를 읽어야 한다.

---

## 풀이

```bash
hacker@hello-hackers~more-catting-practice:~$ /challenge/run
```

바이너리 출력 예시:
```
The flag is in a random-ish place in the file system. 
Go find it! It's at /some/random/path/flag
```

flag 경로를 cat으로 읽기:
```bash
cat /some/random/path/flag
# pwn.college{...}
```

---

## 다양한 경로 처리

```bash
# 공백이 있는 경로
cat "/path with spaces/flag"
cat /path\ with\ spaces/flag

# 특수문자가 있는 경로
cat "/path/with-dashes/flag"

# 깊은 중첩 경로
cat /a/b/c/d/e/f/flag
```

---

## find로 flag 파일 찾기 (대안)

경로를 잊었거나 모를 때:
```bash
find / -name flag 2>/dev/null
find / -name "flag" -type f 2>/dev/null
```

---

## 관련 문제

- [[02-Catting-Absolute-Paths]] - 기본 cat
- [[02-Pondering-Paths/Overview]] - 경로 심화
