# Daring Destruction - Overview

**Module:** Linux Luminarium → Daring Destruction  
**문제 수:** 5개  
**주제:** 파일 삭제, 데이터 파괴, 안전한 삭제

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Removing-Files]] | `rm` |
| 2 | [[02-Removing-Directories]] | `rm -rf`, `rmdir` |
| 3 | [[03-Shredding-Files]] | `shred` |
| 4 | [[04-Overwriting-Files]] | `/dev/zero`, `truncate` |
| 5 | [[05-Daring-Deletion]] | 종합 |

---

## 삭제 명령어 요약

```bash
# rm: 파일 삭제
rm file                  # 단일 파일
rm -f file               # 강제 (확인 없이)
rm -r dir/               # 디렉토리 재귀 삭제
rm -rf dir/              # 강제 재귀 삭제 (주의!)
rm -i file               # 확인하며 삭제

# rmdir: 빈 디렉토리만 삭제
rmdir emptydir

# shred: 안전한 삭제 (덮어쓰기 후 삭제)
shred -u file            # 3회 덮어쓰기 후 삭제
shred -n 10 -u file      # 10회 덮어쓰기

# truncate: 파일 크기 변경
truncate -s 0 file       # 파일 내용 비우기
truncate -s 100 file     # 100바이트로

# 내용 비우기 (파일 유지)
> file                   # 리다이렉션으로 비우기
cat /dev/null > file
echo -n "" > file
```
