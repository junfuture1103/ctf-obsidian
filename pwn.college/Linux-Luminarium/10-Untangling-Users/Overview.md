# Untangling Users - Overview

**Module:** Linux Luminarium → Untangling Users  
**문제 수:** 4개  
**주제:** 사용자 시스템, su, sudo, 권한 상승

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Becoming-Root-with-su]] | `su` |
| 2 | [[02-Other-Users-with-su]] | `su username` |
| 3 | [[03-Cracking-Passwords]] | 패스워드 크래킹 |
| 4 | [[04-Using-sudo]] | `sudo` |

---

## 핵심 개념

```bash
# su: 사용자 전환
su              # root로 전환 (패스워드 필요)
su -            # root 환경으로 전환
su username     # 다른 사용자로
su - username   # 다른 사용자 환경으로

# sudo: root 권한으로 명령 실행
sudo command    # root로 실행
sudo -l         # 허용된 명령 목록
sudo -u user command  # 특정 사용자로
sudo su         # root 쉘 획득
sudo -i         # root 로그인 쉘

# 사용자 정보
whoami          # 현재 사용자
id              # UID, GID, 그룹
groups          # 그룹 목록
cat /etc/passwd # 사용자 목록
cat /etc/shadow # 패스워드 해시 (root만)
```
