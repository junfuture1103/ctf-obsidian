# An Epic Filesystem Quest

**Module:** Linux Luminarium → Comprehending Commands  
**Challenge:** #9  
**Tags:** `find`, `filesystem`, `navigation`, `clues`

---

## 문제 설명

파일 시스템 곳곳에 숨겨진 단서(clue)를 따라가며 최종적으로 flag를 찾아야 한다.  
각 단서 파일이 다음 위치를 알려준다.

---

## 풀이 전략

### 단계 1: 첫 단서 찾기
```bash
ls /
cat /HINT  # 또는
cat /clue
```

### 단계 2: 단서 따라가기
```
HINT: The next clue is in /opt/...
```

```bash
cat /opt/some/path/CLUE
```

### 단계 3: 반복
각 단서가 다음 위치를 가리킬 때:
```bash
# 현재 위치에서 파일 확인
ls -la
cat CLUE  # 또는 cat HINT

# 히든 파일 확인
ls -la /path/
cat /path/.hidden_clue
```

### 단계 4: 최종 flag
마지막 단서가 가리키는 위치:
```bash
cat /final/location/flag
# pwn.college{...}
```

---

## 유용한 명령어

```bash
# 재귀적으로 CLUE/HINT 파일 찾기
find / -name "CLUE" 2>/dev/null
find / -name "HINT" 2>/dev/null
find / -name "*.clue" 2>/dev/null

# 숨김 파일 포함 탐색
find / -name ".*" -type f 2>/dev/null | head -20

# 최근 수정된 파일
find / -newer /challenge -type f 2>/dev/null
```

---

## 파일 시스템 탐색 패턴

```bash
# 전체 탐색 시나리오
cat /CLUE
# → /opt/secret/CLUE

cat /opt/secret/CLUE  
# → /usr/local/share/.hidden/CLUE

ls -la /usr/local/share/.hidden/
cat /usr/local/share/.hidden/CLUE
# → pwn.college{...}
```

---

## 관련 문제

- [[11-finding-files]] - find 명령어 심화
