# Your First Flag

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #2  
**Tags:** `linux-basics`, `cat`, `flag`

---

## 문제 설명

pwn.college에서 처음으로 flag를 획득하는 문제.  
`/flag` 파일 또는 챌린지 바이너리 실행을 통해 flag를 얻는다.

---

## 핵심 개념

### Flag 형식
```
pwn.college{some_flag_content_here}
```

### Flag 파일 위치
- `/flag` — 대부분의 pwn.college 문제에서 flag가 저장되는 경로
- 일반적으로 root 소유, 챌린지 바이너리가 SUID로 읽어줌

---

## 풀이

### 단계 1: 접속
```bash
ssh hacker@dojo.pwn.college
```

### 단계 2: 챌린지 실행
```bash
# 챌린지 시작 후 바이너리 실행
/challenge/run
```

### 단계 3: Flag 획득
```
pwn.college{...여기에_실제_flag...}
```

### 직접 읽기 시도 (대부분 권한 거부됨)
```bash
cat /flag
# cat: /flag: Permission denied  ← 일반적으로 root만 읽을 수 있음

ls -la /flag
# -r-------- 1 root root ... /flag
```

챌린지 바이너리는 SUID 비트가 설정되어 있어 root 권한으로 flag를 읽어 출력해준다.

---

## Linux 파일 권한 기초

```
-rwxr-xr-x  1  root  root  12345  Jan 1  /challenge/run
 |||||||||||  |  ||||  ||||
 ||||||||||| links owner group
 |||------  others (r-x)
 |||--- group (r-x)
 |||user/owner (rwx)
 ||special bits
 |type (- = regular file)
```

### SUID 비트 (Set User ID)
```bash
ls -la /challenge/run
# -rwsr-xr-x  ← 's'가 SUID 비트
```
SUID가 설정된 실행 파일은 **파일 소유자의 권한**으로 실행된다.  
pwn.college 챌린지 바이너리는 root 소유 + SUID → root 권한으로 `/flag` 읽기 가능.

---

## 유용한 명령어

```bash
# 파일 내용 출력
cat /flag

# 파일 권한 확인
ls -la /flag

# 현재 사용자 확인
whoami
id

# SUID 파일 찾기
find / -perm -4000 2>/dev/null
```

---

## 관련 개념

- [[01-Connecting-over-SSH]] - SSH 접속
- [[03-Challenge-Programs]] - 챌린지 바이너리 실행
- [[04-The-Flag-File]] - flag 파일 심화
