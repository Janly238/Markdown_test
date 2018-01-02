Tokenquery
====

## Tokenquery是什么
Token，将文本分解成更小的处理单元（令牌）
Tokenquery，查询提取令牌序列

### TokenQuery语言
```[expr_for_token1][expr_for_token2][expr_for_token3]```

### 量词
```
| ?	| 一次或根本不	| [expr_for_token]?
| *	| 零次或多次	| [expr_for_token]*
| +	| 一次或多次	| [expr_for_token]+
| {x}	| x次数	| [expr_for_token]{3}
| {x,y}	| 在x和y之间的次数	| [expr_for_token]{3,5}
```


