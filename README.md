Tokenquery
====

## Tokenquery是什么
* Token，将文本分解成更小的处理单元（令牌）
* STokenquery，查询提取令牌序列

### TokenQuery语言
```[expr_for_token1][expr_for_token2][expr_for_token3]```

### 量词
|符号 | 含义 | 例子
|------ |-----|-----
| ?	| 一次或根本不	| [expr_for_token]? 
| *	| 零次或多次	| [expr_for_token]* 
 |+	| 一次或多次	| [expr_for_token]+ 
 |{x}	| x次数	| [expr_for_token]{3} 
 |{x,y}	| 在x和y之间的次数	| [expr_for_token]{3,5}  


### string 字符串操作。
| 函数名 | 含义 | 例子
| ------ | ----- | -----
|str_eq	 |字符串等于额外的设置字符串	|[str_eq(Obama)] ， [pos:str_eq(VBZ)]
|str_reg	|字符串匹配额外的设置字符串提供的正则表达式	|[str_req(an?)]， [pos:str_eq(V.*)]
|str_len	|字符串的长度与额外设置字符串的值相比较 |（==，>，<，!=，>=，<=）	[str_len(=12)]，[ner:str_len(>6)]，[str_len(!=2)]

### int 算术操作

| 函数名 | 含义 | 例子
| ------ | ----- | -----
|int_value	|转为整数，并可以增加额外的算法操作 |（==，>，<，!=，>=，<=）	[int_value(==5)]，[month:int_value(>1)]，[year:int_value(>1990)]
|int_e	|转为整数，并检查是否等于括号里面的数字|	[int_value(5)] ， [month:int_value(1)]
|int_g	|大于，相当于int_value(>X)	|[month:int_g(1)]
|int_l	|小于，相当于 int_value(<X) 	|[month:int_l(6)]
|int_ne	| 不等于，相当于int_value(!=X)	|[int_ne(13)]
|int_le	|小于等于，相当于int_value(<=X)	|[int_le(12)]
|int_ge	|大于等于，相当于 int_value(>=X)	|[int_ge(0)]

### web  捕捉web模式
| 函数名 | 含义 | 例子
| ------ | ----- | -----
|web_is_url	|该字符串是一个网址	|[text:web_is_url()] ， [freebase_id:web_is_url()]
|web_is_email	|该字符串是一个电子邮件	|[text:web_is_email()] ， [contact:web_is_email()]
|web_is_emoji	|字符串是表情符号或emojicon	|[text:web_is_emoji()]
|web_is_hex_code	|该字符串是一个十六进制代码	|[color:web_is_hex_code()]
|web_is_hashtag	|该字符串是一个hashtag	|[tag:web_is_hashtag()]

### Date日期
| 函数名 | 含义 | 例子
| ------ | ----- | -----
|date_is	|日期与括号内的字符串相同	|[date:date_is(2008-09-15T15:53:00)]
|date_is_after	|日期是在括号内日期之后|	[date:date_is_after(2008-09-15)]
|date_is_before	|日期在在括号内的日期之前|	[date:date_is_before(2008-09-15)]
|date_y_is	|日期的年份等于括号内的年份|	[date:date_y_is(2008)]
|date_m_is	|日期的月份等于括号内的月份|	[date:date_m_is(9)]， [date:date_m_is(09)]
|date_d_is	|日期的天数等于括号内的天数|	[date:date_y_is(15)]

### 向量
| 函数名 | 含义 | 例子
| ------ | ----- | -----
| change_string_to_vector| 逗号分隔，忽略空格，每个单元转为float类型|
|vec_cos_sim	|两个向量之间的余弦相似性	|[word2vec:vec_cos_sim([1, 0, -2, 1.5]>0.5)]
|vec_cos_dist	|两个向量之间的余弦距离|	[word2vec:vec_cos_dist([1, 0, -2, 1.5]==0)]
|vec_man_dist	|曼哈顿两个向量之间的距离|	[word2vec:vec_man_dist([1, 0, -2, 1.5]>=10)]

### 复合表达式
可以用多个基本表达式，组合元素。基本表达式：与and，或or，非！。	
* [!pos:str_reg(V.*)]意味着它不是一个任何标记的动词。  		
* [pos:str_reg(V.*)&!str_eq(is)]匹配任何动词并且不是is。您可以使用圆括号来更改优先级。
```
!X and Y        <=>   ( (!(X)) and Y )
!(X and Y)      <=>   ( !(X and Y) )
!(X and Y) or Z <=>   ( ( !(X and Y) ) or Z )
(X and Y) or Z  <=>   ( ( X and Y) or Z )
X and Y or Z    <=>   ( X and (Y or Z) )
```

### location 位置
| 函数名 | 含义 | 例子
| ------ | ----- | -----
|sentence_index | 检查索引的范围|sentence_index(<20%),sentence_index(<3)
|is_in_sentence |判断是否在句子中|is_in_sentence (True)
|is_in_paragraph| 判断是否在段落中|is_in_paragraph(ptitle)
|is_in_section|判断是否在章节中|is_in_section(requ)


### taxonomy 字典
| 函数名 | 含义 | 例子
| ------ | ----- |-----
|tax_is_job_title|是否职位名称|
|tax_is_job_title_root|是否职位名称(根名称)|
|tax_is_skill_level| 技能等级| 熟悉、熟练、了解、精通、能够、掌握
|tax_is_jd_require_title| 是否岗位要求|岗位要求、职位要求、任职资格、招聘详情、职责要求、任职要求、就职标准
|tax_is_jd_opt_require_title| 是否可选择的标题|加分项、以下.*优先
|tax_is_jd_respons_title|岗位要求题目|工作职责、岗位职责、职位描述、职责表述、职责