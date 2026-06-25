# Challenge Files

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #9  
**Tags:** `linux-basics`, `file-system`, `find`, `navigation`

---

## 문제 설명

챌린지 환경의 파일 시스템을 탐색하고 필요한 파일을 찾는 방법을 익힌다.  
`find`, `ls`, `file` 등의 명령어를 활용한다.

---

## 핵심 개념

### pwn.college 파일 시스템 구조
```
/
├── challenge/          ← 챌린지 바이너리 위치
│   └── run             ← 실행할 챌린지 파일
├── flag                ← flag 파일 (root 소유)
├── home/
│   └── hacker/         ← 홈 디렉토리
│       ├── .ssh/
│       └── (작업 파일들)
└── tmp/                ← 임시 파일 저장
```

---

## 풀이

### 단계 1: 환경 탐색
```bash
# 챌린지 디렉토리 확인
ls -la /challenge/

# flag 파일 위치 확인
ls -la /flag

# 현재 위치
pwd
```

### 단계 2: 챌린지에 필요한 파일 찾기
```bash
# 특정 이름 파일 검색
find / -name "*.txt" 2>/dev/null
find /challenge -type f 2>/dev/null

# 숨김 파일 탐색
ls -la ~
ls -la /home/hacker/
```

### 단계 3: 챌린지 실행
```bash
/challenge/run
# pwn.college{...}
```

---

## find 명령어 완전 정복

### 기본 구문
```
find [경로] [옵션] [동작]
```

### 이름으로 검색
```bash
find / -name "flag"           # 정확한 이름
find / -name "flag*"          # 와일드카드
find / -name "*.txt"          # 확장자
find / -iname "FLAG"          # 대소문자 무시
```

### 타입으로 검색
```bash
find / -type f                # 일반 파일
find / -type d                # 디렉토리
find / -type l                # 심볼릭 링크
```

### 권한으로 검색
```bash
find / -perm 777              # 정확히 777
find / -perm -4000            # SUID 비트 포함
find / -perm -2000            # SGID 비트 포함
find / -perm /o+w             # 기타 사용자 쓰기 가능
```

### 소유자로 검색
```bash
find / -user root             # root 소유
find / -user hacker           # hacker 소유
find / -group shadow          # shadow 그룹
```

### 크기로 검색
```bash
find / -size +1M              # 1MB 초과
find / -size -100k            # 100KB 미만
find / -size 4k               # 정확히 4KB
```

### 시간으로 검색
```bash
find / -mtime -1              # 1일 이내 수정
find / -newer /flag           # /flag보다 최신
find / -mmin -60              # 60분 이내 수정
```

### 검색 후 실행
```bash
find / -name "*.txt" -exec cat {} \;     # 각 파일에 cat 실행
find / -perm -4000 -exec ls -la {} \;   # SUID 파일 목록
find / -name "flag" -exec cat {} +       # 배치로 실행
```

### 오류 억제
```bash
find / -name "flag" 2>/dev/null          # 권한 오류 숨기기
find / -name "flag" 2>&1 | grep -v "Permission denied"
```

---

## 파일 내용 분석

```bash
# 파일 타입 확인
file /challenge/run
# ELF 64-bit LSB executable...

# 16진수 덤프
xxd /flag | head
hexdump -C /flag | head

# 문자열 추출 (바이너리에서)
strings /challenge/run
strings /challenge/run | grep "pwn.college"

# 파일 크기
du -sh /challenge/run
wc -c /challenge/run

# 파일 해시
md5sum /flag
sha256sum /flag
```

---

## 심볼릭 링크 탐색

```bash
# 심볼릭 링크 찾기
find / -type l 2>/dev/null

# 링크 대상 확인
ls -la /some/link
readlink /some/link
readlink -f /some/link  # 절대 경로
```

---

## 관련 개념

- [[08-Using-the-Shell]] - 쉘 기본 명령어
- [[04-The-Flag-File]] - flag 파일
- [[03-Challenge-Programs]] - 챌린지 바이너리
