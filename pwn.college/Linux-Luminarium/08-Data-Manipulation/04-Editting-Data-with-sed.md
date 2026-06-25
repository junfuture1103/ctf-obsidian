# Editing Data with sed

**Module:** Linux Luminarium → Data Manipulation  
**Challenge:** #4  
**Tags:** `sed`, `stream-editor`, `text-processing`

---

## 문제 설명

`sed`를 사용하여 챌린지 출력 데이터를 변환하거나 필터링하여 flag를 추출한다.

---

## 풀이

```bash
# 특정 패턴을 다른 것으로 치환
/challenge/run | sed 's/ENCODED/DECODED/g'

# 특정 줄만 출력
/challenge/run | sed -n '/pwn.college/p'

# 패턴 추출
/challenge/run | sed -n 's/.*\(pwn\.college{[^}]*}\).*/\1/p'
```

**출력:**
```
pwn.college{...}
```

---

## sed 완전 정복

### 기본 구문
```
sed [옵션] '명령어' [파일]
```

### 치환 (s 명령)
```bash
sed 's/pattern/replacement/'        # 첫 번째만
sed 's/pattern/replacement/g'       # 모두
sed 's/pattern/replacement/2'       # 두 번째만
sed 's/pattern/replacement/gi'      # 대소문자 무시
sed 's/pattern/replacement/p'       # 치환 후 출력

# 구분자 변경 (경로에 / 포함 시)
sed 's|/old/path|/new/path|g'
sed 's#/old#/new#g'
```

### 주소 지정
```bash
sed '5s/old/new/'                   # 5번째 줄
sed '2,5s/old/new/'                 # 2~5번째 줄
sed '/pattern/s/old/new/'          # 패턴 있는 줄
sed '/start/,/end/s/old/new/'      # 범위 내 줄
```

### 출력/삭제
```bash
sed -n '5p'                         # 5번째 줄만 출력
sed -n '2,5p'                       # 2~5번째 줄
sed -n '/pattern/p'                 # 패턴 줄 출력
sed '5d'                            # 5번째 줄 삭제
sed '/pattern/d'                    # 패턴 줄 삭제
sed '/^$/d'                         # 빈 줄 삭제
```

### 삽입/추가
```bash
sed '3i\새 줄'                      # 3번째 줄 앞에 삽입
sed '3a\새 줄'                      # 3번째 줄 뒤에 추가
sed '/pattern/i\새 줄'              # 패턴 줄 앞에
```

### 정규식 그룹 참조
```bash
# \(...\) 캡처 그룹, \1 참조
echo "2024-01-15" | sed 's/\([0-9]*\)-\([0-9]*\)-\([0-9]*\)/\3\/\2\/\1/'
# 15/01/2024

# 확장 정규식 (-E)
echo "hello world" | sed -E 's/(hello) (world)/\2 \1/'
# world hello
```

---

## CTF에서 sed 활용

```bash
# base64 인코딩 제거 후 디코딩
/challenge/run | sed 's/[^A-Za-z0-9+/=]//g' | base64 -d

# flag 패턴 추출
output=$(./exploit)
echo "$output" | sed -n 's/.*\(pwn\.college{[^}]*}\).*/\1/p'

# 16진수를 아스키로
echo "41 42 43" | sed 's/ //g' | xxd -r -p
```
