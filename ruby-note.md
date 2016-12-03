#Ruby 的相关知识点
###ruby 的整体风格特征:
#### %q 单引号字符串(不解释嵌套表达式#{ ... })
```
%q(string test #{time.now}) == 'string test #{time.now}'
```
#####%Q 双引号字符串(不解释嵌套表达式#{ ... })
```
%(string test #{Time.now}) == "string test #{Time.now}"
```
#####%r 正则表达式模式
```
foo = "var"
%r(/home/#{foo})  == %r(/home/#{foo})
```
####%i 符号 symbol 数组
```
 %i(one two three) == [:a, :b, :c]
```
###require, load,include 都是 Kernel 模块中的方法,他们的区别如下:

- require,load 用于包含文件,include 则用于包含模块。
- require 加载一次,load 可加载多次。
- require 加载 Ruby 代码文件时可以不加后缀名,load 加载代码文件时必须加后缀名。
- require 一般情况下用于加载库文件,而 load 用于加载配置文件。

###ruby 标识符的一些约定:

- 局部变量以小写字母或者下划线开头
- 全局变量以美元符号`$`开头。
- 实例变量以 at 符号`@`开头
- 类变量以双 at 符号`@@`开头
- 常量或类名或模块名以大写字母开头(建议常量全部用大写)。 
- 伪变量:`true`、`false`、`nil`、`__FILE__`,`__LINE__`

###Ruby 中的访问权限:

- **public**公共方法,可以被定义它的类和其子类访问,可以被类和子类的实例对象调用;

- **protected**保护方法,可以被定义它的`类和其子类`访问,不能被类和子类的实例对象直接调用,但是可以`在类和子类中指定给实例对象`;

- **private** 私有方法,可以被定义它的`类和其子类访问,私有方法不能指定对象`。

###区间:
**`..`** :两个点号创建一个闭区间

**`...`**:而三个点号创建一个右开区间(即右边界不取值

###正则表达式:
- **Ruby 中正则表达式的写法**

```
1.在/ ... /之间,要进行转义。

2.在%r{ ... }内,不用进行转义。

3.Regexp.new()内,不用进行转义。

```
- **匹配的两种方法**

```
=~ 肯定匹配, !~ 否定匹配。

=~ 表达式返回匹配到的位置索引,失败返回 nil,符号左右内容可交换

md = regexp.match(str),返回 MatchData 数组,从 0 开始,md[0]存储的是匹配到的值。 

md.pre_match:返回匹配前内容($`)。

md.post_match:返回匹配后内容($’)。

例:

p /cat/ =~ "dog and cat" #=> 8

md = /cat/.match("bigcatcomes")

puts "#{md.pre_match}->#{md[0]}<-#{md.post_match}"

```
- **替换**

```
sub(): 只替换第一次匹配
gsub(): 会替换所有的匹配,没有匹配到返回原字符串的副本。
str = "ABDADA"
new_str = str.sub(/A/, "*")
new_str2 = str.gsub(/A/, "*")
p new_str #=> "*BDADA"
p new_str2 #=> "*BD*D*"

注意：
1.如果想修改原始字符串用 sub!()和 gsub!(),没有匹配到返回 nil。
2.方法后面还可以跟 block,对匹配的字符串进行操作

例:
	a='quick brown fox'
		result=a.gsub(/[aeiou]/) do | v |
		v.upcase 
	end
	p result # => "qUIck brOwn fOx"
```
- **分组匹配**

```
Ruby 的分组匹配与其它语言差别不大,分组匹配表达式是对要进行分组的内容加()。 对于匹配到的结果,可以用系统变量#$1,#$2,...索引,也可用 matchData 数组来索引,索引值从 $1 开始。

￼￼	md = /(\d\d):(\d\d)(..)/.match("12:50am")
	puts "Hour is #$1, minute #$2"
	puts "Hour is #{md[1]}, minute #{md[2]}"
	
