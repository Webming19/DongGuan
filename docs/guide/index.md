# Markdown 与 MDX

Rspress 不仅支持 Markdown，还支持强大的内容开发方式——[MDX](https://mdxjs.com/)。

## Markdown

MDX 是 Markdown 的超集，这意味着您可以像往常一样编写 Markdown 文件。例如：

```md
# Hello World
```

## 使用组件

当您想在 Markdown 文件中使用 React 组件时，您应该将文件的扩展名命名为`.mdx`。例如：

```mdx
// docs/index.mdx
import { CustomComponent } from './custom';

# Hello World

<CustomComponent />
```

## 前置内容 (Front Matter)

您可以在 Markdown 文件的开头添加前置内容，它是一个用 YAML 格式定义的一些元数据的对象。例如：
```yaml
---
title: Hello World
---
```

> 注意：默认情况下，Rspress 使用 h1 标题作为 html 标题。

您还可以访问正文中定义的前置内容属性，例如：

```markdown
---
title: Hello World
---

# {frontmatter.title}
```

之前定义的属性将作为`frontmatter`属性传递给组件。因此最终的输出将是：

```html
<h1>Hello World</h1>
```

## 自定义容器

您可以使用 `:::` 语法创建自定义容器并支持自定义标题。例如：

**输入:**

```markdown
:::tip
This is a `block` of type `tip`
:::

:::info
This is a `block` of type `info`
:::

:::warning
This is a `block` of type `warning`
:::

:::danger
This is a `block` of type `danger`
:::

::: details
This is a `block` of type `details`
:::

:::tip Custom Title
This is a `block` of `Custom Title`
:::

:::tip{title="Custom Title"}
This is a `block` of `Custom Title`
:::
```

**输出:**

:::tip
This is a `block` of type `tip`
:::

:::info
This is a `block` of type `info`
:::

:::warning
This is a `block` of type `warning`
:::

:::danger
This is a `block` of type `danger`
:::

::: details
This is a `block` of type `details`
:::

:::tip Custom Title
This is a `block` of `Custom Title`
:::

:::tip{title="Custom Title"}
This is a `block` of `Custom Title`
:::

## 代码块

### 基础用法

您可以使用 \`\`\` 语法创建代码块并支持自定义标题。例如：

**输入:**

````md
```js
console.log('Hello World');
```

```js title="hello.js"
console.log('Hello World');
```
````

**输出:**

```js
console.log('Hello World');
```

```js title="hello.js"
console.log('Hello World');
```


### 显示行号

如果要显示行号，可以在配置文件中启用`showLineNumbers`选项：

```ts title="rspress.config.ts"
export default {
  // ...
  markdown: {
    showLineNumbers: true,
  },
};
```

### 行高亮

您还可以同时应用行高亮和代码块标题，例如：

**输入:**

````md
```js title="hello.js" {1,3-5}
console.log('Hello World');

const a = 1;

console.log(a);

const b = 2;

console.log(b);
```
````

**输出:**

```js title="hello.js" {1,3-5}
console.log('Hello World');

const a = 1;

console.log(a);

const b = 2;

console.log(b);
```

## Rustify MDX 编译器

您可以通过以下配置启用 Rustify MDX 编译器：
