# Setting Up VSCode

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #7  
**Tags:** `vscode`, `remote-ssh`, `ide`, `development`

---

## 문제 설명

VS Code의 Remote SSH 확장을 사용해 pwn.college 서버에 직접 연결하여 IDE 환경을 구성한다.

---

## 핵심 개념

### VS Code Remote - SSH
로컬 VS Code UI를 유지하면서 원격 서버에서 파일을 편집하고 터미널을 실행하는 확장.

---

## 풀이

### 단계 1: VS Code 확장 설치
1. VS Code 실행
2. `Ctrl+Shift+X` → Extensions
3. **"Remote - SSH"** 검색 후 설치 (Microsoft 공식)

### 단계 2: SSH Config 설정
```bash
# ~/.ssh/config 파일 편집
Host pwncollege
    HostName dojo.pwn.college
    User hacker
    IdentityFile ~/.ssh/id_ed25519
    Port 22
```

### 단계 3: SSH 키 생성 및 등록
```bash
# 키 생성
ssh-keygen -t ed25519 -C "pwncollege" -f ~/.ssh/id_ed25519

# 공개키 내용 복사
cat ~/.ssh/id_ed25519.pub
```

1. https://pwn.college 로그인
2. 프로필 → **Settings** → **SSH Keys**
3. 공개키 내용 붙여넣기 후 저장

### 단계 4: VS Code로 접속
1. `Ctrl+Shift+P` → **"Remote-SSH: Connect to Host"**
2. `pwncollege` 선택 (또는 `hacker@dojo.pwn.college`)
3. 연결 완료 후 **"Open Folder"** → `/` 또는 `/home/hacker`

### 단계 5: 챌린지 실행
VS Code 내장 터미널 (`Ctrl+\``) 에서:
```bash
/challenge/run
# pwn.college{...}
```

---

## VS Code 유용한 설정

### settings.json 추천
```json
{
    "terminal.integrated.fontFamily": "MesloLGS NF",
    "editor.fontSize": 14,
    "terminal.integrated.fontSize": 13,
    "files.autoSave": "afterDelay",
    "editor.tabSize": 4,
    "editor.insertSpaces": true
}
```

### 유용한 확장 (CTF용)
```
- Remote - SSH (필수)
- Hex Editor (바이너리 분석)
- C/C++ (IntelliSense)
- Python (pwntools 자동완성)
- GitLens
```

---

## VS Code 단축키 (터미널)

| 단축키 | 기능 |
|--------|------|
| `` Ctrl+` `` | 터미널 토글 |
| `Ctrl+Shift+5` | 터미널 분할 |
| `Ctrl+Shift+\`` | 새 터미널 |
| `Ctrl+K Ctrl+C` | 주석 처리 |

---

## pwn.college 웹 VSCode

pwn.college는 웹 기반 VSCode도 제공한다:
1. 챌린지 페이지 → **"VSCode"** 탭
2. 별도 설치 없이 브라우저에서 바로 사용 가능

---

## SSH 연결 문제 해결

```bash
# 연결 테스트
ssh -v hacker@dojo.pwn.college

# known_hosts 초기화 (호스트 키 변경 시)
ssh-keygen -R dojo.pwn.college

# 특정 키로 연결
ssh -i ~/.ssh/id_ed25519 hacker@dojo.pwn.college
```

---

## 관련 개념

- [[01-Connecting-over-SSH]] - SSH 기본
- [[06-Getting-a-Desktop]] - 데스크톱 환경
- [[08-Using-the-Shell]] - 쉘 사용
