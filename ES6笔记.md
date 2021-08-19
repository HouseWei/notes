## 11.对象的新增方法

1. **Object.fromEntries()**

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

   

2. **Object.is()**

   用来比较两个值是否严格相等

## 12.运算符的扩展

1. **指数运算符**

   （`**`），多个指数运算符连用时，是从最右边开始计算的。

   ```
   //相当于 2 ** （3 ** 2）
   2 ** 3 ** 2
   ```

   

2. 链判断运算符

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

   

3. 

   

   

   

   

   

   