# Redirecting Output

**Module:** Linux Luminarium → Practicing Piping  
**Challenge:** #1  
**Tags:** `redirect`, `stdout`, `file-output`

---

## 문제 설명

챌린지 바이너리의 출력을 특정 파일로 리다이렉션해야 한다.

---

## 풀이

```bash
# stdout을 파일로 저장
/challenge/run > /home/hacker/output
# 또는
/challenge/run > /tmp/flag

# 저장된 내용 확인
cat /home/hacker/output
# pwn.college{...}
```

---

## 리다이렉션 완전 정복

### stdout (파일 디스크립터 1)
```bash
command > file      # stdout → file (덮어쓰기)
command 1> file     # 동일 (명시적)
command >> file     # stdout → file (추가)
command > /dev/null # 출력 버리기
```

### stderr (파일 디스크립터 2)
```bash
command 2> file     # stderr → file
command 2>> file    # stderr → file (추가)
command 2>/dev/null # stderr 버리기
```

### 동시 리다이렉션
```bash
command > out.txt 2>&1      # stdout, stderr 모두 파일로
command &> file             # 위와 동일 (bash 단축)
command > out 2> err        # 각각 다른 파일
command 2>&1 | grep pattern # stderr도 파이프로
```

### 순서가 중요한 이유
```bash
# stderr → stdout → file (올바른 순서)
command > file 2>&1

# 잘못된 순서! stderr를 현재 stdout(터미널)으로 보낸 후 stdout을 file로
command 2>&1 > file  ← stderr는 터미널로 나옴
```

---

## stdin 리다이렉션

```bash
command < file         # file → stdin
command << EOF         # here-document (직접 입력)
line 1
line 2
EOF

command <<< "string"   # here-string
```

---

## /dev 특수 파일

```bash
/dev/null    # 블랙홀 (읽으면 EOF, 쓰면 버려짐)
/dev/zero    # 0바이트 무한 스트림
/dev/urandom # 난수 스트림
/dev/stdin   # stdin 파일 디스크립터
/dev/stdout  # stdout 파일 디스크립터
/dev/stderr  # stderr 파일 디스크립터
/dev/fd/0    # fd 0 (stdin)
/dev/fd/1    # fd 1 (stdout)
```
