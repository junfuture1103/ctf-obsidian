# Connecting over SSH

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #1  
**Tags:** `ssh`, `linux-basics`

---

## 문제 설명

pwn.college에 SSH로 접속하는 방법을 익히는 첫 번째 문제.  
웹사이트의 VSCode 또는 데스크톱 터미널을 통해 접속하거나, 직접 SSH 클라이언트를 사용한다.

---

## 핵심 개념

### SSH (Secure Shell)
원격 서버에 암호화된 연결로 접속하는 프로토콜.

```
ssh [옵션] [사용자@]호스트
```

### pwn.college SSH 접속법

```bash
ssh -p 22 hacker@dojo.pwn.college
```

- **사용자명:** `hacker`
- **호스트:** `dojo.pwn.college`
- **포트:** 기본 22

### SSH 키 설정 (권장)

```bash
# 키 생성
ssh-keygen -t ed25519 -C "pwncollege"

# 공개키 복사 (pwn.college 설정 페이지에 등록)
cat ~/.ssh/id_ed25519.pub
```

---

## 풀이

### 방법 1: 웹 터미널 사용
1. https://pwn.college/welcome/ 접속
2. 우측 상단 "Start" 클릭
3. 챌린지 시작 후 웹 터미널 사용

### 방법 2: SSH 직접 접속
```bash
# SSH 접속
ssh hacker@dojo.pwn.college

# 접속 성공 후 flag 확인
cat /flag
```

### Flag 획득
접속에 성공하면 flag가 출력되거나 `/flag` 파일에 저장되어 있음.

```bash
cat /flag
# pwn.college{...}
```

---

## 주요 SSH 옵션

| 옵션 | 설명 |
|------|------|
| `-p <port>` | 포트 지정 |
| `-i <key>` | 개인키 파일 지정 |
| `-v` | 디버그 출력 |
| `-L <local>:<host>:<remote>` | 로컬 포트 포워딩 |
| `-D <port>` | SOCKS 프록시 |

---

## 관련 개념

- [[02-Your-First-Flag]] - flag 파일 읽기
- [[07-Setting-Up-VSCode]] - VSCode SSH 연결

---

## 참고

- pwn.college SSH 설정: https://pwn.college 계정 설정 > SSH Keys
- SSH 공식 문서: `man ssh`
