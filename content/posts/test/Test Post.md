+++
title = 'Test Post'
date = 2025-06-04
lastmod = 2024-11-20T18:00:00+08:00
draft = false
categories = ["test"]
tags = ["test5"]
+++
# TEST $1+1=2$
{{< notice notice-info >}} 一生疏狂尽余欢，半剖肝胆入剑寒。 剑至高危如蜀道，生逢穷途行路难。 {{< /notice >}}
{{< notice notice-warning >}} 一生疏狂尽余欢，半剖肝胆入剑寒。 剑至高危如蜀道，生逢穷途行路难。 {{< /notice >}}
{{< notice notice-tip >}} 一生疏狂尽余欢，半剖肝胆入剑寒。 剑至高危如蜀道，生逢穷途行路难。 {{< /notice >}}
{{< notice notice-note >}} 一生疏狂尽余欢，半剖肝胆入剑寒。 剑至高危如蜀道，生逢穷途行路难。 {{< /notice >}}
```
print("Hello World")
print("Hello World")
print("Hello World")
```
这是示例 {{< sidenote >}} 这是示例的侧边注解 {{< /sidenote >}}

这是示例 {{< sidenote >}} 这是示例的侧边注解 {{< /sidenote >}}

这是示例 {{< sidenote >}} 这是示例的侧边注解 {{< /sidenote >}}

这是示例 {{< sidenote >}} 这是示例的侧边注解 {{< /sidenote >}}

这是示例 {{< sidenote >}} 这是示例的侧边注解 {{< /sidenote >}}

这是示例 {{< sidenote >}} 这是示例的侧边注解 {{< /sidenote >}}

# Heading 1
## Heading 2               
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

#### 标题（用底线的形式

This is an H1
=============

This is an H2
-------------

### 字符效果和横线等
                
----

~~删除线~~ <s>删除线（开启识别HTML标签时）</s>
*斜体字*      _斜体字_
**粗体**  __粗体__
***粗斜体*** ___粗斜体___

上标：X<sub>2</sub>，下标：O<sup>2</sup> (不行)

$x^2$  $x_2$

### 引用 Blockquotes

> 引用文本 Blockquotes

引用的行内混合 Blockquotes
                    
