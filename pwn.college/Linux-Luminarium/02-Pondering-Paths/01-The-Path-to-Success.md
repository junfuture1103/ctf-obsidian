# The Path to Success

**Module:** Linux Luminarium → Pondering Paths  
**Challenge:** #1  
**Tags:** `absolute-path`, `binary-execution`

---

## 문제 설명

절대 경로를 사용하여 챌린지 바이너리를 실행해야 한다.  
`run` 또는 `PATH에 없는 바이너리`를 절대 경로로 실행하는 방법을 익힌다.

---

## 풀이

```bash
# 절대 경로로 실행
/challenge/run
```

**출력:**
```
pwn.college{...}
```

---

## 절대 경로의 중요성

```bash
# 이렇게 하면 안 됨 (PATH에 없으면 실패)
run
# bash: run: command not found

# 이렇게 해야 함
/challenge/run   # 항상 동작
```

---

## 경로 확인 명령어

```bash
pwd              # 현재 위치 확인
ls /challenge/   # 챌린지 파일 목록
which run        # PATH에서 검색 (없으면 실패)
```
