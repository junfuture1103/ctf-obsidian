# Digesting Documentation - Overview

**Module:** Linux Luminarium → Digesting Documentation  
**문제 수:** 7개  
**주제:** man 페이지, --help, 문서 읽기

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Learning-From-Documentation]] | man 기본 |
| 2 | [[02-Learning-Complex-Usage]] | 옵션 조합 |
| 3 | [[03-Reading-Manuals]] | man 페이지 탐색 |
| 4 | [[04-Searching-Manuals]] | man -k, apropos |
| 5 | [[05-Searching-For-Manuals]] | 문서 검색 |
| 6 | [[06-Helpful-Programs]] | --help 옵션 |
| 7 | [[07-Help-for-Builtins]] | help (bash 내장) |

---

## 핵심 개념

```bash
man command          # 전통적 매뉴얼
man -k keyword       # 키워드로 매뉴얼 검색
apropos keyword      # man -k와 동일
command --help       # 빠른 도움말
command -h           # 짧은 도움말
info command         # GNU info 문서
help command         # bash 내장 명령어 도움말
```
