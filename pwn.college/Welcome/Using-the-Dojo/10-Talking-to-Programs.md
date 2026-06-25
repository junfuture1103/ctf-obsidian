# Talking to Programs

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #10  
**Tags:** `stdin`, `pipe`, `pwntools`, `interaction`

---

## 문제 설명

프로그램과 상호작용하는 방법을 익힌다.  
stdin으로 입력 전달, 파이프, 그리고 pwntools를 이용한 자동화된 상호작용을 학습한다.

---

## 핵심 개념

### 프로그램 상호작용 방법
1. **직접 입력** — 키보드로 타이핑
2. **파이프** — `echo` 또는 다른 명령어로 입력 전달
3. **리다이렉션** — 파일에서 입력 읽기
4. **pwntools** — Python으로 자동화된 상호작용

---

## 풀이

### 방법 1: 직접 실행
```bash
/challenge/run
# 프로그램이 입력을 요청하면 직접 타이핑
# > hello
# pwn.college{...}
```

### 방법 2: echo + 파이프
```bash
echo "hello" | /challenge/run
# 또는 특정 입력이 필요한 경우:
echo -e "line1\nline2" | /challenge/run
```

### 방법 3: printf + 파이프
```bash
printf "input\n" | /challenge/run
# 바이너리 데이터 전달
printf "\x41\x42\x43\n" | /challenge/run
```

### 방법 4: heredoc
```bash
/challenge/run << EOF
line 1
line 2
EOF
```

### 방법 5: 파일에서 입력
```bash
echo "input" > /tmp/input.txt
/challenge/run < /tmp/input.txt
```

### 방법 6: pwntools (Python)
```python
from pwn import *

# 로컬 프로세스
p = process("/challenge/run")

# 출력 읽기
output = p.recvline()
print(output)

# 입력 전송
p.sendline(b"hello")

# 상호작용 계속
p.interactive()

# flag 받기
flag = p.recvall()
print(flag)
```

---

## pwntools 기본 사용법

### 설치
```bash
pip install pwntools
```

### 프로세스 상호작용
```python
from pwn import *

p = process("/challenge/run")

# 데이터 수신
data = p.recv(100)          # 최대 100바이트
line = p.recvline()         # 줄 단위
until = p.recvuntil(b":")   # 특정 문자열까지
all_data = p.recvall()      # 종료까지 전부

# 데이터 송신
p.send(b"data")             # 줄바꿈 없이
p.sendline(b"data")         # 줄바꿈 포함
p.sendafter(b"prompt:", b"response")   # 프롬프트 후 전송

# 인터랙티브 모드
p.interactive()
```

### SSH를 통한 원격 접속 (pwntools)
```python
from pwn import *

# SSH 연결
shell = ssh(host='dojo.pwn.college',
            user='hacker',
            keyfile='~/.ssh/id_ed25519')

# 명령 실행
result = shell.run("cat /flag")
print(result.recvall())

# 프로세스 실행
p = shell.process("/challenge/run")
p.interactive()
```

---

## stdin/stdout/stderr 이해

```
프로그램
   ↑          ↓         ↓
stdin(0)  stdout(1) stderr(2)

# 리다이렉션
프로그램 < input.txt        # stdin을 파일에서
프로그램 > output.txt       # stdout을 파일로
프로그램 2> error.txt       # stderr를 파일로
프로그램 > out.txt 2>&1     # 둘 다 같은 파일로
```

### /dev/stdin 활용
```bash
cat /dev/stdin | /challenge/run
```

---

## 특수 케이스: 바이너리 입력

### Python으로 바이너리 데이터 생성
```python
# 특정 바이트 값 전달
import subprocess
payload = b"\x41" * 10 + b"\x00"
proc = subprocess.run(["/challenge/run"],
                     input=payload,
                     capture_output=True)
print(proc.stdout)
```

### Bash에서 바이너리 입력
```bash
# \x 이스케이프 시퀀스
printf "\x41\x42\x43" | /challenge/run

# Python으로 생성
python3 -c "import sys; sys.stdout.buffer.write(b'\x41'*10)" | /challenge/run
```

---

## 프로그램 출력 분석

```bash
# 출력 저장
/challenge/run > output.txt 2>&1

# 실시간 보면서 저장
/challenge/run | tee output.txt

# strace로 시스템 콜 추적
strace /challenge/run

# ltrace로 함수 호출 추적
ltrace /challenge/run
```

---

## 관련 개념

- [[03-Challenge-Programs]] - 챌린지 바이너리
- [[08-Using-the-Shell]] - 쉘 파이프/리다이렉션
- [[Linux-Fundamentals]] - Linux 기초 지식
