# Matching with Wildcards

**Module:** Linux Luminarium → File Globbing  
**Challenge:** #1  
**Tags:** `glob`, `wildcard`, `asterisk`

---

## 문제 설명

`*` 와일드카드를 사용하여 `/challenge/run`을 실행해야 한다.  
특정 글로브 패턴으로 바이너리를 지정해서 실행하는 방법을 익힌다.

---

## 풀이

```bash
# * 은 임의의 문자열 매칭
/challenge/*
# 또는
/chall*/run
# 또는
/*allenge/run
```

**출력:**
```
pwn.college{...}
```

---

## * 와일드카드 동작

```bash
# 모든 파일 매칭
ls /challenge/*
echo /home/hacker/*

# 확장자 매칭
ls *.txt
ls *.py

# 패턴 결합
ls /usr/*/bin
ls /home/*/Desktop

# 중간 매칭
ls /ch*ge/run
ls *challenge*
```

### 글로브 확장 확인
```bash
# echo로 확장 결과 미리 확인
echo /challenge/*
# /challenge/run

echo /home/hacker/*.txt
# /home/hacker/a.txt /home/hacker/b.txt
```

---

## 글로빙 실패 케이스

```bash
# 매칭되는 파일 없으면 리터럴 문자열로 남음
echo /nonexistent/*
# /nonexistent/*  ← 파일 없어서 그대로 출력

# nullglob 설정하면 빈 문자열로
shopt -s nullglob
echo /nonexistent/*
# (빈 출력)
```

---

## 관련 문제

- [[02-Matching-Single-Characters]] - ? 와일드카드
- [[05-Mixing-Globs]] - 혼합 패턴
