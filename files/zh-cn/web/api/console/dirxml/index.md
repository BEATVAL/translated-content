---
title: Console.dirxml()
slug: Web/API/Console/dirxml
translation_of: Web/API/Console/dirxml
---
{{APIRef("Console API")}}{{Non-standard_header}}

显示一个明确的 XML/HTML 元素的包括所有后代元素的交互树。如果无法作为一个 element 被显示，那么会以 JavaScript 对象的形式作为替代。它的输出是一个继承的扩展的节点列表，可以让你看到子节点的内容。

## 语法

```plain
console.dirxml(object);
```

## 参数

- `object`
  - : 一个属性将被输出的 JavaScript 对象。

## 浏览器兼容性

{{Compat("api.console.dirxml")}}

## 相关链接

- [Opera Dragonfly documentation: Console](http://www.opera.com/dragonfly/documentation/console/)
