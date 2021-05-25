## 锚点

- 任意 1-6 个 **#** 标注的标题都会被添加上同名的锚点链接

  ```markdown
  	[标题1](#标题1) 
  	[标题2](#标题2) 
  	[标题3](#标题3) 
  
  	# 标题1
  	## 标题2
  	### 标题3
  ```

- 锚点跳转的标识名称，可使用任意字符，大写字母要转换成小写

  ```markdown
  	[Github](#github标题1)
  
  	### Github标题1
  ```

- 多单词锚点的空格用 **-** 代替

  ```markdown
  	[Github 标题2 Test](#github-标题2-test)
  
  	### Github 标题2 Test
  ```

- 多级序号需要去除 **.**

  ```markdown
  	[2.3. Github 标题](#23-github-标题)
  
  	### 2.3. Github 标题
  ```