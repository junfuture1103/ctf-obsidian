# Catting Absolute Paths

**Module:** Linux Luminarium → Hello Hackers  
**Challenge:** #2  
**Tags:** `cat`, `absolute-path`

---

## 문제 설명

`cat` 명령어와 절대 경로를 사용하여 특정 위치의 파일을 읽는다.  
챌린지 바이너리가 flag를 특정 경로에 복사해두면, cat으로 읽어야 한다.

---

## 풀이

```bash
hacker@hello-hackers~catting-absolute-paths:~$ /challenge/run
```

바이너리 실행 후 지정된 경로를 cat으로 읽기:

```bash
cat /flag
# 또는
cat /path/to/flag  # 바이너리가 알려주는 경로
```

**출력:**
```
pwn.college{...}
```

---

## cat 명령어

```bash
cat /flag                    # 절대 경로로 파일 읽기
cat /home/hacker/file.txt    # 다른 경로
cat file1 file2              # 여러 파일 연결 출력
```

### 절대 경로 vs 상대 경로
```
절대 경로: /flag              ← /로 시작, 어디서든 동일
상대 경로: ./flag             ← 현재 디렉토리 기준
         ../flag             ← 상위 디렉토리 기준
```

---

## 관련 문제

- [[01-Intro-to-Hacking]] - 첫 실행
- [[03-More-Catting-Practice]] - 다양한 경로
