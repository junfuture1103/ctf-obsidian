# Detach and Attach

**Module:** Linux Luminarium → Terminal Multiplexing  
**Challenge:** #1  
**Tags:** `tmux`, `detach`, `attach`, `session`

---

## 문제 설명

tmux 세션에서 챌린지를 실행하고, detach한 후 다시 attach하여 flag를 획득한다.

---

## 풀이

### 단계 1: tmux 세션 시작
```bash
tmux new -s challenge
```

### 단계 2: 챌린지 실행
```bash
/challenge/run
# (대기 중이거나 백그라운드에서 실행 중)
```

### 단계 3: Detach (세션 유지하며 나오기)
```
Ctrl+b d
```

### 단계 4: 다시 Attach
```bash
tmux attach -t challenge
# 또는
tmux a -t challenge
# 또는 (세션 하나면)
tmux attach
```

**출력:**
```
pwn.college{...}
```

---

## tmux 완전 가이드

### 세션 관리
```bash
# 새 세션
tmux                    # 이름 없이
tmux new -s myname      # 이름 있게
tmux new-session -s name -d  # 백그라운드로

# 세션 목록
tmux ls
tmux list-sessions

# 세션 연결
tmux attach             # 마지막 세션
tmux attach -t name     # 특정 세션
tmux a -t 0            # 번호로

# 세션 종료
tmux kill-session -t name
exit  # tmux 내부에서 (세션 종료)
```

### 윈도우 관리
```
Ctrl+b c   새 윈도우 생성
Ctrl+b ,   윈도우 이름 변경
Ctrl+b &   윈도우 닫기 (확인)
Ctrl+b n   다음 윈도우
Ctrl+b p   이전 윈도우
Ctrl+b 0-9 번호로 이동
Ctrl+b w   윈도우 목록 (화살표로 이동)
```

### 패인(Pane) 관리
```
Ctrl+b %   세로 분할
Ctrl+b "   가로 분할
Ctrl+b →←↑↓  패인 이동
Ctrl+b o   순서대로 패인 이동
Ctrl+b q   패인 번호 표시
Ctrl+b x   현재 패인 닫기
Ctrl+b z   현재 패인 최대화/복원
Ctrl+b {   패인 왼쪽으로 이동
Ctrl+b }   패인 오른쪽으로 이동
```

### 스크롤/복사
```
Ctrl+b [   스크롤 모드 진입
PgUp/PgDn  스크롤
q          스크롤 모드 종료
Space      복사 시작
Enter      복사 완료
Ctrl+b ]   붙여넣기
```

---

## CTF에서 tmux 활용

```bash
# 여러 창에서 동시 작업
tmux new -s ctf

# 창 1: exploit 실행
# 창 2: 바이너리 분석 (gdb)
# 창 3: 파일 편집

# 세션 유지하며 SSH 종료 후 재연결
# → SSH 끊겨도 tmux 세션 유지됨!
```

---

## screen (대안)

```bash
screen -S name      # 새 세션
screen -r name      # 재연결
screen -ls          # 목록
Ctrl+a d            # detach
Ctrl+a c            # 새 창
Ctrl+a n/p          # 이전/다음 창
```
