# Linux Fundamentals

**태그:** `linux`, `reference`, `basics`

---

## 파일 시스템 계층 구조 (FHS)

```
/               root
├── bin/        필수 사용자 바이너리 (ls, cat, bash...)
├── boot/       부트로더, 커널
├── dev/        장치 파일
├── etc/        설정 파일
├── home/       사용자 홈 디렉토리
├── lib/        공유 라이브러리
├── opt/        선택적 소프트웨어
├── proc/       프로세스 정보 (가상 fs)
├── root/       root 사용자 홈
├── sbin/       시스템 관리 바이너리
├── sys/        시스템 정보 (가상 fs)
├── tmp/        임시 파일
├── usr/        사용자 프로그램
└── var/        가변 데이터 (로그, 스풀...)
```

---

## 프로세스와 파일 디스크립터

```
표준 파일 디스크립터:
  0 = stdin  (표준 입력)
  1 = stdout (표준 출력)
  2 = stderr (표준 오류)

열린 파일 확인:
  ls -la /proc/$$/fd
  lsof -p $$
```

---

## 환경 변수

```bash
# 모든 환경변수
env
printenv

# 특정 변수
echo $PATH
echo $HOME
echo $USER

# 설정
export MY_VAR="value"

# 임시 설정 (명령어에만 적용)
MY_VAR="value" command
```

---

## 프로세스 신호

| 신호 | 번호 | 의미 |
|------|------|------|
| SIGKILL | 9 | 강제 종료 (무시 불가) |
| SIGTERM | 15 | 정상 종료 요청 |
| SIGINT | 2 | 인터럽트 (Ctrl+C) |
| SIGSEGV | 11 | 세그멘테이션 폴트 |
| SIGSTOP | 19 | 일시 중지 (무시 불가) |
| SIGCONT | 18 | 계속 |

```bash
kill -SIGTERM PID
kill -9 PID      # SIGKILL
kill -l          # 모든 신호 목록
```

---

## 사용자 및 권한 관리

```bash
# 사용자 정보
cat /etc/passwd     # 사용자 목록
cat /etc/group      # 그룹 목록
cat /etc/shadow     # 패스워드 해시 (root만)

# sudo 권한 확인
sudo -l

# 그룹 멤버십
groups
id
```

---

## 네트워크 기초

```bash
# 인터페이스 확인
ip addr
ifconfig

# 연결 확인
ss -tuln        # 열린 포트
netstat -tuln   # (구식)

# 연결 테스트
ping host
nc host port
curl http://host:port

# DNS
nslookup domain
dig domain
```

---

## /proc 파일 시스템

```bash
# 프로세스 정보
cat /proc/$$/status      # 현재 쉘 상태
cat /proc/$$/maps        # 메모리 맵
cat /proc/$$/cmdline     # 명령줄
ls /proc/$$/fd           # 열린 파일 디스크립터

# 시스템 정보
cat /proc/cpuinfo        # CPU 정보
cat /proc/meminfo        # 메모리 정보
cat /proc/version        # 커널 버전
cat /proc/net/tcp        # TCP 연결
```

---

## 유용한 CTF 명령어

```bash
# 바이너리 분석
file binary              # 파일 타입
strings binary           # 문자열 추출
xxd binary | head        # 헥스 덤프
readelf -h binary        # ELF 헤더
objdump -d binary        # 디스어셈블
nm binary                # 심볼 테이블

# 메모리/실행 분석
strace binary            # 시스템 콜 추적
ltrace binary            # 라이브러리 콜 추적
gdb binary               # 디버거

# 인코딩/암호화
base64 <<< "text"
echo -n "text" | md5sum
echo -n "text" | sha256sum
python3 -c "print(bytes.fromhex('4141'))"
```

---

## 관련 문서

- [[pwn.college/Welcome/Using-the-Dojo/08-Using-the-Shell]] - 쉘 사용법
- [[pwntools-Reference]] - pwntools 레퍼런스
