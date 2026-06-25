# Home Sweet Home

**Module:** Linux Luminarium → Pondering Paths  
**Challenge:** #6  
**Tags:** `home-directory`, `tilde`, `argument`

---

## 문제 설명

챌린지 바이너리에 인수로 전달하는 경로가 홈 디렉토리 내의 파일이어야 한다.  
`~` (tilde)의 의미와 홈 디렉토리 개념을 익힌다.

---

## 풀이

```bash
# 챌린지가 인수로 경로를 요구하는 경우
/challenge/run ~/myfile
# 또는
/challenge/run /home/hacker/myfile
```

**출력:**
```
pwn.college{...}
```

---

## ~ (Tilde) 확장

```bash
echo ~
# /home/hacker

echo ~/file
# /home/hacker/file

# 다른 사용자의 홈
echo ~root
# /root

# PATH 내 ~ 확장
cd ~
cd ~/documents
```

---

## 홈 디렉토리 관련

```bash
# 홈으로 이동 (3가지 방법 모두 동일)
cd
cd ~
cd $HOME

# 홈 디렉토리 확인
echo $HOME
# /home/hacker

# 홈 디렉토리 내용
ls ~/
ls -la ~/
```

---

## 조건 분석

챌린지가 요구하는 조건 예시:
```
1. 인수가 1개여야 함
2. 인수가 절대 경로여야 함  
3. 경로가 /home/hacker/ 로 시작해야 함
4. 파일 이름이 한 글자여야 함
```

```bash
/challenge/run ~/a   # /home/hacker/a → 조건 충족
```