> 引用：如果想要插入空白换行`即<br />标签`，在插入处先键入两个以上的空格然后回车即可，[普通链接](http://localhost/)。

### 锚点与链接 Links

[普通链接](http://localhost/)

[普通链接带标题](http://localhost/ "普通链接带标题")

直接链接：<https://github.com>

https://baidu.com

[锚点链接][anchor-id] 

[anchor-id]: http://www.this-anchor-link.com/

[mailto:test.test@gmail.com](mailto:test.test@gmail.com)

GFM a-tail link [@pandao](https://my.oschina.net/u/3691274)  邮箱地址自动链接 test.test@gmail.com  www@vip.qq.com

> @pandao

### 多语言代码高亮 Codes

#### 行内代码 Inline code

执行命令：`npm install marked`

### 图片 Images

Image:

![](https://pandao.github.io/editor.md/examples/images/4.jpg)

> Follow your heart.

![](https://pandao.github.io/editor.md/examples/images/8.jpg)

> 图为：厦门白城沙滩

图片加链接 (Image + Link)：

[![](https://pandao.github.io/editor.md/examples/images/7.jpg)](https://pandao.github.io/editor.md/images/7.jpg "李健首张专辑《似水流年》封面")

> 图为：李健首张专辑《似水流年》封面
                
----

### 列表 Lists

#### 无序列表（减号）Unordered Lists (-)
                
- 列表一
- 列表二
- 列表三
     
#### 无序列表（星号）Unordered Lists (*)

* 列表一
* 列表二
* 列表三

#### 无序列表（加号和嵌套）Unordered Lists (+)
                
+ 列表一
+ 列表二
    + 列表二-1
    + 列表二-2
    + 列表二-3
+ 列表三
    * 列表一
    * 列表二
    * 列表三

#### 有序列表 Ordered Lists (-)
                
1. 第一行
2. 第二行
3. 第三行

#### GFM task list

- [x] GFM task list 1
- [x] GFM task list 2
- [ ] GFM task list 3
    - [ ] GFM task list 3-1
    - [ ] GFM task list 3-2
    - [ ] GFM task list 3-3
- [ ] GFM task list 4
    - [ ] GFM task list 4-1
    - [ ] GFM task list 4-2
                
----
                    
### 绘制表格 Tables

| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机      | $1600   |   5     |
| 手机        |   $12   |   12   |
| 管线        |    $1    |  234  |
                    
First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell 

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

| Function name | Description                    |
| ------------- | ------------------------------ |
| `help()`      | Display the help window.       |
| `destroy()`   | **Destroy your computer!**     |

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |

| Item      | Value |
| --------- | -----:|
| Computer  | $1600 |
| Phone     |   $12 |
| Pipe      |    $1 |
                
----

#### 特殊符号 HTML Entities Codes

&copy; &  &uml; &trade; &iexcl; &pound;
&amp; &lt; &gt; &yen; &euro; &reg; &plusmn; &para; &sect; &brvbar; &macr; &laquo; &middot; 

X&sup2; Y&sup3; &frac34; &frac14;  &times;  &divide;   &raquo;

18&ordm;C  &quot;  &apos;

[========]

### Emoji表情 :smiley:

> Blockquotes :star:

#### GFM task lists & Emoji & fontAwesome icon emoji & editormd logo emoji :editormd-logo-5x:

- [x] :smiley: @mentions, :smiley: #refs, [links](), **formatting**, and <del>tags</del> supported :editormd-logo:;
- [x] list syntax required (any unordered or ordered list supported) :editormd-logo-3x:;
- [x] [ ] :smiley: this is a complete item :smiley:;
- [ ] []this is an incomplete item [test link](#) :fa-star: @pandao; 
- [ ] [ ]this is an incomplete item :fa-star: :fa-gear:;
    - [ ] :smiley: this is an incomplete item [test link](#) :fa-star: :fa-gear:;
    - [ ] :smiley: this is  :fa-star: :fa-gear: an incomplete item [test link](#);
 
#### 反斜杠 Escape

\*literal asterisks\*

[========]
            
### 科学公式 TeX(KaTeX)

$$E=mc^2$$

行内的公式$$E=mc^2$$行内的公式，行内的$$E=mc^2$$公式。

$$x > y$$

$$
\sqrt{3x - 1} + (1 + x)^2
$$
                    
$$\sin(\alpha)^{\theta}=\sum_{i=0}^{n}(x^i + \cos(f))$$


### 分页符 Page break

> Print Test: Ctrl + P



```
#include<stdio.h>
#include<string.h>
#include <ctype.h>
#include<stdlib.h>
int type(const char *str) {
    const char *p = str;

    if (*p == '\0') {
        return 0;
    }

    if (strncmp(p, "0x", 2) == 0 || strncmp(p, "0X", 2) == 0) {
        p += 2;

        if (*p == '\0') {
            return 0; // 只有 0x/0X 是非法的
        }

        while (*p) {
            if (!isxdigit(*p)) {
                return 0; // 包含非十六进制字符
            }
            p++;
        }

        return 2; // 合法十六进制
    }
    while (*p) {
        if (!isdigit(*p)) {
            return 0;
        }
        p++;
    }

    return 1;
}

long long dec_2_num(const char *str){
		char *endptr;
		return strtoll(str, &endptr, 10);
}
long long hex_2_num(const char *str){
		char *endptr;                                              
		return strtoll(str, &endptr, 16);         
}


int main(int argc,char *argv[]){
	if(argc != 3){
		printf("ERROR\n");
		return 0;
	}

	const char *input1 = argv[1];
	const char *input2 = argv[2];

	if (strlen(input1)>15 ||strlen(input2)>15 ){
		printf("ERROR\n");        
        return 0;  
	}

	if(!(type(input1)&&type(input2))){
		printf("ERROR\n");
                return 0;
	}
	
	long long num1,num2;
	if(type(input1)==1){
		num1=dec_2_num(input1);
	}else if(type(input1)==2){
		num1=hex_2_num(input1);
	}else{
		printf("ERROR\n");
                return 0;
	}
	if(type(input2)==1){
                num2=dec_2_num(input2);
        }else if(type(input2)==2){
                num2=hex_2_num(input2);
        }else{                             
                printf("ERROR\n");
                return 0;
        }

	printf("0x%llX %lld\n",num1+num2,num1+num2);
	return 0;
}
```
