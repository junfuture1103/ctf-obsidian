# Pondering PATH - Overview

**Module:** Linux Luminarium → Pondering PATH  
**문제 수:** 5개  
**주제:** $PATH 환경변수, 명령어 검색, 경로 조작

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-The-PATH-Variable]] | $PATH 이해 |
| 2 | [[02-Setting-PATH]] | PATH 설정 |
| 3 | [[03-Adding-Commands]] | PATH에 경로 추가 |
| 4 | [[04-Hijacking-Commands]] | PATH 하이재킹 |
| 5 | [[05-Hiding-Commands]] | PATH 조작 |

---

## $PATH 개념

```bash
# PATH 확인
echo $PATH
# /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 명령어 검색 순서
which ls        # /bin/ls (첫 번째 매칭)

# PATH에 경로 추가
export PATH="/my/dir:$PATH"          # 앞에 추가 (우선순위 높음)
export PATH="$PATH:/my/dir"          # 뒤에 추가

# PATH 비우기 (위험!)
export PATH=""
ls  # command not found!

# 절대 경로로 대체
/bin/ls
```

---

## 명령어 검색 우선순위

```
1. 쉘 별칭 (alias)
2. 쉘 내장 명령어 (builtin)
3. PATH에서 순서대로 검색
```

```bash
type ls          # 명령어 타입 확인
which ls         # PATH에서 찾은 위치
whereis ls       # 바이너리 + 매뉴얼 위치
command -v ls    # 스크립트에서 안전한 검색
```
