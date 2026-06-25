# Using the Shell

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #8  
**Tags:** `bash`, `shell`, `linux-basics`, `commands`

---

## 문제 설명

Linux 쉘(bash)의 기본 사용법을 익힌다.  
CTF에서 필수적인 명령어들과 쉘 기능을 학습한다.

---

## 핵심 개념

### bash (Bourne Again SHell)
Linux의 기본 쉘. 명령어 실행, 스크립팅, 파이프라인 등을 제공한다.

---

## 풀이

### 챌린지 실행
```bash
/challenge/run
# 쉘 관련 작업을 요구하는 챌린지
# pwn.college{...}
```

---

## 필수 Linux 명령어 레퍼런스

### 파일/디렉토리 탐색
```bash
pwd              # 현재 디렉토리
ls               # 파일 목록
ls -la           # 숨김 파일 포함, 권한 표시
ls -lah          # 사람이 읽기 쉬운 크기 단위
cd /path         # 디렉토리 이동
cd ~             # 홈 디렉토리
cd -             # 이전 디렉토리
tree             # 트리 구조 표시
```

### 파일 조작
```bash
cat file         # 파일 내용 출력
less file        # 페이지 단위 보기 (q로 종료)
head -n 20 file  # 앞 20줄
tail -n 20 file  # 뒤 20줄
tail -f file     # 실시간 추적

cp src dst       # 복사
mv src dst       # 이동/이름변경
rm file          # 삭제
rm -rf dir/      # 디렉토리 삭제 (주의!)
mkdir -p a/b/c   # 디렉토리 생성 (중간 경로 포함)
touch file       # 빈 파일 생성 / 타임스탬프 갱신
```

### 검색
```bash
find / -name "flag" 2>/dev/null           # 파일명으로 검색
find / -perm -4000 2>/dev/null            # SUID 파일 검색
grep -r "pattern" /dir                   # 재귀 텍스트 검색
grep -n "pattern" file                   # 줄번호 포함
grep -i "pattern" file                   # 대소문자 무시
locate filename                          # 인덱스로 빠른 검색
which command                            # 명령어 경로
whereis command                          # 바이너리/매뉴얼 위치
```

### 프로세스 관리
```bash
ps aux           # 모든 프로세스
ps -ef           # 프로세스 상세 정보
top / htop       # 실시간 프로세스 모니터
kill PID         # 프로세스 종료 (SIGTERM)
kill -9 PID      # 강제 종료 (SIGKILL)
jobs             # 백그라운드 작업 목록
fg %1            # 포그라운드로 전환
bg %1            # 백그라운드로 전환
command &        # 백그라운드 실행
```

### 권한 관련
```bash
whoami           # 현재 사용자
id               # UID/GID 정보
sudo command     # root 권한으로 실행
su - user        # 사용자 전환
chmod 755 file   # 권한 변경
chown user file  # 소유자 변경
```

### 텍스트 처리
```bash
echo "text"      # 텍스트 출력
printf "fmt" args # 포맷 출력
wc -l file       # 줄 수 세기
sort file        # 정렬
uniq             # 중복 제거
cut -d: -f1 file # 구분자로 필드 추출
awk '{print $1}' # 패턴 처리
sed 's/old/new/g' # 텍스트 치환
tr 'a-z' 'A-Z'  # 문자 변환
xxd file         # 16진수 덤프
base64 file      # Base64 인코딩
base64 -d file   # Base64 디코딩
```

---

## 쉘 기능

### 리다이렉션
```bash
command > file       # stdout을 파일로
command >> file      # stdout 추가
command 2> file      # stderr를 파일로
command 2>&1         # stderr를 stdout으로
command > /dev/null  # 출력 버리기
command < file       # stdin을 파일에서
```

### 파이프
```bash
cmd1 | cmd2          # cmd1 출력을 cmd2 입력으로
ls -la | grep "flag" # 파이프 예시
cat file | wc -l     # 줄 수 세기
```

### 변수
```bash
VAR="value"          # 변수 설정
echo $VAR            # 변수 참조
echo ${VAR}          # 명시적 참조
export VAR           # 환경변수로 내보내기
env                  # 모든 환경변수
```

### 명령어 치환
```bash
result=$(command)    # 명령어 결과를 변수에
echo $(whoami)       # 현재 사용자 출력
```

### 조건/반복
```bash
# 조건
if [ -f file ]; then echo "exists"; fi
[ -f file ] && echo "exists"

# 반복
for i in 1 2 3; do echo $i; done
while true; do command; done
```

---

## bash 단축키

| 단축키 | 기능 |
|--------|------|
| `Ctrl+C` | 현재 명령 중단 |
| `Ctrl+Z` | 백그라운드로 |
| `Ctrl+D` | EOF / 로그아웃 |
| `Ctrl+L` | 화면 지우기 |
| `Ctrl+R` | 히스토리 검색 |
| `Ctrl+A` | 줄 시작으로 |
| `Ctrl+E` | 줄 끝으로 |
| `!!` | 이전 명령 재실행 |
| `!$` | 이전 명령의 마지막 인수 |
| `Tab` | 자동완성 |

---

## 관련 개념

- [[09-Challenge-Files]] - 파일 탐색
- [[10-Talking-to-Programs]] - 프로그램 입력
- [[04-The-Flag-File]] - 파일 권한
