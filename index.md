# index.js源码解读

index.js是antd库的入口文件。但实际上webpack调用的是index-with-locales.js。

主要功能是动态加载components下面的组件index.tsx和样式style/index.tsx。

## camelCase函数

将名称转换成大驼峰命名。

charAt: 根据索引取出字符串中某个字符。

toUpperCase: 转换成大写。

slice: 截取字符串。

replace: 替换字符串，第一个可以是要替换的字符串或者匹配的正则，第二个是要替换成的字符串或者生成字符串的函数。

## require.context

webpack提供的动态引入文件的函数。第一个参数为相对路径，第二个为指定是否包括子目录，第三个指定加载文件的正则。

返回一个函数req，可以通过req.keys()获取加载文件的数组。可以通过req(key)获取特定的文件的对象。
