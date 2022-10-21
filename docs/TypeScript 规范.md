---
sidebar_position: 4
---

# TypeScript 规范

## 命名

TypeScript 类型别名/接口以及类均使用大写开头。

正例：

```tsx
export interface BasePage {
  total: number;
  per_page: number;
  current_page: number;
  last_page: number;
}

type CheckPeopleProps = {
  phone: string | number;
  password: string | number;
};

export class Light implements SLightBase {
  visible = true;
  color = '#fff';
  intensity = 1;
}
```

反例：

```tsx
export interface basePage {
  total: number;
  per_page: number;
  current_page: number;
  last_page: number;
}
```

## 类型签名

所有类型都应有签名/声明 ，除特殊情况均不使用 `any` 。

正例：

```tsx
const createStore = <S extends Record<string, unknown>>(initialState: S) => {
  const _state = initialState;

  // ...

  return {
    state: _state,
  };
};
```

反例：

```tsx
export interface Columns {
  title: string; //名称
  dataIndex: string;
  sorter?: (a: any, b: any) => any; //排序
  render?: (tags: any, rowData?: any) => any;
  defaultSortOrder?: string;
} //列表表头数据
```

### 不确定的类型

总会出现静态无法检查的类型，可以使用 `unknow` 配合运行时检查。除特殊情况均不使用 `any` 。

```tsx
const setAge = (age: number) => {};
const setName = (name: string) => {};

const doSomething = (data: unknown) => {
  if (typeof data === 'number') {
    setAge(data);
  }
  if (typeof data === 'string') {
    setName(data);
  }
};
```

### 为什么不使用 `any`

```tsx
let vAny: any = 10; // We can assign anything to any
let vUnknown: unknown = 10; // We can assign anything to unknown just like any

let s1: string = vAny; // Any is assignable to anything
let s2: string = vUnknown; // Invalid; we can't assign vUnknown to any other type (without an explicit assertion)

vAny.method(); // Ok; anything goes with any
vUnknown.method(); // Not ok; we don't know anything about this variable
```

[https://stackoverflow.com/questions/51439843/unknown-vs-any](https://stackoverflow.com/questions/51439843/unknown-vs-any)
