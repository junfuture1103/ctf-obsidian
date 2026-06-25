# Shell Variables - Overview

**Module:** Linux Luminarium → Shell Variables  
**문제 수:** 8개  
**주제:** 쉘 변수, 환경 변수, 특수 변수

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Printing-Variables]] | `echo $VAR` |
| 2 | [[02-Setting-Variables]] | `VAR=value` |
| 3 | [[03-Multi-Word-Variables]] | 따옴표 |
| 4 | [[04-Exporting-Variables]] | `export` |
| 5 | [[05-Printing-Exported-Variables]] | `env` |
| 6 | [[06-Storing-Command-Output]] | `$(cmd)` |
| 7 | [[07-Reading-Input]] | `read` |
| 8 | [[08-Reading-Files]] | `<` + 변수 |

---

## 변수 레퍼런스

```bash
# 설정/읽기
VAR=value          # 로컬 변수 (공백 없이!)
echo $VAR          # 값 출력
echo "${VAR}"      # 명시적 (권장)

# 환경 변수
export VAR         # 자식 프로세스에 전달
export VAR=value   # 설정과 동시에 export
env                # 모든 환경 변수 출력
printenv VAR       # 특정 변수 출력
unset VAR          # 변수 삭제

# 명령어 치환
VAR=$(command)     # 명령어 출력 저장
VAR=`command`      # 구식 문법

# 특수 변수
$0    # 스크립트 이름
$1    # 첫 번째 인수
$@    # 모든 인수 (배열)
$*    # 모든 인수 (문자열)
$#    # 인수 개수
$?    # 이전 명령어 종료 코드
$$    # 현재 쉘 PID
$!    # 마지막 백그라운드 PID
```
