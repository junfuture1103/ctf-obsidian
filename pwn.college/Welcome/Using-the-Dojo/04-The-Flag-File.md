# The Flag File

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #4  
**Tags:** `linux-basics`, `file-permissions`, `cat`, `flag`

---

## 문제 설명

`/flag` 파일의 구조와 접근 방법을 이해한다.  
파일 권한, SUID, 그리고 챌린지 바이너리를 통한 flag 획득 흐름을 학습한다.

---

## 핵심 개념

### /flag 파일
```bash
ls -la /flag
# -r-------- 1 root root 58 Jan 1 00:00 /flag
```

- 소유자: `root`
- 권한: `r--------` (root만 읽기 가능)
- `hacker` 사용자는 직접 읽기 **불가**

### 챌린지 바이너리를 통한 우회
```bash
ls -la /challenge/run
# -rwsr-xr-x 1 root root ... /challenge/run
```

SUID 설정 → root 권한으로 실행 → `/flag` 읽기 가능

---

## 풀이

### 단계 1: flag 파일 권한 확인
```bash
ls -la /flag
# -r-------- 1 root root 58 Jan 1 /flag
```

### 단계 2: 직접 읽기 시도 (실패 확인)
```bash
cat /flag
# cat: /flag: Permission denied
```

### 단계 3: 챌린지 실행으로 flag 획득
```bash
/challenge/run
# Here is your flag!
# pwn.college{...}
```

---

## Linux 파일 권한 상세

### 권한 표기법
```
-rwxrwxrwx
 |||------  others
 |||--- group  
 |||user/owner
 |file type (- regular, d dir, l link)
```

| 문자 | 숫자 | 의미 |
|------|------|------|
| r | 4 | 읽기 |
| w | 2 | 쓰기 |
| x | 1 | 실행 |
| s | - | SUID/SGID |
| t | - | Sticky bit |

### chmod 사용법
```bash
# 숫자 방식
chmod 755 file   # rwxr-xr-x
chmod 644 file   # rw-r--r--
chmod 600 file   # rw-------
chmod 400 file   # r--------

# 기호 방식
chmod u+x file   # 소유자에 실행 권한 추가
chmod go-w file  # 그룹/기타에서 쓰기 권한 제거
chmod +s file    # SUID 설정
```

### SUID / SGID
```bash
# SUID (Set User ID) - 소유자 권한으로 실행
chmod u+s file
# 결과: -rwsr-xr-x

# SGID (Set Group ID) - 그룹 권한으로 실행
chmod g+s file
# 결과: -rwxr-sr-x

# SUID 파일 시스템 전체 검색 (보안 감사에 활용)
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null
```

---

## cat 명령어 심화

```bash
# 기본 사용
cat /flag

# 여러 파일
cat file1 file2

# 줄번호 표시
cat -n /flag

# 특수문자 표시
cat -A /flag

# tac: 역순 출력
tac /flag
```

---

## 관련 개념

- [[02-Your-First-Flag]] - flag 기본
- [[03-Challenge-Programs]] - 챌린지 바이너리
- [[08-Using-the-Shell]] - 쉘 기본 명령어
