﻿# trace.js

JavaScript代码调试、测试、错误监测上报工具，提供各浏览器下统一的日志窗口，兼容包括IE6在内的绝大部分浏览器。超轻量级工具。

![trace](http://mokjs.sinaapp.com/pic/trace.png)

## 使用方法

开发时在页面里引入trace.js：

    <script type="text/javascript" src="trace.js"></script>

在浏览器里打开页面，按组合键 `Alt + ~` 即可打开日志窗口。

日志窗口的操控方法及快捷键使用请查看日志窗口右上角的 `Help` 菜单。

为提高线上的性能或者减小JS文件大小，上线时可换成trace-online.js：

    <script type="text/javascript" src="trace-online.js"></script>

当然也可以不换。trace-online.js里的代码请自行按照业务需求修改。

## 接口API

    trace()

输出普通日志，以白色字体显示。

    trace.ok()

输出成功日志，以绿色字体显示。

    trace.warn()

输出警告日志，以黄色字体显示。

    trace.error()

输出错误日志，以红色字体显示。

以上4个接口都可同时传多个参数。输出日志时各数据间以 `◆` 符号分隔。

    trace.time(mark)

开始计算某一段代码的用时，mark为计时标记。

    trace.timeEnd(mark)

结束计算某一段代码的用时，mark为计时标记。


## 用于测试的接口API

    trace.eq(actualValue, expectedValue, msg)

判断实际结果actualValue与期望值expectedValue是否一致，trace内部用全等 `===` 比较。msg为不相等时的报错信息。

    trace.assert(trueValue, msg)

判断结果是否为true，trace内部用 `=== true` 比较。msg为参数trueValue不等true时的报错信息。

    trace.report()

打印测试报告。

## 代码示例

```javascript
	trace.time('test-example');
	trace('div>加粗<b>haha</b>没"有用<span');
	trace.ok('div>加粗<b>haha</b>没有用<span', {}, 2011);
	trace.error('计算结果：', 2012+12-10, 0, null, 2010);
	trace.warn(123, '', new Date);
	trace.warn(null);

	var obj = {
		abc: 'abs>k"<dld>sd<c',
		num: 456,
		arr: [456,567],
		nul: null,
		dt: new Date(),
		reg: /^reg$/ig,
		cde: {
			hjk: 236,
			arr: [456,567,789],
			nul: null,
			dt: new Date(),
			reg: /^reg22$/ig,
			mnj: {
				iuy: 789,
				kjdj: 'some str',
				objjj: {
					kqwe: 'haha~',
					end: 100
				}
			}
		}
	};
	trace(obj);
	//setTimeout(function(){trace.ok({'sajgj':858,'iojk':'value hehe.'});},10000);

	trace([0, 1.1, 2, 3]);
	trace('array===' + [0, 1.1, 2, 3]);
	trace( 0==false );
	trace(new Date());
	trace(Date);
	trace(/^85/g.toString());
	trace(new RegExp('sj\\/d', 'gi'));
	trace(/^8s<kdk5/g);
	trace(/^8s<kdk5/g, 'somenote');
	var c34 = '双引号"end &#34;', c39 = "单引号'end &#39;";
	trace(c34, c39);
	trace(c39);
	trace('div>加粗<b>haha</b>没有用<span');

	//调用测试接口
	trace.eq(1, '1');
	trace.eq(1, 2);
	trace.eq('abc', 'abc');
	trace.assert(456, 'error!');
	trace.report();

	var a = 456;
	trace.eq(1, 1);
	trace.assert(!!a, 'error!');
	trace.report();

	trace.sendLog();
	trace.timeEnd('test-example');
```