# Removing Files

**Module:** Linux Luminarium → Daring Destruction  
**Challenge:** #1  
**Tags:** `rm`, `delete`, `file-removal`

---

## 문제 설명

특정 파일을 삭제해야 챌린지가 통과된다.

---

## 풀이

```bash
# 챌린지 실행하여 삭제할 파일 확인
/challenge/run
# "Please delete /home/hacker/delete_me to get the flag"

# 파일 삭제
rm /home/hacker/delete_me

# 다시 실행
/challenge/run
# pwn.college{...}
```

---

## rm 명령어 심화

### 기본 사용
```bash
rm file                  # 단일 파일
rm file1 file2 file3     # 여러 파일
rm *.txt                 # 글로브 패턴
rm -v file               # 삭제 내용 출력
```

### 디렉토리 삭제
```bash
rmdir emptydir           # 빈 디렉토리만
rm -r dir/               # 재귀 삭제
rm -rf dir/              # 강제 재귀 삭제
rm -rI dir/              # 각 파일 확인하며 재귀 삭제
```

### 안전 옵션
```bash
rm -i file               # 삭제 전 확인
rm -I dir/               # 3개 이상 파일 시 한 번만 확인
rm --preserve-root /     # / 삭제 방지 (기본값)
```

---

## 삭제 불가 상황

### 권한 없는 파일
```bash
rm /root/file
# rm: cannot remove '/root/file': Permission denied

sudo rm /root/file  # sudo 사용
```

### 읽기 전용 파일 (쓰기 권한 없음)
```bash
chmod 444 file
rm file
# rm: remove write-protected regular file 'file'? y  ← 강제 확인
rm -f file  # 강제 삭제
```

### 사용 중인 파일
```bash
# 실행 중인 바이너리도 삭제 가능 (inode 참조)
# 프로세스가 종료되면 실제 삭제됨
```

---

## 삭제된 파일 복구

```bash
# ext4 파일 시스템
# foremost, photorec으로 복구 시도
sudo foremost -t all -i /dev/sda1 -o /tmp/recovered

# inode로 복구 (빠른 삭제 후)
ls -lai /dir  # inode 번호 확인
debugfs /dev/sda1 -R "undel <inode>"
```

---

## 관련 개념

- [[02-Removing-Directories]] - 디렉토리 삭제
- [[03-Shredding-Files]] - 안전한 삭제
