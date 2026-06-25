# Learning From Documentation

**Module:** Linux Luminarium → Digesting Documentation  
**Challenge:** #1  
**Tags:** `man`, `documentation`, `flags`

---

## 문제 설명

챌린지 바이너리가 특정 인수나 플래그를 요구한다.  
`--help` 또는 `man` 페이지를 읽어서 올바른 사용법을 찾아야 한다.

---

## 풀이

### 단계 1: 도움말 확인
```bash
/challenge/run --help
```

출력 예시:
```
Usage: run [OPTIONS]
  -f, --flag     Print the flag
  -v, --verbose  Verbose mode
  ...
```

### 단계 2: 올바른 옵션으로 실행
```bash
/challenge/run --flag
# 또는
/challenge/run -f
```

**출력:**
```
pwn.college{...}
```

---

## man 페이지 사용법

```bash
# 기본 사용
man ls
man cat
man grep

# man 페이지 내 탐색
/pattern    # 검색 (n=다음, N=이전)
q           # 종료
G           # 끝으로
g           # 처음으로
Space       # 다음 페이지
b           # 이전 페이지
```

### man 페이지 섹션
```
1  사용자 명령어
2  시스템 콜
3  라이브러리 함수
4  장치 파일
5  파일 형식
6  게임
7  기타
8  시스템 관리 명령어
```

```bash
man 2 open    # 섹션 2의 open
man 3 printf  # 섹션 3의 printf
man -a printf # 모든 섹션
```

---

## --help vs man

| 특성 | --help | man |
|------|--------|-----|
| 속도 | 빠름 | 상대적으로 느림 |
| 상세도 | 요약 | 상세 |
| 항상 있음 | 아님 | 대부분 있음 |
| 검색 | 불가 | 가능 (/pattern) |

---

## 관련 문제

- [[06-Helpful-Programs]] - --help 옵션
- [[03-Reading-Manuals]] - man 페이지 탐색
