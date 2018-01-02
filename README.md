Tokenquery
====
[参考文档] (https://github.com/threfo/tokenquery)  
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

### Vector向量
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
|contains_pos| 是否包含某词性 |contains_pos(njdt_requ_opt)
|contains_pos_reg| 是否包含某词性 |contains_pos_reg(njdt)


### taxonomy 字典
| 函数名 | 含义 | 例子
| ------ | ----- |-----
|tax_is_job_title|是否职位名称|
|tax_is_job_title_root|是否职位名称(根名称)|
|tax_is_skill_level| 技能等级| 熟悉、熟练、了解、精通、能够、掌握
|tax_is_jd_require_title| 是否岗位要求|岗位要求、职位要求、任职资格、招聘详情、职责要求、任职要求、就职标准
|tax_is_jd_opt_require_title| 是否可选择的标题|加分项、以下.*优先
|tax_is_jd_respons_title|岗位要求题目|工作职责、岗位职责、职位描述、职责表述、职责


JTL
====
JTL： JSON 转换语言
[参考文档] (https://github.com/AgalmicVentures/JTL)  

### 算术运算
JTL 使用与Python相同的语义支持以波兰语表示的以下运算符：

* 算术：+，-，\*，/，\*\*，%
* 比较：==，!=，<，<=，>，>=
例如：
```
"candidates $ first $ .text $ extractInt+3.0"
```

### function 函数
JTL有各种各样的内置转换。为了方便处理缺失值，除非另有说明，否则所有函数都将通过null（非常类似monad选项）。

### 基本
| 函数名 | 含义 
| ------ | ----- 
|default\<value\> | 返回输入值或第一个参数，如果输入是null（这是特殊null处理的情况下）
|defaultNan |如果输入是null，返回输入值或NaN
|isNull | 如果值是null，则返回true
|toBool |将输入值转换为布尔值。
|toFloat| 将输入值转换为浮点数，如果不是有效数字则返回null
|toInt| 将输入值转换为整数，如果不是有效整数则返回null
|toString|将输入值转换为字符串
|extractInt | 文本中的数字转成int类型的数字（十四-->14）
|toNumber | 优先转为Float类型，否则返回int类型

### Bool 布尔
```not```
反转布尔值。

### Dictionary字典
| 函数名 | 含义 
| ------ | ----- 
|keys|以列表形式返回字典的key
|values |以列表形式返回字典的值

### Hashing 哈希
JTL支持多种加密散列函数：
```md5，sha1，sha224，sha256，sha384，sha512。```
```另外，对于每种散列类型（例如）都支持HMAChmac_md5。```

### Math 数学

* 基础知识：abs，ceil，floor
* 指数：exp，lg，ln，log，sqrt
* 标志：isFinite，isNan
* 三角：sin，cos，tan
* 双曲三角：sinh，cosh，tanh
* 高级： erf

### Sequence序列
| 函数名 | 含义 
| ------ | ----- 
|count \<ELEMENT\> |返回元素出现在列表中的次数。
|first |返回列表的第一个元素，如果列表是空则返回null
|init |返回列表中除最后一个之外的所有元素
|last |返回列表的最后一个元素，如果列表是空则返回null
|rest |在第一个元素之后返回列表的其余部分
|length |返回列表的长度
|max |在列表中找到最大值
|min |在列表中找到最小值
|sorted | 返回列表的排序版本
|sum |采取列表中的值的总和
|unique|返回删除重复项的列表副本

### string串
* 转型：capitalize，lower，swapCase，upper
* 空格：lstrip，rstrip，strip 
* 搜索：find，replace，startsWith，endsWith
* 拆分/加入：join，split，lines，unlines，words，unwords

#### 转型
| 函数名 | 使用 
| ------ | -----
|lower|  s.lower()
| upper|   s.upper()
| capitalize |   s.capitalize()
| swapCase |   s.swapcase()

#### 空格
| 函数名 | 使用  
| ------ | -----
|strip|   s.strip()
|  lstrip|   s.lstrip()
| rstrip|   s.rstrip()

#### 搜索
| 函数名 | 使用  
| ------ | -----
| find |   s.find(f)
| replace |   s.replace(f, g)
| startsWith |   s.startswith(f)
| endsWith |   s.endswith(f)
| append |   (s or '') + (f or '')

#### 拆分/加入
| 函数名 | 使用
| ------ | -----
|  split|  s.split(sp)
|  lines|  s.split('\n')
|  unlines| '\n'.join(s)
|  words|   s.split(' ')
| unwords|   ' '.join(s)

### 文本操作
| 函数名 | 含义 
| ------ | ----- 
|seq_filter | 序列过滤器 
|mapper | 映射
  