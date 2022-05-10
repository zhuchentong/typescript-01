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

<!--

-->
