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
