# Pasting into the Desktop

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #5  
**Tags:** `desktop`, `clipboard`, `vnc`, `linux-gui`

---

## 문제 설명

pwn.college의 웹 기반 데스크톱 환경에 클립보드로 텍스트를 붙여넣는 방법을 익힌다.  
VNC 기반 웹 터미널에서 복사/붙여넣기 방법이 일반 터미널과 다르다.

---

## 핵심 개념

### pwn.college 접속 방식
1. **Web Terminal** — 브라우저에서 터미널만 사용
2. **Web Desktop** — VNC 기반 전체 GUI 데스크톱
3. **SSH** — 로컬 터미널에서 SSH 접속
4. **VSCode** — Remote SSH 확장으로 IDE 사용

### 웹 데스크톱 (VNC) 클립보드
VNC 환경에서는 일반적인 `Ctrl+C` / `Ctrl+V`가 그대로 작동하지 않는다.

---

## 풀이

### 방법 1: 웹 데스크톱 사용 시 클립보드

1. pwn.college 웹사이트에서 **Desktop** 탭 클릭
2. VNC 뷰어 좌측 패널 클릭 (보통 화살표 아이콘)
3. **Clipboard** 섹션에 텍스트 붙여넣기
4. 데스크톱 내 터미널에서 `Ctrl+Shift+V` 또는 중간 클릭(마우스 휠)으로 붙여넣기

### 방법 2: noVNC 클립보드 패널
```
noVNC 좌측 패널 → 클립보드 아이콘 클릭 → 텍스트 입력 → 적용
```

### 방법 3: SSH로 우회 (권장)
클립보드 문제를 완전히 피하려면 SSH 접속 사용:
```bash
ssh hacker@dojo.pwn.college
# 로컬 터미널에서 일반적인 복사/붙여넣기 가능
```

### 단계별 풀이
```bash
# 데스크톱 터미널 열기 (우클릭 → Terminal)
# 챌린지 실행
/challenge/run

# 클립보드로 복사할 명령어나 flag 텍스트를 붙여넣어야 하는 경우
# VNC 클립보드 패널 활용
```

---

## 웹 데스크톱 단축키

| 단축키 | 기능 |
|--------|------|
| `Ctrl+Alt+Shift` | noVNC 사이드 패널 열기 |
| `Ctrl+Shift+V` | 터미널에 붙여넣기 |
| 마우스 중간 버튼 | X11 클립보드 붙여넣기 |
| `Ctrl+C` | 복사 (터미널에서는 인터럽트!) |
| `Ctrl+Insert` | 복사 (터미널) |
| `Shift+Insert` | 붙여넣기 (터미널) |

### 터미널에서의 복사/붙여넣기
```
복사: Ctrl+Shift+C 또는 마우스로 선택
붙여넣기: Ctrl+Shift+V 또는 Shift+Insert 또는 마우스 중간 버튼
```

---

## X11 클립보드 vs 시스템 클립보드

Linux에는 두 개의 클립보드가 있다:
- **PRIMARY (X11):** 마우스 선택 시 자동 복사, 중간 버튼으로 붙여넣기
- **CLIPBOARD:** `Ctrl+C`로 복사, `Ctrl+V`로 붙여넣기

```bash
# xclip으로 클립보드 조작
echo "text" | xclip -selection clipboard
xclip -selection clipboard -o

# xdotool로 붙여넣기 자동화
xdotool type "text to paste"
```

---

## 관련 개념

- [[01-Connecting-over-SSH]] - SSH 접속 (클립보드 문제 없음)
- [[06-Getting-a-Desktop]] - 데스크톱 환경
- [[07-Setting-Up-VSCode]] - VSCode 사용 (가장 편리)
