# Perceiving Permissions - Overview

**Module:** Linux Luminarium → Perceiving Permissions  
**문제 수:** 8개  
**주제:** 파일 권한, SUID, SGID, Sticky Bit

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Changing-File-Ownership]] | `chown` |
| 2 | [[02-Groups-and-Files]] | `chgrp`, 그룹 |
| 3 | [[03-Fun-with-Group-Challenge]] | 그룹 멤버십 |
| 4 | [[04-Changing-Permissions]] | `chmod` |
| 5 | [[05-Executable-Files]] | 실행 권한 |
| 6 | [[06-Permission-Tweaking-Practice]] | chmod 실습 |
| 7 | [[07-Permissions-Setting-Practice]] | 권한 설정 |
| 8 | [[08-The-SUID-Bit]] | SUID |

---

## 권한 레퍼런스

```bash
# chmod
chmod 755 file     # rwxr-xr-x
chmod 644 file     # rw-r--r--
chmod u+x file     # 소유자 실행 추가
chmod go-w file    # 그룹/기타 쓰기 제거
chmod +s file      # SUID/SGID
chmod +t dir       # Sticky bit

# chown
chown user file
chown user:group file
chown -R user dir  # 재귀

# chgrp
chgrp group file

# 특수 비트
chmod u+s file     # SUID: rwsr-xr-x
chmod g+s file     # SGID: rwxr-sr-x
chmod +t dir       # Sticky: rwxrwxrwt
```

---

## 권한 표기 해석

```
-rwsr-xr-x  1  root  shadow  ...  /usr/bin/passwd
 |||------  others (r-x = 101 = 5)
 |||--- group (r-x = 5)
 |||user (rws = 4+2+1=7, s=SUID)
 |type: - (regular file)

숫자 변환:
  r = 4
  w = 2
  x = 1
  s (SUID/SGID) = 별도 비트
  t (sticky) = 별도 비트

예: 4755
  4 = SUID 비트
  7 = rwx (소유자)
  5 = r-x (그룹)
  5 = r-x (기타)
```
