# Linking Files

**Module:** Linux Luminarium → Comprehending Commands  
**Challenge:** #12  
**Tags:** `symlink`, `ln`, `hard-link`

---

## 문제 설명

심볼릭 링크(소프트 링크) 또는 하드 링크를 사용하여 파일에 접근하는 방법을 익힌다.

---

## 풀이

챌린지가 특정 경로의 파일을 읽으려 할 때, 심볼릭 링크로 `/flag`를 가리키게 한다:

```bash
# 심볼릭 링크 생성: /challenge/expected-path → /flag
ln -s /flag /challenge/expected-path

# 챌린지 실행
/challenge/run
# → 챌린지가 /challenge/expected-path를 읽음 → /flag의 내용 출력
# pwn.college{...}
```

---

## 링크 종류

### 심볼릭 링크 (Soft Link)
```bash
ln -s /original/file /link/path
# /link/path → /original/file

# 확인
ls -la /link/path
# lrwxrwxrwx 1 hacker hacker 14 ... /link/path -> /original/file

# 원본 경로 확인
readlink /link/path
readlink -f /link/path   # 절대 경로
```

### 하드 링크
```bash
ln /original/file /link/path
# 동일한 inode를 공유, 같은 파티션에만 가능
# 디렉토리에는 사용 불가

# inode 확인
ls -lai file
stat file
```

---

## 심볼릭 링크 vs 하드 링크 비교

| 특성 | 심볼릭 링크 | 하드 링크 |
|------|------------|-----------|
| 원본 삭제 시 | 끊어짐 (dangling) | 파일 유지 |
| 다른 파티션 | 가능 | 불가능 |
| 디렉토리 | 가능 | 불가능 |
| inode | 다름 | 동일 |
| 크기 | 경로 길이 | 원본과 동일 |

---

## CTF 활용 패턴

```bash
# 챌린지가 /tmp/myfile을 읽는 경우
ln -s /flag /tmp/myfile
/challenge/run   # /tmp/myfile 읽음 → /flag 내용 반환

# 챌린지가 특정 경로에 쓰는 경우
ln -s /flag /challenge/output
/challenge/run   # /challenge/output에 쓰려 하면 → /flag 덮어쓰기 시도?
# (이 경우 write 권한 필요)
```

---

## 링크 관련 명령어

```bash
# 링크 제거
rm /link/path     # 링크만 삭제, 원본 유지

# 링크 찾기
find / -type l 2>/dev/null
find / -maxdepth 3 -type l -ls 2>/dev/null

# 끊어진 링크 찾기
find / -xtype l 2>/dev/null
```
