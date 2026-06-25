# Silly Shebanigans - Overview

**Module:** Linux Luminarium → Silly Shebanigans  
**문제 수:** 6개  
**주제:** Shebang(#!), 스크립트 인터프리터, 실행 방법

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Shebangs]] | `#!/bin/bash` |
| 2 | [[02-Interpreted-Languages]] | Python, Ruby, Perl |
| 3 | [[03-Invoking-Python]] | `#!/usr/bin/env python3` |
| 4 | [[04-Invoking-Perl]] | `#!/usr/bin/perl` |
| 5 | [[05-Invoking-Ruby]] | `#!/usr/bin/ruby` |
| 6 | [[06-Invoking-Many-Programs]] | 다양한 인터프리터 |

---

## Shebang 형식

```bash
#!/bin/bash              # bash
#!/bin/sh                # POSIX sh
#!/usr/bin/env python3   # Python 3 (env 사용 권장)
#!/usr/bin/env python    # Python 2/3
#!/usr/bin/env perl      # Perl
#!/usr/bin/env ruby      # Ruby
#!/usr/bin/env node      # Node.js
#!/usr/bin/env php       # PHP
#!/bin/awk -f            # awk
#!/bin/sed -f            # sed
```

### `/usr/bin/env` 사용 이유
```bash
# 절대 경로 방식: 특정 위치에만 있어야 함
#!/usr/bin/python3

# env 방식: PATH에서 검색 (이식성 높음)
#!/usr/bin/env python3
# → env가 PATH에서 python3 찾아서 실행
```
