代码分析

1. $num=$_GET['num'];：读取URL中GET传参num的值。

2. !is_numeric($num)：is_numeric()用来检测变量是否为数字或数字字符串。只有变量不是数字/数字字符串，才能进入这个代码块。

3. 内层 $num == 1：PHP == 是弱类型比较，会自动做类型转换。要求变量松散等于1。
矛盾点：既要满足 is_numeric() 为false（不是数字字符串），又要弱比较 $num ==1。
字符串1a不可以，因为is_numeric("1a")判定false，但弱比较"1a"==1成立，不过还有更稳定的数组payload。
PHP中传入数组时：is_numeric(数组) 返回 false；数组和数字1做==比较结果为true，满足全部条件。
Payload
/?num[]=1
完整请求行：
GET /?num[]=1 HTTP/1.1
Payload原理

URL传num[]=1，PHP接收后$num会被解析成数组。

1. is_numeric(数组) → false，!is_numeric条件成立，进入代码块。

2. 数组 ==1 在PHP5弱比较结果为true，触发输出flag。

操作步骤（Burp Repeater）

1. 访问靶场原始页面，抓包，将GET请求发送到Repeater模块。

2. 修改请求URL，添加payload参数：/?num[]=1。


3. 点击Send发送数据包，在右侧Response响应包内获取flag。

总结&踩坑记录

1. GET参数必须用?分割路径和参数，缺少?服务器会把参数当成文件路径，读取不到GET变量，新手高频坑。

2. PHP弱类型==和is_numeric组合是Web基础CTF考点。

3. 数组payload是这类矛盾题的兜底解法，避开字符串的各类过滤。
