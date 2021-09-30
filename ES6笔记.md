## 11.对象的新增方法

### 1.Object.fromEntries()

`Object.fromEntries()`将键值对的数据结构还原为对象

```javascript
// 例一
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);

Object.fromEntries(entries)
// { foo: "bar", baz: 42 }

// 例二
const map = new Map().set('foo', true).set('bar', false);
Object.fromEntries(map)
// { foo: true, bar: false }
```

配合`URLSearchParams`对象，将查询字符串转为对象

```javascript
Object.fromEntries(new URLSearchParams('foo=bar&baz=qux'))
// { foo: "bar", baz: "qux" }
```



### 2.Object.is()

用来比较两个值是否严格相等

## 12.运算符的扩展

### 1.指数运算符

（`**`），多个指数运算符连用时，是从最右边开始计算的。

```
//相当于 2 ** （3 ** 2）
2 ** 3 ** 2
```



### 2.链判断运算符

(`?.`)

```javascript
const firstName = message?.body?.user?.firstName || 'default';
const fooValue = myForm.querySelector('input[name=foo]')?.value
```

直接在链式调用的时候判断，左侧的对象是否为`null`或`undefined`。如果是的，就不再往下运算，而是返回`undefined`。

报错场合

```javascript
// 构造函数
new a?.()
new a?.b()

// 链判断运算符的右侧有模板字符串
a?.`{b}`
a?.b`{c}`

// 链判断运算符的左侧是 super
super?.()
super?.foo

// 链运算符用于赋值运算符左侧
a?.b = c
```



### 3.NULL判断运算符

如果某个属性的值是`null`或`undefined`，有时候需要为它们指定默认值

`??`：只有运算符左侧的值为`null`或`undefined`时，才会返回右侧的值

```javascript
const headerText = response.settings.headerText ?? 'Hello, world'
```

常见做法是通过`||`运算符指定默认值，但空字符串或`false`或`0`，也会生效。

### 4.逻辑赋值运算符

```
// 或赋值运算符
x ||= y
// 等同于
x || (x = y)

// 与赋值运算符
x &&= y
// 等同于
x && (x = y)

// Null 赋值运算符
x ??= y
// 等同于
x ?? (x = y)
```

用途之一：为变量或属性设置默认值



## 13.Symbol

1. 



## 14.Set和Map数据结构

### 1.Set

它类似于数组，但是成员的值都是唯一的，没有重复的值。

​	**属性**

​	`Set.prototype.constructor`; 构造函数，默认就是`Set`函数。

​	`Set.prototype.size`：返回`Set`实例的成员总数。

​	**方法**

​	`Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。

​	`Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。

​	`Set.prototype.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。

​	`Set.prototype.clear()`：清除所有成员，没有返回值。



### 2.WeakSet

1.WeakSet 的成员只能是对象，而不能是其他类型的值。

2.WeakSet 没有`size`属性，没有办法遍历它的成员。

​		WeakSet 不能遍历，是因为成员都是弱引用，随时可能消失，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。



### **3.Map**

`Object` 结构提供了“字符串—值”的对应，`Map` 结构提供了“值—值”的对应

```javascript
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```

注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。

```javascript
const map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```

上面代码的`set`和`get`方法，表面是针对同一个键，但实际上这是两个不同的数组实例，内存地址是不一样的，因此`get`方法无法读取该键，返回`undefined`。

由上可知，Map 的**键**实际上是跟**内存地址**绑定的，只要内存地址不一样，就视为两个键。

#### 实例的属性和操作方法

**（1）size 属性**

`size`属性返回 Map 结构的成员总数。

**（2）Map.prototype.set(key, value)**

`set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键。

**（3）Map.prototype.get(key)**

`get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。

**（4）Map.prototype.has(key)**

`has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

**（5）Map.prototype.delete(key)**

`delete`方法删除某个键，返回`true`。如果删除失败，返回`false`。

**（6）Map.prototype.clear()**

`clear`方法清除所有成员，没有返回值。

```javascript
const map = new Map()
map.set(1,1)
map.set(2,2)
map.set(3,'zs').set(4,'ls')
map.get(3) // zs
map.get(5) // undefined
map.has(2) // true
map.has(5) // false
map.delete(1) // true
map.delete(5) // false
map.clear()
```



#### **遍历方法**

Map 结构原生提供三个遍历器生成函数和一个遍历方法。

- `Map.prototype.keys()`：返回键名的遍历器。
- `Map.prototype.values()`：返回键值的遍历器。
- `Map.prototype.entries()`：返回所有成员的遍历器。
- `Map.prototype.forEach()`：遍历 Map 的所有成员。

需要特别注意的是，Map 的遍历顺序就是插入顺序。

Map 还有一个`forEach`方法，与数组的`forEach`方法类似，也可以实现遍历。

`forEach`方法还可以接受第二个参数，用来绑定`this`。

```javascript
const reporter = {
  report: function(key, value) {
    console.log("Key: %s, Value: %s", key, value);
  }
};

map.forEach(function(value, key, map) {
  this.report(key, value);
}, reporter);
```

上面代码中，`forEach`方法的回调函数的`this`，就指向`reporter`。

#### 与其他数据结构的互相转换

**（1）Map 转为数组**

```javascript
const myMap = new Map()
  .set(true, 7)
  .set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
```

