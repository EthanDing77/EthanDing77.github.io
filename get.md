一、题目描述

查看页面源代码可见PHP代码，代码要求GET参数what等于flag时，页面输出flag。

二、解题思路

PHP通过$_GET读取URL中的GET参数。构造URL，拼接?what=flag，访问页面触发判断逻辑，拿到flag。

三、详细解题步骤

1. F12查看页面源代码，分析PHP逻辑：读取GET参数what，当what=="flag"就输出flag。

2. 在原网址末尾拼接参数：?what=flag。

3. 访问拼接后的URL，页面直接输出flag。
