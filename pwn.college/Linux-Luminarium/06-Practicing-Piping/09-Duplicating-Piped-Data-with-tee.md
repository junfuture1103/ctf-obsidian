# Duplicating Piped Data with tee

**Module:** Linux Luminarium → Practicing Piping  
**Challenge:** #9  
**Tags:** `tee`, `pipe`, `duplicate`

---

## 문제 설명

`tee` 명령어를 사용하여 데이터를 파일에 저장하면서 동시에 다음 명령으로 파이프한다.

---

## 풀이

```bash
# tee: stdout으로 출력하면서 동시에 파일에도 저장
/challenge/run | tee /home/hacker/output | /challenge/receiver

# 또는 파일 저장 + 화면 출력
/challenge/run | tee /tmp/flag_output
cat /tmp/flag_output
```

**출력:**
```
pwn.college{...}
```

---

## tee 명령어

```bash
# 기본 사용
command | tee file       # 출력 복제: stdout + file

# 추가 모드
command | tee -a file    # 기존 파일에 추가

# 여러 파일
command | tee file1 file2

# 보이지 않게 (파일에만)
command | tee file > /dev/null

# 확인하면서 저장
long_command | tee output.txt | tail -5
```

---

## 파이프라인에서 tee 활용

```bash
# 중간 단계 확인
cat /etc/passwd | tee /tmp/debug | grep root

# 로깅하면서 처리
./exploit | tee exploit.log | grep "flag"

# 두 프로그램에 동시 전달
/challenge/run | tee >(program1) >(program2) > /dev/null
```

---

## 프로세스 치환과 결합

```bash
# >() 프로세스 치환으로 여러 프로그램에 데이터 전달
command | tee >(grep "error" > errors.log) >(wc -l > count.txt)

# 입력 프로세스 치환
diff <(command1) <(command2)
```
