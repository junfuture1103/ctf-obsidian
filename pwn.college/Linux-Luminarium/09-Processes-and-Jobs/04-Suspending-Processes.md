# Suspending Processes

**Module:** Linux Luminarium → Processes and Jobs  
**Challenge:** #4  
**Tags:** `Ctrl+Z`, `SIGSTOP`, `job-control`, `fg`, `bg`

---

## 문제 설명

실행 중인 챌린지 프로세스를 `Ctrl+Z`로 일시 중지(suspend)하고,  
다른 명령을 실행한 후 다시 포그라운드로 가져와야 한다.

---

## 풀이

### 시나리오: 동시에 두 인스턴스 실행

```bash
# 첫 번째 챌린지 실행
/challenge/run &    # 백그라운드로 시작
# 또는
/challenge/run
# (실행 중) → Ctrl+Z

# 중지 확인
# [1]+  Stopped   /challenge/run

# 작업 목록
jobs
# [1]+  Stopped   /challenge/run

# 두 번째 명령 실행
/challenge/run
# (다른 작업)

# 첫 번째 다시 포그라운드
fg %1
```

**출력:**
```
pwn.college{...}
```

---

## 잡 제어 심화

### 상태 전환
```
실행 중(Running)
    ↓ Ctrl+Z
중지됨(Stopped)
    ↓ bg / fg
포그라운드/백그라운드 실행
```

### jobs 명령어
```bash
jobs              # 현재 쉘의 잡 목록
jobs -l           # PID 포함
jobs -p           # PID만

# 출력 형식
# [1]+  Running    command &
# [1]+  Stopped    command
# [1]-  Stopped    command (이전 잡)
# [1]+  Done       command (완료)
```

### fg / bg
```bash
fg          # 가장 최근 잡 포그라운드
fg %1       # 1번 잡
fg %name    # 이름으로 지정

bg          # 가장 최근 정지 잡 백그라운드 재개
bg %2       # 2번 잡 백그라운드 재개
```

---

## 신호 (Signals)

```bash
# 잡에 신호 전송
kill %1           # SIGTERM to job 1
kill -STOP %1     # SIGSTOP (Ctrl+Z와 동일)
kill -CONT %1     # SIGCONT (재개)
kill -INT %1      # SIGINT (Ctrl+C와 동일)

# PID로 신호 전송
kill -SIGSTOP 1234
kill -SIGCONT 1234
```

---

## 실전 패턴

```bash
# 긴 작업 실행 중 잠시 다른 작업
./long_process
# Ctrl+Z
# [1]+  Stopped   ./long_process

ls /flag
cat /flag

fg           # long_process 재개
```
