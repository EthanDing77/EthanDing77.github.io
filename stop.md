题目名称：你必须让他停下
来源：Bugku-CTF
标签：Web、JS断点调试、前端
难度：入门

一、题目描述

页面图片持续轮换、自动刷新，提示：Stop at panda ! u will get flag。肉眼无法直接看到flag。

二、解题思路

页面使用window.location.reload()实现JS自动刷新，每次刷新页面内容不同。只有加载10.jpg图片的页面，源码内带有被display:none隐藏的flag。通过添加JS行断点拦截刷新，反复捕获页面，找到目标图片后提取flag。

三、详细解题步骤

1. F12打开开发者工具，切换到Sources源代码面板。

2. 找到window.location.reload();刷新代码，点击行号添加行断点。

3. 刷新页面，代码运行到断点处自动暂停，阻止页面刷新。

4. 持续放行代码，直到页面出现< img src="10.jpg">。

5. 找到隐藏a标签，删除display:none，复制flag提交。

四、Flag

flag{29f018a4ff479aeaefdaf498bd991e55}

五、总结与收获
考点：JS断点调试、CSS隐藏元素。
window.location.reload()用来刷新网页；display:none的元素存在页面DOM中，只是浏览器不显示。页面内容动态变化，需要断点多次拦截捕获目标页面。

