# Process Substitution

**Module:** Linux Luminarium → Practicing Piping  
**Challenge:** #14  
**Tags:** `process-substitution`, `bash`, `advanced-piping`

---

## 문제 설명

프로세스 치환(`<()`, `>()`)을 사용하여 명령어 출력을 파일처럼 다른 명령어에 전달한다.

---

## 풀이

```bash
# <() 프로세스 치환: 명령어 출력을 파일처럼 사용
/challenge/run < <(/challenge/input_generator)

# 또는
diff <(/challenge/run1) <(/challenge/run2)

# >() 프로세스 치환: 출력을 다른 프로세스의 입력으로
/challenge/run > >(/challenge/receiver)
```

**출력:**
```
pwn.college{...}
```

---

## 프로세스 치환 문법

### 입력 치환 `<(command)`
```bash
# 명령어 출력을 임시 파일처럼 사용
diff <(ls dir1) <(ls dir2)     # 두 디렉토리 비교
sort -u <(cat file1) <(cat file2)  # 합치고 정렬

# 실제 동작: /dev/fd/N 으로 전달
echo <(echo "hello")
# /dev/fd/63  ← 임시 파일 디스크립터
```

### 출력 치환 `>(command)`
```bash
# 출력을 다른 프로세스의 stdin으로
tee >(grep "error") >(wc -l)

# 로깅
command > >(tee logfile)
```

---

## 언제 프로세스 치환을 쓰나?

```bash
# 일반 파이프 불가 케이스:
# diff는 두 파일 인수가 필요
diff file1 <(sort file2)    # 한쪽만 파이프

# 두 명령어 비교
diff <(command1) <(command2)

# while 루프에서 변수 유지
while read line; do
    count=$((count+1))
done < <(cat file)  # 서브쉘 없이 읽기
```

---

## 파이프 vs 프로세스 치환

```bash
# 파이프: 왼쪽 → 오른쪽 단방향
cmd1 | cmd2

# 프로세스 치환: 파일처럼 전달 (순서 유연)
cmd2 <(cmd1)          # cmd1 출력 → cmd2의 인수
cmd1 > >(cmd2)        # cmd1 출력 → cmd2 stdin
```
