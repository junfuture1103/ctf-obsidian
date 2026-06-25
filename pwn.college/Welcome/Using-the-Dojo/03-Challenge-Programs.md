# Challenge Programs

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #3  
**Tags:** `linux-basics`, `binary-execution`, `suid`

---

## 문제 설명

pwn.college의 챌린지 바이너리를 실행하는 방법을 익힌다.  
모든 챌린지는 `/challenge/` 디렉토리에 실행 파일로 제공된다.

---

## 핵심 개념

### /challenge/ 디렉토리
pwn.college에서 모든 챌린지 바이너리는 `/challenge/` 디렉토리에 위치한다.

```bash
ls /challenge/
# run  (또는 challenge-specific binary name)
```

### 챌린지 실행 방법
```bash
/challenge/run
# 또는
/challenge/<challenge_name>
```

---

## 풀이

### 단계 1: 챌린지 디렉토리 확인
```bash
ls -la /challenge/
# total 20
# drwxr-xr-x 2 root root 4096 Jan  1 00:00 .
# drwxr-xr-x 1 root root 4096 Jan  1 00:00 ..
# -rwsr-xr-x 1 root root 8192 Jan  1 00:00 run
```

### 단계 2: 바이너리 정보 확인 (선택)
```bash
file /challenge/run
# /challenge/run: ELF 64-bit LSB executable, x86-64, ...

strings /challenge/run | head -20
```

### 단계 3: 실행
```bash
/challenge/run
# Correct! Here is your flag:
# pwn.college{...}
```

---

## ELF 바이너리 기초

### file 명령어
```bash
file /challenge/run
# ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV),
# dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2,
# BuildID[sha1]=..., for GNU/Linux 3.2.0, not stripped
```

- **ELF:** Linux 실행 파일 형식
- **64-bit:** 64비트 아키텍처
- **LSB:** Little-endian
- **PIE:** Position Independent Executable (ASLR 지원)
- **dynamically linked:** 공유 라이브러리 사용
- **not stripped:** 심볼 정보 포함 (디버깅 용이)

### SUID 실행 파일
```bash
ls -la /challenge/run
# -rwsr-xr-x 1 root root ... /challenge/run
#    ^
#    s = SUID bit (root 권한으로 실행됨)
```

---

## 유용한 명령어

```bash
# 실행 파일 정보
file /challenge/run
readelf -h /challenge/run

# 문자열 확인
strings /challenge/run

# 동적 라이브러리 확인
ldd /challenge/run

# strace로 시스템 콜 추적
strace /challenge/run

# ltrace로 라이브러리 콜 추적
ltrace /challenge/run
```

---

## 실행 권한 오류 시

```bash
# 실행 권한 없는 경우
chmod +x /challenge/run  # 보통 이미 설정됨

# 경로 문제
./run          # 현재 디렉토리
/challenge/run # 절대 경로 (권장)
```

---

## 관련 개념

- [[02-Your-First-Flag]] - flag 획득 기본
- [[04-The-Flag-File]] - flag 파일
- [[10-Talking-to-Programs]] - 프로그램에 입력 전달
