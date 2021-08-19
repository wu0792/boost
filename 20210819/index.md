### 泛型中的类型名称后，等号后面的是默认类型

``` javascript
const say = <Data = number>(p: Data) => {}

say(1)
say<string>('')
```

### ~表示数字的按位取反，~~加在数字后面相当于两次按位取反，正数就Math.floor() / 负数就Math.ceil() 的作用，等价于 `| 0`, 性能有5%左右的提升，但可读性不好，不推荐使用，发现 swr 中有使用

``` javascript
~~1.2 === 1.2 | 0 === 1
~~(-1.3) === (-1.3 | 0) === -1
export const createKey = () => 'swr-key-' + ~~(Math.random() * 1e7)
```


### WeakMap 用来存储弱引用的键值对，所谓弱引用就是在未被外部使用的前提下，随时可能将作为垃圾回收，而Key被要求是非原始类型（Not Primitive)，WeakMap的一大特点是无法遍历所有key，因为所有key随时可能被回收


### 原始值(Primitive)是指不是object对象，包括7种原始类型：string, number, bigint, boolean, undefined, null, symbol，所有原始值都不可变(immutable)，也就是不能被修改，除了null和undefined，其余所有原始值都有与之对应的包装器类型，通过访问包装器的 valueOf() 可以返回其原始值
``` js
String <=> string
Number <=> number
BigInt <=> bigint
Boolean <=> boolean
Symbol <=> symbol
```

### 判断是否服务端的时候，现在需要增加一个 Deno 的判断
``` js
export const IS_SERVER = typeof window === 'undefined' || 'Deno' in window
```

### 用来定义一个参数为指定参数类型的方法
``` js
const navigatorConnection =
  typeof navigator !== 'undefined' &&
  (navigator as Navigator & {
    connection?: {
      effectiveType: string
      saveData: boolean
    }
  }).connection
```

### 判断浏览器的弱网状态
``` js
export const slowConnection =
  !IS_SERVER &&
  navigatorConnection &&
  (['slow-2g', '2g'].includes(navigatorConnection.effectiveType) ||
    navigatorConnection.saveData)
```









