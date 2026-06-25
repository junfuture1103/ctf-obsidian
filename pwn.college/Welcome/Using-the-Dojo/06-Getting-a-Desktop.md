# Getting a Desktop

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Challenge:** #6  
**Tags:** `desktop`, `vnc`, `gui`, `linux`

---

## 문제 설명

pwn.college의 웹 기반 데스크톱 환경(VNC)을 시작하고 활용하는 방법을 익힌다.

---

## 핵심 개념

### pwn.college 데스크톱 환경
- **기술:** noVNC (브라우저 기반 VNC 클라이언트)
- **DE:** XFCE (경량 데스크톱 환경)
- **목적:** GUI 앱 실행, 그래픽 디버거, 복잡한 작업

---

## 풀이

### 단계 1: 데스크톱 시작
1. https://pwn.college 로그인
2. 챌린지 페이지에서 **"Start"** 클릭하여 컨테이너 시작
3. **"Desktop"** 탭 클릭

### 단계 2: 데스크톱에서 터미널 열기
- 바탕화면 우클릭 → **"Open Terminal Here"**
- 또는 하단 작업표시줄 터미널 아이콘 클릭

### 단계 3: 챌린지 실행
```bash
# 터미널에서
/challenge/run
# pwn.college{...}
```

---

## XFCE 데스크톱 기본 조작

### 터미널 단축키
| 단축키 | 기능 |
|--------|------|
| `Ctrl+Alt+T` | 새 터미널 |
| `Ctrl+Shift+C` | 복사 |
| `Ctrl+Shift+V` | 붙여넣기 |
| `Ctrl+Shift+N` | 새 탭 |

### 파일 관리자
```bash
# 터미널에서 파일 관리자 열기
thunar &

# 또는 바탕화면 우클릭 → "Open File Manager"
```

### 스크린샷
```bash
# 전체 화면
scrot screenshot.png

# 선택 영역
scrot -s screenshot.png

# xfce4-screenshooter
xfce4-screenshooter
```

---

## VNC 해상도 조정

```bash
# 현재 해상도 확인
xrandr

# 해상도 변경
xrandr -s 1920x1080
xrandr --output VNC-0 --mode 1920x1080
```

---

## 데스크톱 vs SSH 사용 비교

| 상황 | 권장 방법 |
|------|-----------|
| 텍스트 작업, 스크립팅 | SSH |
| GUI 앱 (GDB, IDA, Ghidra) | 데스크톱 |
| 파일 편집 | VSCode + SSH |
| 빠른 명령 실행 | 웹 터미널 |

---

## 데스크톱 환경에서 유용한 도구

```bash
# 텍스트 에디터
mousepad file.txt   # XFCE 기본 에디터
gedit file.txt      # GNOME 에디터 (있는 경우)

# 그래픽 디버거
# gdb with pwndbg + pwntools 시각화

# 파일 탐색
thunar              # GUI 파일 관리자
```

---

## 관련 개념

- [[05-Pasting-into-the-Desktop]] - 클립보드 사용
- [[07-Setting-Up-VSCode]] - VSCode 설정
- [[01-Connecting-over-SSH]] - SSH 접속
