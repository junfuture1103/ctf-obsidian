# Invoking Python

**Module:** Linux Luminarium → Silly Shebanigans  
**Challenge:** #3  
**Tags:** `python`, `shebang`, `script`

---

## 문제 설명

Python 스크립트를 실행 파일로 만들어 챌린지를 해결한다.

---

## 풀이

### 방법 1: Python 스크립트 파일
```python
#!/usr/bin/env python3
import os
import subprocess

# 챌린지 실행
result = subprocess.run(["/challenge/run"], capture_output=True, text=True)
print(result.stdout)
```

```bash
chmod +x solve.py
./solve.py
```

### 방법 2: 직접 실행
```bash
python3 -c "import subprocess; print(subprocess.run(['/challenge/run'], capture_output=True, text=True).stdout)"
```

### 방법 3: 챌린지가 Python 스크립트를 요구하는 경우
```bash
# /challenge/run이 Python 파일을 인수로 받는 경우
cat > /tmp/solution.py << 'EOF'
#!/usr/bin/env python3
print("required_output")
EOF
chmod +x /tmp/solution.py
/challenge/run /tmp/solution.py
```

---

## Python으로 CTF 작업

### 프로세스 실행
```python
import subprocess
import os

# 간단한 실행
result = subprocess.run(["/challenge/run"], capture_output=True, text=True)
print(result.stdout)
print(result.stderr)

# 입력 전달
result = subprocess.run(["/challenge/run"], input="my input\n", capture_output=True, text=True)

# 환경 변수 설정
env = os.environ.copy()
env["MY_VAR"] = "value"
result = subprocess.run(["/challenge/run"], env=env, capture_output=True, text=True)
```

### 파일 조작
```python
# 파일 읽기
with open("/flag", "r") as f:
    print(f.read())

# 바이너리 읽기
with open("/challenge/run", "rb") as f:
    data = f.read()
    
# 파일 쓰기
with open("/tmp/output", "w") as f:
    f.write("content")
```

### 바이너리/인코딩
```python
# 바이트 조작
data = b"\x41\x42\x43"
print(data.hex())   # 414243
print(data.decode())  # ABC

# base64
import base64
encoded = base64.b64encode(b"hello")
decoded = base64.b64decode(encoded)

# 16진수
bytes.fromhex("414243")  # b'ABC'
b"ABC".hex()              # '414243'
```

---

## Python one-liners

```bash
# 파일 내용 출력
python3 -c "print(open('/flag').read())"

# 바이너리 출력
python3 -c "import sys; sys.stdout.buffer.write(b'\x41'*100)"

# 명령 실행
python3 -c "import os; os.system('/challenge/run')"

# pwntools
python3 -c "from pwn import *; p = process('/challenge/run'); print(p.recvall())"
```
