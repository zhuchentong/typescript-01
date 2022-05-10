---
layout: "section"
---

# TypeScript类型运算


---

# extends 匹配运算符

<div class="flex">

```ts {monaco}
type Equal<X, Y> = X extends Y ? true : false;

type EqualResult = Equal<1,1>
```

<v-click>

```ts {monaco}
type TypeName<T> =
    T extends string    ? "string" :
    T extends number    ? "number" :
    T extends boolean   ? "boolean" :
    T extends undefined ? "undefined" :
    T extends Function  ? "function" :
    "object";

type Result1 = TypeName<"1">
type Result2 = TypeName<2>
type Result3 = TypeName<true>
type Result4 = TypeName<undefined>
type Result5 = TypeName<(a:string)=>void>
```

</v-click>

</div>



---

# infer 推导运算符

<div class="flex">

<div class="flex-1">

```ts {monaco}
type ParamType<T> = T extends (...args: infer P) => any ? P : T;
```

</div>

<div class="flex-1 space-y-8">

<v-click>

```ts {monaco}
type ElementOf<T> = T extends Array<infer E> ? E : never;

type Value  = ElementOf<[1,1,1]>
```

</v-click>

<v-click>

```ts {monaco}
type GetLabelTypeFromObject<T> = T extends { label: infer R } ? R : never

type LabelType = GetLabelTypeFromObject<{label: string}>
```
</v-click>


<v-click>

```ts {monaco}
type GetValueType<P> = P extends Promise<infer Value> ? Value : never;

type Result = GetValueType<Promise<string>>

```
</v-click>


</div>

</div>

---
layout: center
---

# 模式匹配

> Typescript 类型的模式匹配是通过 extends 对类型参数做匹配，结果保存到通过 infer 声明的局部类型变量里，如果匹配就能从该局部变量里拿到提取出的类型

---
class: space-y-4
---

# First

> 从数组从提取数组的第一个元素

<v-click>

```ts {monaco}
type GetFirst<Arr extends unknown[]> = 
    Arr extends [infer First, ...unknown[]] ? First : never;
```

</v-click>


---
class: space-y-4
---

# Last

> 从数组从提取数组的最后一个元素

<v-click>

```ts {monaco}
type GetLast<Arr extends unknown[]> = 
    Arr extends [...unknown[], infer Last] ? Last : never;
```

</v-click>


---
class: space-y-4
---

# Rest

> 从数组从提取除最后一个元素外的数组

<v-click>

```ts {monaco}
type PopArr<Arr extends unknown[]> = 
    Arr extends [] ? [] 
        : Arr extends [...infer Rest, unknown] ? Rest : never;
```

</v-click>



---
class: space-y-4
---

# StartsWith

> 判断字符串是否开始于相应字符

<v-click>

```ts {monaco}
type StartsWith<Str extends string, Prefix extends string> = 
    Str extends `${Prefix}${string}` ? true : false;
```

</v-click>


---
class: space-y-4
---

# Replace

> 替换类型字符中的相应字符

<v-click>

```ts {monaco}
type ReplaceStr<
    Str extends string,
    From extends string,
    To extends string
> = Str extends `${infer Prefix}${From}${infer Suffix}` 
        ? `${Prefix}${To}${Suffix}` : Str;
```

</v-click>

---
class: space-y-4
---

# Trim

> 去除字符中的空格

<v-click>

```ts {monaco}
type TrimStrRight<Str extends string> = 
    Str extends `${infer Rest}${' ' | '\n' | '\t'}` 
        ? TrimStrRight<Rest> : Str;
```

</v-click>


<v-click>

```ts {monaco}
type TrimStrLeft<Str extends string> = 
    Str extends `${' ' | '\n' | '\t'}${infer Rest}` 
        ? TrimStrLeft<Rest> : Str;
```

</v-click>

<v-click>

```ts {monaco}
type TrimStrRight<Str extends string> = 
    Str extends `${infer Rest}${' ' | '\n' | '\t'}` 
        ? TrimStrRight<Rest> : Str;

type TrimStrLeft<Str extends string> = 
    Str extends `${' ' | '\n' | '\t'}${infer Rest}` 
        ? TrimStrLeft<Rest> : Str;

type TrimStr<Str extends string> =TrimStrRight<TrimStrLeft<Str>>;
```

</v-click>