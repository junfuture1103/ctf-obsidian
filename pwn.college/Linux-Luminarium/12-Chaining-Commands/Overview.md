# Chaining Commands - Overview

**Module:** Linux Luminarium → Chaining Commands  
**문제 수:** 12개  
**주제:** 명령어 연결, 조건부 실행, 서브쉘

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Chaining-with-Semicolons]] | `;` |
| 2 | [[02-Your-First-Shell-Script]] | 쉘 스크립트 |
| 3 | [[03-Redirecting-Script-Output]] | 스크립트 + 리다이렉션 |
| 4 | [[04-Executable-Shell-Scripts]] | `chmod +x` |
| 5 | [[05-Conditional-Execution]] | `&&`, `\|\|` |
| 6 | [[06-And-Chains]] | `&&` 체인 |
| 7 | [[07-Or-Chains]] | `\|\|` 체인 |
| 8 | [[08-Mixing-Ands-and-Ors]] | 혼합 |
| 9 | [[09-Shell-Scripting]] | 스크립트 작성 |
| 10 | [[10-Subshells]] | `()` 서브쉘 |
| 11 | [[11-Command-Substitution]] | `$()` |
| 12 | [[12-Nesting-Command-Substitution]] | 중첩 치환 |

---

## 연산자 요약

```bash
# 순차 실행
cmd1 ; cmd2          # cmd1 성공 여부 무관
cmd1 && cmd2         # cmd1 성공 시만 cmd2
cmd1 || cmd2         # cmd1 실패 시만 cmd2

# 서브쉘
(cmd1 ; cmd2)        # 서브쉘에서 실행 (변수 격리)
$(cmd)               # 출력을 변수로

# 조건
[ condition ] && cmd # 조건 참이면 실행
[ -f file ] && cat file

# 종료 코드
$?                   # 이전 명령 종료 코드
true ; echo $?       # 0 (성공)
false ; echo $?      # 1 (실패)
```
