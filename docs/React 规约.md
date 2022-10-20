---
sidebar_position: 3
---

# React 规约

## 数据不可变

不可以直接修改状态。

正例：

```tsx
const [count, setCount] = useState(0);
const handle = () => {
  setCount((d) => d + 1);
};
```

反例：

```tsx
const handle = () => {
  count++;
};
```

## 状态的修改

数据不可变在 React 中非常重要，在一般状况下更新状态都不能直接修改状态值。更新状态必须要使用 `setState` 方法。

```tsx
const handleSet = () => {
  // 获取的状态是用 setData 提供的回调，也没有修改原有的状态
  setData((draft) => ({
    ...draft,
    someDate: {
      name: 'test2',
    },
  }));
};
```

但 React 的状态是浅对比的，如果状态是复杂的引用值，浅克隆的修改也可以生效。

```tsx
const [data, setData] = useState({
  id: 1,
  someData: {
    name: 'test',
  },
});

const handleSet = () => {
  // 1. 浅克隆 temp.someData 依然是 data.someData 的引用
  // 2. 获取的状态可能不是最新的
  // 3. useCallback 需要添加依赖
  let temp = { ...data };
  temp.someData = {
    name: 'test2',
  };
  setData(temp);
};
```

但是并不推荐这样做，获取最新的状态的方法最好是利用 `setState()` 提供的回调。或者使用第三方库，例如 `use-immer`

```tsx
const [data, setData] = useImmer({
  id: 1,
  someData: {
    name: 'test',
  },
});

const handleSet = () => {
  // use-immer 提供了一个可直接修改的 draft
  setData((draft) => {
    draft.someData = {
      name: 'test2',
    };
  });
};
```
