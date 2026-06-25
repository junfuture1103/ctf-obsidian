# Cracking Passwords

**Module:** Linux Luminarium → Untangling Users  
**Challenge:** #3  
**Tags:** `password-cracking`, `john`, `hashcat`, `shadow`

---

## 문제 설명

`/etc/shadow` 파일의 패스워드 해시를 크래킹하여 다른 사용자로 로그인한다.

---

## 풀이

### 단계 1: shadow 파일 확인
```bash
cat /etc/shadow
# root:$6$rounds=5000$...:...:...:...:...:...:...:
# hacker:!:...:...:...:...:...:...:...:
# zardus:$6$aaaa$bbbb...:...:
```

### 단계 2: 해시 추출
```bash
cat /etc/shadow | grep -v "^hacker" | grep -v "!\|*" > /tmp/hashes.txt
```

### 단계 3: John the Ripper로 크래킹
```bash
# 단어 목록으로 크래킹
john /tmp/hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

# 결과 확인
john /tmp/hashes.txt --show
```

### 단계 4: 획득한 패스워드로 su
```bash
su zardus
# Password: (크래킹된 패스워드)

# flag 획득
cat /flag
# pwn.college{...}
```

---

## /etc/shadow 형식

```
username:$type$salt$hash:lastchanged:min:max:warn:inactive:expire:
```

### 해시 타입
| prefix | 알고리즘 |
|--------|---------|
| `$1$` | MD5 |
| `$2a$` | bcrypt |
| `$5$` | SHA-256 |
| `$6$` | SHA-512 (가장 일반적) |
| `$y$` | yescrypt |

---

## 패스워드 크래킹 도구

### John the Ripper
```bash
# 설치
sudo apt install john

# 단어 목록 공격
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

# 규칙 적용
john hash.txt --wordlist=words.txt --rules

# 브루트포스
john hash.txt --incremental

# 결과 확인
john hash.txt --show
john --show --format=sha512crypt hash.txt
```

### Hashcat
```bash
# GPU 크래킹 (더 빠름)
hashcat -m 1800 hash.txt rockyou.txt    # sha512crypt ($6$)
hashcat -m 500 hash.txt rockyou.txt     # md5crypt ($1$)
hashcat -m 3200 hash.txt rockyou.txt    # bcrypt ($2$)

# 결과 확인
hashcat hash.txt --show
```

---

## /etc/passwd vs /etc/shadow

```bash
# /etc/passwd (모두 읽기 가능)
root:x:0:0:root:/root:/bin/bash
# username:password:UID:GID:comment:home:shell
# x = 패스워드가 shadow에 있음

# /etc/shadow (root만)
root:$6$...:19000:0:99999:7:::
```

---

## 관련 개념

- [[04-Using-sudo]] - sudo 권한 상승
- [[11-Perceiving-Permissions/Overview]] - 파일 권한
