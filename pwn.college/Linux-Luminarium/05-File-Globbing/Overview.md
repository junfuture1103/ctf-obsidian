# File Globbing - Overview

**Module:** Linux Luminarium → File Globbing  
**문제 수:** 10개  
**주제:** 와일드카드 패턴 매칭

---

## 문제 목록

| # | Challenge | 패턴 |
|---|-----------|------|
| 1 | [[01-Matching-with-Wildcards]] | `*` |
| 2 | [[02-Matching-Single-Characters]] | `?` |
| 3 | [[03-Matching-Character-Classes]] | `[abc]` |
| 4 | [[04-Matching-Paths-with-Wildcards]] | 경로 + `*` |
| 5 | [[05-Mixing-Globs]] | 혼합 패턴 |
| 6 | [[06-Glob-Exclusions]] | `[!abc]` |
| 7 | [[07-Ranges]] | `[a-z]` |
| 8 | [[08-Brace-Expansion]] | `{a,b,c}` |
| 9 | [[09-Complex-Brace-Expansion]] | `{1..10}` |
| 10 | [[10-Applying-Globbing]] | 종합 |

---

## 글로빙 패턴 레퍼런스

```
*         임의의 0개 이상 문자
?         정확히 1개의 임의 문자
[abc]     a, b, c 중 하나
[a-z]     a부터 z까지 (범위)
[!abc]    a, b, c가 아닌 것
[^abc]    a, b, c가 아닌 것 ([!abc]와 동일)
{a,b,c}   a, b, c 중 하나 (브레이스 확장)
{1..10}   1부터 10까지 (범위 확장)
```

---

## 주의: 글로빙 vs 정규식

글로빙은 쉘에서 파일명 매칭용, 정규식과 다르다:

| 패턴 | 글로빙 | 정규식 |
|------|--------|--------|
| `*` | 임의의 0개 이상 | 앞 문자 0개 이상 반복 |
| `?` | 임의 1개 | 앞 문자 0 또는 1개 |
| `.` | 리터럴 `.` | 임의 1개 문자 |
| `[abc]` | 동일 | 동일 |
