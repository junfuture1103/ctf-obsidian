# Exporting Variables

**Module:** Linux Luminarium → Shell Variables  
**Challenge:** #4  
**Tags:** `export`, `environment-variables`, `subprocess`

---

## 문제 설명

변수를 `export`하여 챌린지 바이너리(자식 프로세스)에서 접근할 수 있게 해야 한다.

---

## 풀이

```bash
# 변수 설정 후 export
PWN=value
export PWN

# 또는 한 번에
export PWN=value

# 챌린지 실행 (바이너리가 환경변수 PWN을 읽음)
/challenge/run
```

**출력:**
```
Congratulations! You set the variable correctly!
pwn.college{...}
```

---

## export의 작동 원리

```
현재 쉘 (부모)
    VAR=hello     ← 로컬 변수 (자식에게 안 보임)
    export VAR    ← 환경 변수로 승격 (자식에게 보임)
    /challenge/run  ← 자식 프로세스 생성
         ↓
    자식 프로세스
         getenv("VAR") = "hello"  ← 읽을 수 있음
```

```bash
# 확인
export MY_VAR="hello"
bash -c 'echo $MY_VAR'   # hello (자식 bash에서 보임)

# export 없으면
MY_VAR="hello"
bash -c 'echo $MY_VAR'   # 빈 줄 (자식에게 안 보임)
```

---

## 환경 변수 조작

```bash
# 일시적으로만 설정 (해당 명령어에만)
MY_VAR=hello /challenge/run

# 모든 환경 변수 확인
env
env | grep MY_VAR

# 특정 변수 확인
echo $MY_VAR
printenv MY_VAR

# 환경 변수 제거
unset MY_VAR
export -n MY_VAR  # export 취소 (로컬로)

# 초기화된 환경으로 실행
env -i /challenge/run    # 환경 변수 없이
env -i VAR=val /challenge/run  # 지정된 변수만
```

---

## CTF 활용: 환경 변수로 입력 전달

```bash
# 챌린지가 특정 환경 변수를 읽는 경우
export SECRET_KEY="mykey"
/challenge/run

# 여러 변수 한 번에
export VAR1=a VAR2=b VAR3=c
/challenge/run
```
