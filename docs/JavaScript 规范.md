---
sidebar_position: 5
---

# JavaScript 规范

## 变量

不涉及到修改的变量以及常量均使用 `const` 声明，只有在需要修改到变量本身时才使用 `let` 声明。没有特殊情况均不使用 `var` 。

```tsx
const someData = await fetch();

// 需要修改变量时再使用 let
let count = 0;
const handleCount = () => (count += 1);
```

## 常量

常量命名全部大写，力求语义表达完整清楚。

```tsx
const MAX_EMBED_COUNT = 10;
```

## 命名

变量名采用小写驼峰命名。除开头外以单词分割首字母大写

正例：

```tsx
const mediaContent = [];
const [imgSize, setImgSize] = useState();
```

反例：

```tsx
const mediacontent = [];
const [img_size, set_img_size] = useState();
```

## 缩进

缩进使用两个空格。嵌套的节点应该缩进。

```tsx
<Suspense fallback>
  <CardTopBar
    style={{
      color: '#0E6FF6',
    }}
    onClose={() => dispatch(setShowBook(false))}
  />
</Suspense>
```

## 分号

除个别语句外，语句结尾应添加分号。

```tsx
// 标记点的位置，对应图片原始大小的位置
const [point, setPoint] = useState({
  left: 674.5,
  top: 349.5,
});
// 标记点的渲染位置
const [pointPos, setPointPos] = useState({
  left: 0,
  top: 0,
});
```

## 引号

JavaScript 代码中使用单引号 `'` ，JSX 与 HTML 属性使用双引号 `"` 。

```tsx
const name = 'xfy';
const btn = document.querySelector('.btn');

<button className="btn">
  Click Me
</button>

<button class="btn">
  Click Me
</button>
```

## 括号

多个 `if` 之间括号不能省略。

正例：

```tsx
if (condition) {
  doSomething();
} else if (either) {
  doAother();
} else {
  return something;
}
```

反例：

```tsx
if (condition) doSomething();
else if (either) doAother();
else return something;
```

## 判断

在封装方法时，未达到执行条件，且方法可以返回时，优先 `return` 。

正例：

```tsx
function doSomething(condition) {
  if (!condition) return;
  doSomething();
}
```

反例：

```tsx
function doSomething(condition) {
  if (condition) {
    doSomething();
  }
}
```

### 条件过多时

条件过多时，可以使用 `switch` 语句或使用对象代替。在 `switch` 语句中声明变量默认是在同一个作用域中，需要在 `case` 语句中添加大括号。

正例：

```tsx
const number = 2;
switch (number) {
  case 1: {
    const message = 'first number';
    console.log(message);
    break;
  }
  case 2: {
    const message = 'second number';
    console.log(message);
    break;
  }
  case 3: {
    const message = 'third number';
    console.log(message);
    break;
  }
  default: {
    const message = 'second number';
    console.log(message);
    break;
  }
}
```

```tsx
const number = 2;
const numberMap = {
  1: () => {
    const message = 'first number';
    console.log(message);
  },
  2: () => {
    const message = 'second number';
    console.log(message);
  },
  3: () => {
    const message = 'third number';
    console.log(message);
  },
};

// default
if (typeof numberMap[number] !== 'function') {
  const message = 'second number';
  console.log(message);
}

numberMap[number]();
```

反例：

```tsx
const number = 2;
switch (number) {
  case 1:
    const message = 'first number';
    console.log(message);
    break;
  case 2:
    const message = 'second number';
    console.log(message);
    break;
  case 3:
    const message = 'third number';
    console.log(message);
    break;
  default:
    const message = 'second number';
    console.log(message);
    break;
}
// Cannot redeclare block-scoped variable 'message'.ts(2451)
```

### 判断值可能是数字时

由于数字 `0` 隐式转换结果为 `false` ，当判断的条件可能是数字时，一定要留意不能使用缩写。

正例：

```tsx
// 如果 number 存在则执行
if (number != null) {
  doSomething();
}
```

反例：

```tsx
// 如果 number 存在则执行，如果 number 为 0，则该条件也不会生效。
if (number) {
  doSomething();
}
```

## 相等判断

除 `null` 和 `undefined` ，其他值判断是否相等都应该使用 `===` 而非 `==` 。

正例：

```tsx
if (condition === 42) {
  doSomething();
}
if (condition != null) {
  doSomething();
}
```

反例：
