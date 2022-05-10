---
layout: "section"
---

# TypeScript类型系统

---

<div class="flex justify-center">

<div class="flex-1 text-center">

# 基础类型

- **Boolean**
- **Number**
- **String**
- **Array**
- **Null**
- **Undefined**

</div>

<div class="flex-1 text-center">

# 扩展类型

- **Enum（枚举）**
- **Any （任意）**
- **Unknown（未知）**
- **Tuple（元组）**
- **void（与 Any 相反）**
- **Never（用于不存在）**

</div>

</div>

<div class="py-4">

<v-click>

```ts {monaco}
type TTuple = [string, number];
type Res = TTuple[number]; // string | number
```

</v-click>

</div>

<style>
ul{
        list-style:none;
}
</style>
<!-- 
数组类型是指任意多个同一类型的元素构成的，比如 number[]、Array<number>，而元组则是数量固定，类型可以不同的元素构成的，比如 [1, true, 'guang']。
-->

---
layout: image-left
image: https://pic2.zhimg.com/v2-2c82c1cbb0b5af2f8bab6cd772541a8a_1440w.jpg?source=172ae18b
---


# 泛型

> 泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。


<v-click>

```ts{1-2|all}
type AddStr = (x:string, y:string)=>string
type AddNumber = (x:number, y:number)=>number

type Add<T> = (x:T,y:T)=>T
```

</v-click>


---

# TypeScript内置类型

- **Partial**
- **Required**
- **Readonly**
- **Pick**
- **Record**
- **Exclude**
- **Extract**
- **Omit**
- **NonNullable**
- **Parameters**
- **ConstructorParameters**
- **ReturnType**
- **InstanceType**
- **Uppercase**
- **Lowercase**
- **Capitalize**
- **Uncapitalize**

<style>
ul{
padding:10px 0;
    display:flex;
    flex-wrap:wrap;
    gap:10px;
}

li{
        background-color:#228ada;
        border-radius:10px;
        padding:5px 10px;
        width:30%;
        list-style:none;
        font-size:20px;
        text-align:center;
}
</style>

---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

# **Partial**

```ts
type Partial<T> = {
    [P in keyof T]?: T[P];
}
```

</div>

</template>



<template v-slot:right>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
interface Person {
        name: string
        age: number
        sex: number
}

const user:Partial<Person> = { name: "zhangsan" }
```

</v-click>

</div>

</template>



---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
interface Person {
        name: string
        age?: number
}

const user: Require<Person> = { name: "zhangsan" }
```

</v-click>

</div>

</template>


<template v-slot:right>

<div class="h-full flex flex-col justify-center">

# **Required**

```ts
type Required<T> = {
    [P in keyof T]-?: T[P];
};
```

</div>

</template>


---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

# **Readonly**

```ts
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
}
```

</div>

</template>



<template v-slot:right>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
interface Person {
        name: string
        age?: number
}

const user:Readonly<Person> = { name: "zhangsan" }

user.name = "zhaosi"
```

</v-click>

</div>

</template>


---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
interface Person {
        name: string
        age: number
}

const user1:Person = {
        name:"zhangsan",
        age:20
}

const user2: Pick<Person,"name"> = {
        name: "li4"
}

const user3: Pick<Person,"name"> = {
        name: "wang5",
        age: 77
}
```

</v-click>

</div>

</template>


<template v-slot:right>

<div class="h-full flex flex-col justify-center">

# **Pick**

```ts
type Pick<T, K extends keyof T> = {
    [P in K]: T[P];
};
```

</div>

</template>



---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

# **Record**

```ts
type Record<K extends keyof any, T> = {
    [P in K]: T;
};
```

</div>

</template>



<template v-slot:right>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
const user :Record<string,string> = {
        user: "no name",
        signature: "no body in here"
}
```

</v-click>

</div>

</template>


---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
type UserProps = "name" | "age"

type StudentProps = "name" | "age" | "class" | "school"

const user1: Exclude<StudentProps,UserProps> = "name"
```

</v-click>

</div>

</template>


<template v-slot:right>

<div class="h-full flex flex-col justify-center">

# **Exclude**

```ts
type Exclude<T, U> = T extends U ? never : T;
```

</div>

</template>


---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

# **Extract**

```ts
type Extract<T, U> = T extends U ? T : never;
```

</div>

</template>



<template v-slot:right>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
type UserProps = "name" | "age"

type StudentProps = "name" | "age" | "class" | "school"

const user1: Extract<StudentProps,UserProps> = "name"
```

</v-click>

</div>

</template>


---
layout: two-cols
---

<template v-slot:default>

<div class="h-full flex flex-col justify-center">

<v-click>

```ts {monaco}
type UserProps = {
        name: string
        age: number
        class: string
        school: string
}

type StudentProps = "name" | "age" 

type OmitResult = Omit<UserProps,StudentProps> 

const user1: OmitResult = {}
```

</v-click>

</div>

</template>


<template v-slot:right>

<div class="h-full flex flex-col justify-center">

# **Omit**

```ts
type Omit<T, K extends keyof any> =
Pick<T, Exclude<keyof T, K>>;
```

</div>

</template>