**（2）数组 转为 Map**

将数组传入 Map 构造函数，就可以转为 Map。

```javascript
new Map([
  [true, 7],
  [{foo: 3}, ['abc']]
])
// Map {
//   true => 7,
//   Object {foo: 3} => ['abc']
// }
```

**（3）Map 转为对象**

如果所有 Map 的键都是字符串，它可以无损地转为对象。

如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。

```javascript
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

const myMap = new Map()
  .set('yes', true)
  .set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```

**（4）对象转为 Map**

对象转为 Map 可以通过`Object.entries()`。

```javascript
let obj = {"a":1, "b":2};
let map = new Map(Object.entries(obj));
```

**（5）Map 转为 JSON**

**（6）JSON 转为 Map**

### 4.WeakMap

`WeakMap`与`Map`的区别有两点。

首先，`WeakMap`只接受对象作为键名（`null`除外），不接受其他类型的值作为键名。

其次，`WeakMap`的键名所指向的对象，不计入垃圾回收机制。

只要所引用的对象的其他引用都被清除，垃圾回收机制就会释放该对象所占用的内存。也就是说，一旦不再需要，WeakMap 里面的键名对象和所对应的键值对会自动消失，不用手动删除引用。

注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用。

## 15.Proxy

Proxy 用于修改某些操作的默认行为，可以对外界的访问进行过滤和改写，表示由它来“代理”某些操作

```javascript
var proxy = new Proxy(target, handler);
```

**Proxy 支持的拦截操作**

- **get(target, propKey, receiver)**：拦截对象属性的读取，比如`proxy.foo`和`proxy['foo']`。
- **set(target, propKey, value, receiver)**：拦截对象属性的设置，比如`proxy.foo = v`或`proxy['foo'] = v`，返回一个布尔值。
- **has(target, propKey)**：拦截`propKey in proxy`的操作，返回一个布尔值。
- **deleteProperty(target, propKey)**：拦截`delete proxy[propKey]`的操作，返回一个布尔值。
- **ownKeys(target)**：拦截`Object.getOwnPropertyNames(proxy)`、`Object.getOwnPropertySymbols(proxy)`、`Object.keys(proxy)`、`for...in`循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而`Object.keys()`的返回结果仅包括目标对象自身的可遍历属性。
- **getOwnPropertyDescriptor(target, propKey)**：拦截`Object.getOwnPropertyDescriptor(proxy, propKey)`，返回属性的描述对象。
- **defineProperty(target, propKey, propDesc)**：拦截`Object.defineProperty(proxy, propKey, propDesc）`、`Object.defineProperties(proxy, propDescs)`，返回一个布尔值。
- **preventExtensions(target)**：拦截`Object.preventExtensions(proxy)`，返回一个布尔值。
- **getPrototypeOf(target)**：拦截`Object.getPrototypeOf(proxy)`，返回一个对象。
- **isExtensible(target)**：拦截`Object.isExtensible(proxy)`，返回一个布尔值。
- **setPrototypeOf(target, proto)**：拦截`Object.setPrototypeOf(proxy, proto)`，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
- **apply(target, object, args)**：拦截 Proxy 实例作为函数调用的操作，比如`proxy(...args)`、`proxy.call(object, ...args)`、`proxy.apply(...)`。
- **construct(target, args)**：拦截 Proxy 实例作为构造函数调用的操作，比如`new proxy(...args)`。



## 16.Reflect

**目的**

（1） 将`Object`对象的一些明显属于语言内部的方法（比如`Object.defineProperty`），放到`Reflect`对象上。

（2） 修改某些`Object`方法的返回结果，让其变得更合理。

```javascript
// 老写法
try {
  Object.defineProperty(target, property, attributes);
  // success
} catch (e) {
  // failure
}

// 新写法
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```



（3） 让`Object`操作都变成函数行为。某些`Object`操作是命令式，比如`name in obj`和`delete obj[name]`，而`Reflect.has(obj, name)`和`Reflect.deleteProperty(obj, name)`让它们变成了函数行为。

```javascript
// 老写法
'assign' in Object // true

// 新写法
Reflect.has(Object, 'assign') // true
```

（4）`Reflect`对象的方法与`Proxy`对象的方法一一对应，只要是`Proxy`对象的方法，就能在`Reflect`对象上找到对应的方法。

```javascript
Proxy(target, {
  set: function(target, name, value, receiver) {
    var success = Reflect.set(target, name, value, receiver);
    if (success) {
      console.log('property ' + name + ' on ' + target + ' set to ' + value);
    }
    return success;
  }
});
```





## other:个人笔记

#### 1.null 和undefined的区别

​	**null表示“没有对象”，即该处不应该有值**。典型用法：

```
（1） 作为函数的参数，表示该函数的参数不是对象。

（2） 作为对象原型链的终点。
```

​	**undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。**典型用法是：

```
（1）变量被声明了，但没有赋值时，就等于undefined。

（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。

（3）对象没有赋值的属性，该属性的值为undefined。

（4）函数没有返回值时，默认返回undefined。
```



#### 2.eventbus

可用于兄弟组件传值

`$on`:监听当前实例上的自定义事件。必须要在`$emit`触发之前注册，否则无法监听到。

`$emit`:触发当前实例上的事件。