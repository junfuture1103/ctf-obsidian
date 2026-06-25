# Implicit Relative Path

**Module:** Linux Luminarium → Pondering Paths  
**Challenge:** #4  
**Tags:** `relative-path`, `dot-slash`

---

## 문제 설명

현재 디렉토리에 있는 실행 파일을 `./`를 사용하여 실행해야 한다.  
bash는 보안상 현재 디렉토리를 자동으로 PATH에 포함시키지 않는다.

---

## 문제 상황

```bash
cd /challenge
run            # 실패! PATH에 없음
./run          # 성공! 현재 디렉토리
```

---

## 풀이

```bash
# /challenge 디렉토리로 이동
cd /challenge

# ./ 를 붙여서 현재 디렉토리의 파일 실행
./run
```

**출력:**
```
pwn.college{...}
```

---

## 왜 ./ 가 필요한가?

```bash
echo $PATH
# /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# PATH에 . (현재 디렉토리)가 없음!
# 보안 이유: 악성 프로그램이 기본 명령어를 가로채는 것 방지
```

### 예시: PATH 하이재킹 위험
```bash
# 만약 .이 PATH에 있다면:
# 악의적인 사용자가 현재 디렉토리에 ls 라는 프로그램을 만들면
# ls 실행 시 악성 코드가 실행될 수 있음
```

---

## 관련 문제

- [[05-Explicit-Relative-Path]] - 다른 상대 경로
- [[01-The-Path-to-Success]] - 절대 경로
