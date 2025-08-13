`grep -R -i "flag{[^}]\+}" .`

| Flag             | What It Does                       |
| ---------------- | ---------------------------------- |
| `-i`             | Case-insensitive search            |
| `-v`             | Invert match (non-matching lines)  |
| `-w`             | Match whole words only             |
| `-r`             | Recursive directory search         |
| `-n`             | Show line numbers                  |
| `-c`             | Count matches                      |
| `-o`             | Show only matching part of line    |
| `-A`, `-B`, `-C` | Show context around matches        |
| `-l` / `-L`      | List files with/without matches    |
| `-E`, `-e`       | Extended regex / multiple patterns |
| `-x`             | Exact line matching                |
| `-R`             | Recursive                          |

Some regex:

|Token|Meaning|
|---|---|
|`.`|Matches any character (except newline)|
|`\w`, `\d`, `\s`|Word, digit, whitespace respectively|
|`[^...]`|Negated character class|
|`^`, `$`|Start and end of string anchors|
|`*`, `+`, `?`, `{n}`, etc.|Quantifiers|
|`(...)`|Capture group|
|`(?:...)`|Non-capturing group|
|`(?=...)`|Positive lookahead|
|`(?!...)`|Negative lookahead|