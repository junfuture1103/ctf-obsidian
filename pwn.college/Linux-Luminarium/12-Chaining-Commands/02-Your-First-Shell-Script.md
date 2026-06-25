# Your First Shell Script

**Module:** Linux Luminarium → Chaining Commands  
**Challenge:** #2  
**Tags:** `shell-script`, `bash`, `shebang`

---

## 문제 설명

여러 명령어를 담은 쉘 스크립트를 작성하고 실행하는 방법을 익힌다.

---

## 풀이

### 단계 1: 스크립트 작성
```bash
# /home/hacker/solve.sh 작성
cat > /home/hacker/solve.sh << 'EOF'
#!/bin/bash
/challenge/run
EOF
```

### 단계 2: 실행 권한 부여
```bash
chmod +x /home/hacker/solve.sh
```

### 단계 3: 실행
```bash
/home/hacker/solve.sh
# pwn.college{...}

# 또는
bash /home/hacker/solve.sh
```

---

## 쉘 스크립트 기초

### Shebang (#!/...)
```bash
#!/bin/bash          # bash 인터프리터
#!/bin/sh            # POSIX sh
#!/usr/bin/env python3  # python3
#!/usr/bin/env perl  # Perl
```

### 기본 구조
```bash
#!/bin/bash
# 주석

# 변수
NAME="World"
echo "Hello, $NAME!"

# 조건
if [ -f "/flag" ]; then
    cat /flag
else
    echo "Flag not found"
fi

# 반복
for i in 1 2 3; do
    echo $i
done

# 함수
greet() {
    echo "Hello, $1!"
}
greet "hacker"
```

### 실행 방법 비교
```bash
# 방법 1: chmod +x 후 직접 실행
chmod +x script.sh
./script.sh          # shebang 라인 사용

# 방법 2: 인터프리터 명시
bash script.sh
sh script.sh
python3 script.py

# 방법 3: source (현재 쉘에서 실행)
source script.sh
. script.sh          # 동일
```

---

## 실용 스크립트 예제

### 여러 명령 순서 실행
```bash
#!/bin/bash
echo "[*] Starting challenge..."
/challenge/run
echo "[*] Done!"
```

### 출력 저장
```bash
#!/bin/bash
/challenge/run | tee /tmp/output.txt
grep "pwn.college" /tmp/output.txt
```

### 반복 시도
```bash
#!/bin/bash
for i in $(seq 1 10); do
    result=$(/challenge/run 2>&1)
    if echo "$result" | grep -q "pwn.college"; then
        echo "$result" | grep "pwn.college"
        break
    fi
    sleep 1
done
```

---

## 관련 문제

- [[04-Executable-Shell-Scripts]] - chmod +x
- [[15-Silly-Shebanigans/Overview]] - shebang 심화
