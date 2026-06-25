# Grepping for a Needle in a Haystack

**Module:** Linux Luminarium → Comprehending Commands  
**Challenge:** #4  
**Tags:** `grep`, `search`, `pattern`

---

## 문제 설명

수많은 텍스트 중에서 flag를 찾아야 한다.  
`grep` 명령어로 `pwn.college`가 포함된 줄을 찾는다.

---

## 풀이

```bash
# /challenge/run이 거대한 파일을 출력할 때
/challenge/run | grep "pwn.college"

# 또는 파일 내에서 직접 검색
grep "pwn.college" /challenge/data.txt

# 재귀 검색
grep -r "pwn.college" /challenge/
```

**출력:**
```
pwn.college{...}
```

---

## grep 완전 정복

### 기본 사용
```bash
grep "pattern" file          # 기본 검색
grep -i "pattern" file       # 대소문자 무시
grep -n "pattern" file       # 줄번호 표시
grep -c "pattern" file       # 매칭 줄 수
grep -l "pattern" *.txt      # 파일명만 출력
grep -v "pattern" file       # 매칭 안되는 줄
```

### 정규표현식
```bash
grep "^start" file           # 줄 시작
grep "end$" file             # 줄 끝
grep "a.b" file              # a + 임의문자 + b
grep "a*b" file              # a가 0회 이상 반복 후 b
grep "a\+" file              # a가 1회 이상 반복
grep -E "a|b" file           # a 또는 b (확장 정규식)
grep -E "[0-9]+" file        # 숫자
```

### 컨텍스트 출력
```bash
grep -A 3 "pattern" file     # 매칭 줄 + 이후 3줄
grep -B 3 "pattern" file     # 매칭 줄 + 이전 3줄
grep -C 3 "pattern" file     # 매칭 줄 + 전후 3줄
```

### 재귀/바이너리
```bash
grep -r "pattern" /dir/      # 재귀 검색
grep -rl "pattern" /dir/     # 파일명만
grep -a "pattern" binary     # 바이너리 파일도 검색
strings binary | grep "pattern"  # 바이너리 문자열 검색
```

---

## CTF에서 grep 활용

```bash
# flag 패턴 검색
grep -r "pwn.college{" / 2>/dev/null

# 특정 형식 검색
grep -oE "pwn\.college\{[^}]+\}" file  # flag만 추출

# 16진수 문자열 검색
grep -oE "[0-9a-f]{32}" file          # MD5 해시 형식
```
