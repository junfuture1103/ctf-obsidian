# pwntools Reference

**태그:** `pwntools`, `python`, `ctf-tools`, `reference`

---

## 설치

```bash
pip install pwntools
# 또는
pip3 install pwntools
```

---

## 기본 임포트

```python
from pwn import *

# 또는 선택적 임포트
from pwnlib.tubes.process import process
from pwnlib.tubes.remote import remote
from pwnlib.tubes.ssh import ssh
```

---

## 컨텍스트 설정

```python
# 아키텍처/OS 설정
context.arch = 'amd64'       # x86-64
context.arch = 'i386'        # x86-32
context.arch = 'arm'
context.os = 'linux'
context.bits = 64
context.endian = 'little'

# 로그 레벨
context.log_level = 'debug'  # 디버그 출력
context.log_level = 'info'
context.log_level = 'error'

# 한 번에 설정
context(arch='amd64', os='linux', log_level='debug')
```

---

## 프로세스 연결

```python
# 로컬 프로세스
p = process("/challenge/run")
p = process(["/challenge/run", "arg1", "arg2"])
p = process("/challenge/run", env={"VAR": "value"})

# 원격 TCP
p = remote("host", port)
p = remote("dojo.pwn.college", 1337)

# SSH
shell = ssh(host="dojo.pwn.college",
            user="hacker",
            keyfile="~/.ssh/id_ed25519")
p = shell.process("/challenge/run")
p = shell.run("cat /flag")
```

---

## 데이터 수신

```python
# 기본 수신
data = p.recv(n)              # 최대 n 바이트 수신
data = p.recv(4096)           # 최대 4096 바이트
data = p.recvn(n)             # 정확히 n 바이트
line = p.recvline()           # 줄바꿈까지
line = p.recvline(keepends=False)  # 줄바꿈 제거
data = p.recvuntil(b":")      # 특정 패턴까지
data = p.recvuntil(b">>", drop=True)  # 패턴 제거
data = p.recvall()            # 프로세스 종료까지 전부

# 타임아웃
data = p.recv(timeout=5)
data = p.recvline(timeout=2)

# 예외 처리
try:
    data = p.recvuntil(b"flag", timeout=10)
except EOFError:
    print("Connection closed")
```

---

## 데이터 송신

```python
p.send(b"data")               # 그대로 전송
p.sendline(b"data")           # + \n
p.sendafter(b"prompt: ", b"response")     # 프롬프트 후 전송
p.sendlineafter(b"prompt: ", b"response") # + \n

# 여러 줄
p.sendline(b"line1")
p.sendline(b"line2")
```

---

## 패킹/언패킹

```python
# 정수를 바이트로 (리틀 엔디안)
p32(0xdeadbeef)    # 4바이트 리틀 엔디안
p64(0xdeadbeef)    # 8바이트 리틀 엔디안
p16(0x1234)        # 2바이트

# 빅 엔디안
p32(0xdeadbeef, endian='big')

# 바이트를 정수로
u32(b"\xef\xbe\xad\xde")    # → 0xdeadbeef
u64(b"\xef\xbe\xad\xde\x00\x00\x00\x00")

# flat으로 여러 값 패킹
payload = flat(
    0x41 * 24,      # 패딩
    0xdeadbeef,     # 리턴 주소
    0xcafebabe      # 다음 값
)
```

---

## ELF 분석

```python
elf = ELF("/challenge/run")

# 주소 조회
elf.address           # 베이스 주소
elf.symbols['main']   # 함수 주소
elf.got['printf']     # GOT 엔트리
elf.plt['printf']     # PLT 엔트리

# 섹션
elf.bss()             # BSS 섹션 주소
elf.data              # data 섹션 내용

# 문자열 검색
list(elf.search(b"/bin/sh"))
```

---

## 사이클릭 패턴 (버퍼 오버플로우 오프셋 찾기)

```python
# 패턴 생성
pattern = cyclic(100)    # 100바이트 패턴
print(pattern)           # aaaabaaacaaad...

# 크래시 주소로 오프셋 찾기
offset = cyclic_find(0x61616174)  # 크래시 시 EIP/RIP 값
offset = cyclic_find(b"taaa")     # 바이트 버전
print(f"Offset: {offset}")
```

---

## ROP (Return Oriented Programming)

```python
elf = ELF("/challenge/run")
rop = ROP(elf)

# 가젯 찾기
rop.find_gadget(['ret'])
rop.find_gadget(['pop rdi', 'ret'])

# 체인 생성
rop.raw(0x41414141)
rop.call('puts', [elf.got['puts']])
rop.call('main')

payload = rop.chain()
```

---

## GDB 연동

```python
# GDB 자동 실행
p = gdb.debug("/challenge/run", gdbscript="""
    break main
    continue
""")

# 실행 중인 프로세스에 attach
p = process("/challenge/run")
gdb.attach(p, gdbscript="continue")
```

---

## 자주 쓰는 패턴

### 기본 exploit 템플릿
```python
from pwn import *

context.arch = 'amd64'
context.os = 'linux'

# 연결
p = process("/challenge/run")
# p = remote("host", port)

# 출력 확인
p.recvuntil(b"Input: ")

# 페이로드 전송
payload = b"A" * 64
p.sendline(payload)

# 결과 확인
result = p.recvall()
print(result)

# flag 추출
flag = re.search(b"pwn.college{.*?}", result)
if flag:
    print("FLAG:", flag.group())
```

---

## 관련 개념

- [[Linux-Fundamentals]] - Linux 기초
- [[pwn.college/Welcome/Using-the-Dojo/10-Talking-to-Programs]] - 프로그램과 상호작용
