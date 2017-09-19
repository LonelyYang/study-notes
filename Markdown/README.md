# 标题


# 这是 H1 
<code> # 这是 H1 </code>    
<code> # 这是 H1 # </code>    

### 这是 H3
<code> ### 这是 H3 </code>    
<code> ### 这是 H3 ### </code>    

###### 这是 H6
<code> ###### 这是 H6 </code>    
<code> ###### 这是 H6 ###### </code>    

***

# 强调

### _斜体_
<pre> *斜体*          _斜体_ </pre>  
### __粗体__  
<pre> **粗体**          __粗体__ </pre>  
### __斜粗体__  
<pre> ***斜粗体***          ___斜粗体___ </pre>    


***

# 列表
<pre>*   Red
*   Green
*   Blue</pre>

等同于：

<pre>+   Red
+   Green
+   Blue</pre>

也等同于：

<pre>-   Red
-   Green
-   Blue</pre>

多级列表
* Red
  * Green
    * Blue
```
* Red
  * Green
    * Blue
```

***

# 分隔线
<pre>* * *

***

*****

- - -

---------------------------------------</pre>

***

# 缩进

>数据结构  
>>树  
>>>二叉树  
>>>>平衡二叉树  
>>>>>满二叉树  

***

# 图片

* 行内式
<pre>![Alt text](/path/to/img.jpg "Optional title")</pre>
> 一个惊叹号 !
> 接着一个方括号，里面放上图片的替代文字
> 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上 选择性的 'title' 文字。

* 参考式
<pre>参考式的图片语法则长得像这样：

![Alt text][id]

[id]是图片参考的名称，图片参考的定义方式则和连结参考一样：

[id]: url/to/image  "Optional title attribute"</pre>

> 到目前为止， Markdown 还没有办法指定图片的宽高，如果你需要的话，你可以使用普通的 <img> 标签。

***

# 链接
```
<url>  
```
<http://www.baidu.com>  

或者  
```
[name](url)
[链接文字](链接地址)
```
[baidu](http://www.baidu.com)