```

- **匹配所有**
	
	match():只能匹配一次
	
	scan():匹配所有
	
	示例:
	
	```
	result="abcabcabz".scan(%r{abc}) 
	
	p result #=> ["abc", "abc"]
	result.each{|item|
		puts item
	}				#=>输出 2 行 abc
	
	result="abcabcabz".match(%r{abc}) p result[0]          #=> ["abc"]
	```
- **贪婪匹配 vs 懒惰匹配**

	**贪婪匹配:尽可能多匹配,正则默认是贪婪匹配**
	
	```
	a.*b 它将会匹配最长的以 a 开始,以 b 结束的字符串。 
	对于 aabab 的匹配结果是 aabab。 
	result="aabab".match(/a.*b/)
	p result[0] #=> "aabab"
	```
	
	**懒惰匹配:尽可能少匹配**
	
	```
	a.*?b 对于 aabab 的匹配结果是 aab 和 ab。
	result="aabab".scan(%r{a.*?b})
	p result #=> ["aab", "ab"]
	```
###Ruby 哈希 hash 表操作

	**hash 的定义**

	```
	lst={:key1 => value1,:key2 => value2, :key3 => value3,......}
	
	```
	**hash 的读取、赋值**
	
	```
	p lst[:key2]
  	lst[:key4]='jack' 
  	p lst[:key4]
   
   ```
   
   **hash 的键或值个数**
   
   ```
   	p lst.keys.size
	p lst.keys.count 
	p lst.values.size 
	p lst.values.count
	
   ```
   
   **hash 的遍历**
   
   ```
   lst.each{ | key, value | puts "#{ key }=>#{ value }" }
   ```
###Ruby 数组的操作

	**创建一个Array对象**
	
	```
Ruby 的数组自动增长,同时增加他们的元素。
创建数组:有许多方法来创建或初始化数组。
一种方法是用新的类方法:
names = Array.new
在创建阵列时,您可以设置一个数组的大小:
names = Array.new(2) #=> [ nil, nil ]
该数组 names 现在 2 个元素,值都为 nil。你可以返回一个数组的大小或长度的方法:
months.size # This returns 2
months.length # This also returns 2
例:

	names = Array.new(4, "mac")
	puts "#{names}" #=> ["mac", "mac", "mac", "mac"] nums = 	Array.new(10) { | e | e = e * 2 }
	puts "#{nums}" #=> [0, 2, 4, 6, 8, 10, 12, 14, 16, 18] nums = 	Array[1, 2, 3, 4,5]
	p nums #=> [1, 2, 3, 4, 5]
	digits = Array(0..9)
	puts "#{digits}" #=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
￼￼	array=Array[1,2,3,4,5]
	array << 6 << 7 << 8 #向数组中追加元素,或 	array.push(6).push(7).push(8) parray #=>[1,2,3,4,5,6,7,8]
	array=%W(ab cd efg)
	parray.include?("ab") #=>true
	array.each_with_index do | arr, index |
	p arr
	p index end
	a=[1,2,3,5,7,9]
	b=[2,4,6,8,10]
	#两数组相连(不去重)
	p(a+b) #=>[1,2,3,5,7,9,2,4,6,8,10]
	#a 数组中的元素减去 b 数组中与之相同的元素 p (a-b) #=> [1, 3, 5, 7, 9] 	#(并集)除去两个数组中相同的元素
	p(a|b) #=>[1,2,3,5,7,9,4,6,8,10] #(交集)只有两个数组中都相同的元素 	p(p&b) 		#=>false
	
	```
	**创建一个 Array 对象的实例**
	
	```
	Array.[](...) 或 Array[...] 或 [...] 或 Array.new(n) { | x | x = 初始值 }
	1.数组的定义
		array=[1,2,3,4,5,6] array=Array.[](1,2,3,4,5) 		array=Array[1,2,3,4,5] i=1
		Array.new(4) { | x | x += i}
		p array #=> [1, 2, 3, 4, 5]
	2.数组的读取、赋值
		p array[0] array[4]='jack' p array[4]
	3.数组的个数
		p array.size
		p array.count 4数组的遍历(index 从 0 开始计数)
		array.each{ | item | puts item } 
		或 
		array.each_with_index{ | item,index | 
			puts “#{index}: #{item}” 
		} 
	```
   
