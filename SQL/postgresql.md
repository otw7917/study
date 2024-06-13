# postgresql

> 오픈소스, rdbms ✅, vercel, supabase에서 사용중

## installation 라고 쓰고 brew 사용법과 man.....

`brew install postgresql@15` : @버전정보 ~ 16
`brew services start postgresql@15`

이후 `psql postgres`

### psql command not found ❌

- 원인 : postgresql@15의 경우 keg-only, /opt/homebrew에 symlinks가 추가 되지 않았음.

- `~/.zshrc` 에 PATH 추가해주기
  `echo 'export PATH="/opt/homebrew/opt/postgresql@15/bin:$PATH"' >> ~/.zshrc`

#### 참고

- - 심볼릭 링크가 어디있는지 확인하기  
    `brew --prefix` : /opt/homebrew (apple silicon chip)

- - formulae 제대로 설치 되어 있는지 확인하기
    `brew list [formulae]`
    `brew info [formulae]`

- - `man` man으로 cli 도움받기.
    `ln -s [original] [symlinks]` 심볼릭 링크 생성 -s option / default 는 하드링크

- - 하드링크 vs 심볼릭링크
    | 특징 | 하드링크 | 심볼릭링크 |
    | --------------- | -------------------------------- | -------------------------- |
    | 파일시스템 | 같은 파일시스템내에서만 사용가능 | 다른 파일시스템과 사용가능 |
    | 링크대상 | 파일에만 | 파일 & 폴더 참조가능 |
    | 원본파일 삭제시 | 작동 ✅ | 작동 ❌ |
