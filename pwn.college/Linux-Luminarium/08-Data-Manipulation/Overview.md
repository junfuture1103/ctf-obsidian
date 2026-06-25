# Data Manipulation - Overview

**Module:** Linux Luminarium → Data Manipulation  
**문제 수:** 6개  
**주제:** 텍스트 처리 도구

---

## 문제 목록

| # | Challenge | 명령어 |
|---|-----------|--------|
| 1 | [[01-Sorting-Data]] | `sort` |
| 2 | [[02-Uniqing-Data]] | `uniq` |
| 3 | [[03-Filtering-with-tr]] | `tr` |
| 4 | [[04-Editting-Data-with-sed]] | `sed` |
| 5 | [[05-Processing-with-awk]] | `awk` |
| 6 | [[06-Combining-Tools]] | 파이프라인 |

---

## 핵심 도구 빠른 참조

```bash
# sort: 정렬
sort file                  # 알파벳 순
sort -n file               # 숫자 순
sort -r file               # 역순
sort -u file               # 중복 제거 후 정렬
sort -k2 file              # 2번째 필드 기준

# uniq: 중복 처리 (정렬된 입력 필요)
uniq file                  # 연속 중복 제거
uniq -c file               # 개수 포함
uniq -d file               # 중복된 것만
uniq -u file               # 유일한 것만

# tr: 문자 변환
tr 'a-z' 'A-Z'             # 소문자→대문자
tr -d '\n'                 # 줄바꿈 삭제
tr -s ' '                  # 연속 공백 압축

# sed: 스트림 편집기
sed 's/old/new/g'          # 치환
sed -n '5p'                # 5번째 줄만
sed '/pattern/d'           # 패턴 줄 삭제
sed -n '/start/,/end/p'    # 범위 출력

# awk: 패턴 처리
awk '{print $1}'           # 1번째 필드
awk -F: '{print $1}' /etc/passwd  # : 구분자
awk '$3 > 100'             # 조건 필터
awk '{sum+=$1} END{print sum}'  # 합계
```
