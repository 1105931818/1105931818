# TypeScript



## 基本类型

```js
const str: string = 'zx'   //字符串类型

const num: number = 123.5 //数字类型
const infin: number = Infinity //无穷大
const hex: number = 0xfood //十六进制

const b1: boolean = true //布尔值

const n: null = null
const u: undefined = undefined 

function a(): void {
  
} //返回值为空
```

#### 类型声明

​	类型声明是TS非常重要的一个特点

​	通过类型声明可以指定TS中变量（参数，形参）的类型

​	指定类型后，当为变量赋值时，TS编译器会自动检查值是否符合类型声明，符合则赋值，否则报错

​	类型声明给变量设置了类型，使得变量只能存储某种类型的值



#### 自动类型判断

​	TS拥有自动的类型判断机制

​	当对变量的声明和赋值是同时进行的，TS编译器会自动判断变量的类型，所以可以省略掉类型声明

​	声明变量如果不指定类型，则TS解析器会自动判断变量的类型为any（隐式any）



#### 类型

##### 1.顶级类型 top type：any  unknown

​	unknown只能赋值给自身，或是any。unknown为对象时，没有办法读任何属性，方法也不可以调用

##### 2.Object

​	Object可以为任意类型（原型链），object只能为引用数据类型（复杂数据类型）。{ }可以为任意类型，等价于new  Object。

```js
const a1: Object = 1223
const a2: Object = '1234'

const b1: object = []
const b2: object = {}
const b3: object = () => {}

const c1: {} = 1223
const c2: {} = '1234'  //赋值后，无法修改
```

##### 3.Number  String  Boolean

##### 4.number  string  boolean

##### 5.字面量

##### 6.never

![image-20230517150322552](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230517150322552.png)

npm i @types/node -D



#### 接口（interface)

```js
interface A extends B {  //接口继承
  name: string,
  [propName: string]: any  //索引签名，任意key，使用接口这个为任意属性，可添加多个属性也可不加
}   //定义接口

interface A{
  age?: number   //属性？表示该属性可写可不写
  readonly fn: () => boolean   //readonly 只读属性,不能修改
}   //接口重名，会重合

const a: A{
  name: 'zs',
  age: 18,
  sex: '男',
  a: 1,
  b: 2,
  fn: () => {
    return false
  }
}   //使用接口，属性要和接口一样

interface B {
  sex: string
}


//定义函数类型
interface Fn {
  (name: string): number[]
}

const fn1: Fn = function(name: string) {
  return [1, 3, 4]
}
```



#### 数组

```ts
const arr: number[] = [1,2,4,5]  //定义一个数字类型数组
const arr1: Array<boolean> = [true, false]  //定义布尔值的数组


interface X {
  name: string
  age?: number
}
const arr2: X[] = [{name: 'zs'}, {name: 'ls'}]  //定义复杂类型的数组

const arr3: number[][] = [[1], [2], [3]]  //定义二维数组
const arr4: Array<Array<number>> = [[1], [2], [3]]
const arr5: any[] = [1, 'zs', {}]
const arr6: [number, string, {}] = [1, 'zs', {}]

function fn(...args: string[]) {
  console.log(args)
  const arr: IArguments = arguments  //定义伪数组
}

interface A{  //IArguments原理
  callee: Function
  length: number
  [index: number]: any
}
```



#### 函数

```ts
//默认值和可选参数
function add(a: number = 10, b?: number): number{
  return a + b
}

const add = (a: number, b: number): number =>  a + b

interface User {
  name: string
  age: number
}
//参数定义为一个对象
function fn(user: User): User{
  return user
}

//ts可以定义this的类型，必须是第一个参数定义this的类型
interface Obj {
  user: number[]
  add: (this: Obj, num: number) => {}
}
const obj: Obj = {
  user: [1,2,3]
  add(this: Obj, num: number){
    this.user.push(num)
  }
}
obj.add(4)

//函数重载
const arr: number[] = [1,2,3,4]
function find(): number[]
function find(id: number): number[]
function find(add: number[]): number[]
function find(ids?: number | number[]): number[] {
  if(typeof ids === 'number'){
    return user.filter(v => v === ids)
  }else if(Array.isArray(ids)){
    user.push(...ids)
    return user
  }else{
    return user
  }
}
```



#### 类型断言，联合类型，交叉类型

```ts
const phone: number | string = 123415

function fn(type: number | boolean): boolean {
  return !!type
}

//联合类型
interface A {
  name: string
}
interface B {
  age: number
}
const man: A & B = {name: 'zs', age: 18}

//类型断言
const a: A | B
console.log((<A>a).name)
console.log((a as A).name)
```



#### 内置对象定义类型

```ts
const date: Date = new Date()
const reg: RegExp = new RegExp(/\.xx/)
const error: Error = new Error('错误')
const xhr: XMLHttpRequest = new XMLHttpRequest()

//DOM对象类型：HTML(元素名称)Element | HTMLElement
const el: HTMLDivElement = document.querySelector('div')

const lis: NodeList = document.querySelectorAll('li')
const divs: NodeListOf<HTMLElement> = document.querySelectorAll('div')

const local: Storage = localStorage
const lo: Location = location
const pro: Promise<number> = new Promise((r) => r(1))
const cookie: string = document.cookie
```



#### Class

```ts
interface Options {
  el: string | HTMLElement
}
interface VueCls {
  options: Options
  init(): void
}
interface Vnode {
  tag: string
  text?: string
  children?: Vnode[]
}

class Dom {
  //private修饰的函数只能在内部使用,私有属性
  private createElement(el: string) {
    return document.createElement(el)
  }
  
  private setText(el: HTMLElement, text: string | null){
    el.textContent = text
  }
  
  //protected，只能给继承类和内部使用
  protected render(data: Vnode){
    const app = this.createElement(data.tag)
    
    if(data.children && Array.isArray(data.children)){
      data.children.forEach(item => {
        const child = this.render(item)
        app.appendChild(child)
      })
    }else{
      this.setText(app, data.text)
    }
    
    return app
  }
}

//继承和类型约束
class Vue extends Dom implements VueCls {
  readonly options: Options
  constructor(options: Options){
    super()   //初始化父类，父类的prototype.constructor.call
    this.options = options
    this.init()
  }
  init(): void {
    const data: Vnode = {
      tag: 'div',
      children: [
        {
          tag: 'section',
          text: '我是子节点1'，
          children: [
          	{
          		tag: 'div',
          		text: '我是子节点1的子节点'
        		}
          ]
          
        },
        {
        	tag: 'section',
          text: '我是子节点2',
        }
      ]
    }
  
  	const app = typeof this.options.el === 'string' ? document.querySelector(this.options.el) : this.options.el
  	app.appendChild(this.render(data))
  }
  
  static version(){}  //静态方法，静态方法中的this只能调用类中的静态方法
}

new Vue({
  el: '#app'
})



//get,set
class Ref {
  _value: string
  
  constructor(value: string){
    this._value = value
  }
  
  get value(){
    return this._value 
  }
  
  set value(newValue){
    this._value = newValue
  }
}
```



#### 抽象类

```ts
//abstract所定义的类为抽象类,无法被实例化
//abstract所定义的方法，都只能描述不能进行一个实现
abstract class Vue {
  name: string
  constructor(name?: string){
    this.name = name
  }
  
  getName(): string{
    return this.name
  }
  
  abstract init(name: string): void
}

class React extends Vue {
  constructor(){
    super()
  }
  
  init(name: string){
    
  }
  
  setName(name: string){
    this.name = name
  }
}
```



#### 元组

```ts
const arr: readonly [x: number, y?: boolean] = [1, false]  //只读元组
arr['length']   //读取元组的长度
```



#### 枚举

```ts
enum Color {
  red,	//0
  green,	//1
  blue	//2
}
```

![image-20230603233257325](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603233257325.png)

![image-20230603233339099](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603233339099.png)

![image-20230603233359055](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603233359055.png)

![image-20230603233416080](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603233416080.png)

![image-20230603233436149](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603233436149.png)



#### 类型推论，类型别名

TS拥有自动的类型判断机制

​	当对变量的声明和赋值是同时进行的，TS编译器会自动判断变量的类型，所以可以省略掉类型声明

​	声明变量如果不指定类型，则TS解析器会自动判断变量的类型为any（隐式any）

![image-20230603234817200](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603234817200.png)

![image-20230603234848610](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603234848610.png)

![image-20230603235227762](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603235227762.png)



#### never

```ts
type s = number & string
```

![image-20230603235353642](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603235353642.png)

![image-20230603235631505](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603235631505.png)

![image-20230603235658815](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230603235658815.png)



#### Symbol类型

```ts
const a1: symbol = Symbol(1)
const a2: symbol = Symbol(1)
a1 === a2 => false

//for,全局symbol有没有注册过这个key,如果有则直接拿来用，不创建新的。没有则创建新的
Symbol.for(1) === Symbol.for(1) => true
```



![image-20230604000109210](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000109210.png)

![image-20230604000140995](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000140995.png)

```ts
//生成器
function* gen(){
  yield Promise.resolve("1") //同步异步
  yield "2"
  yield "3"
  yield "4"
}

const m = gen()
console.log(m.next()) => { value: Promise{'1'}, done: false }
console.log(m.next()) => { value: '2', done: false }
console.log(m.next()) => { value: '3', done: false }
console.log(m.next()) => { value: '4', done: false }
console.log(m.next()) => { value: undefined, done: true }


//set
const set: Set<number> = new Set([1,1,2,3,4,5,5]) => [1,2,3,4,5]  //自动去重


//map
let map: Map<string, string> = new Map()
const str = '姓名'
map.set(str, 'zs')  //引用类型作为key
map.get(str) => 'zs'


//迭代器
function fu(){
  let iter: Funcion = arguments[Symbol.iterator]()
  let next: object = { value: '', done: false }
  while(!next.done){
    next = iter.next()
    if(!next.done){
      console.log(next.value)
    }
  }
}

//迭代器的语法糖for of
const arr:[number[], object, string] = [[1,2,3],{'zs'},'zs']
for(let value of arr){
  console.log(value)   //[[1,2,3],{'zs'},'zs']
}
//注意对象不能使用for of，因为对象上没有[Symbol.iterator]()方法
```



![image-20230604000211506](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000211506.png)

![image-20230604000234111](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000234111.png)

![image-20230604000307785](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000307785.png)

![image-20230604000327126](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000327126.png)

![image-20230604000350724](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604000350724.png)



#### 泛型

![image-20230604005229654](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604005229654.png)

```ts
type A<T> = string | number | T
const a: A<boolean> = true

interface Data<T> {
  msg: T
}

function add<T = number, K = number>(a: T, b: K): Array<K | T> {
  return [a, b]
}
add('123', [1,2,3])

const axios = {
  get<T>(url: string): Promise<T> {
		return new Promise((resolve, reject) => {
      const xhr: XMLHttpRequest = new XHLHttpRequest()
      xhr.open('GET', url)
      xhr.onreadystatechange = () => {
        if(xhr.readyState === 4 && xhr.status === 200){
					resolve(JSON.parse(xhr.responseText))
        }
      }
      xhr.send(null)
    })
  }
}
interface Data {
  message: string
  code: number
}
axios.get<Data>('./data.json').then(res => {
  console.log(res.code)
})
```

![image-20230604084701335](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604084701335.png)

![image-20230604084733859](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604084733859.png)

![image-20230604084759370](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604084759370.png)

```ts
const obj = { name = 'zs', age = 18 }
type Key = keyof typeof obj   => name | age

interface Data {
	name: string
  age: number
  sex: string
}
type Options<T extends object> = {
  [Key in keyof T]?: T[key]
}
type b = Options<Data>  => b = { 
	name?: string | undefined
  age?: number | undefined
  sex?: string | undefined
}
```



![image-20230604084824405](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604084824405.png)



#### namespace命名空间

![image-20230604100642528](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604100642528.png)

![image-20230604100707600](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604100707600.png)

![image-20230604100734668](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604100734668.png)

![image-20230604100809696](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604100809696.png)



#### 三斜线指令

![image-20230604101731681](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604101731681.png)

![image-20230604101807729](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604101807729.png)



#### 声明文件d.ts

![image-20230604102315380](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604102315380.png)

![image-20230604102413086](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604102413086.png)

![image-20230604102447589](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604102447589.png)

![image-20230604102521794](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604102521794.png)



#### Mixins混入

![image-20230604104434671](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604104434671.png)

![image-20230604104504661](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604104504661.png)

![image-20230604104527501](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604104527501.png)



#### 装饰器Decorator

##### 1.类装饰器 ClassDecorator

##### 2.属性装饰器 PropertyDecorator

##### 3.参数装饰器 ParameterDecorator

##### 4.方法装饰器 MethodDecorator  PropertyDecorator

![image-20230604105352897](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105352897.png)

![image-20230604105421991](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105421991.png)

![image-20230604105459006](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105459006.png)

![image-20230604105528387](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105528387.png)

![image-20230604105621105](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105621105.png)

```ts
import axios from 'axios'
import 'reflect-metadata'

const Get = (url: string):MethodDecorator => {
  const fn: MethodDecorator = (target, _, descriptor: PropertyDecorator) => {
    const key = Reflect.getMetadata('key', target)
    axios.get(url).then(res => {
      descriptor.value(key ? res.data[key] : res.data)
    })
  }
  
  return fn
}

const Result: ParameterDecorator = (target, key, index) => {
  Reflect.defineMetadata('key', 'result', target)
}

class A {
  @Get('https://xxxxxxx')
  getlist(@Result data: any){
    //console.log(data.result.list)
    console.log(data)
  }
}
```



![image-20230604105649372](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105649372.png)

![image-20230604105717832](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105717832.png)

![image-20230604105757540](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105757540.png)

![image-20230604105821641](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230604105821641.png)



#### 代理（proxy）与反射（Reflect)

![image-20230605103312861](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605103312861.png)

![image-20230605103450548](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605103450548.png)

![image-20230605103543886](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605103543886.png)

![image-20230605103619105](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605103619105.png)

```ts

//代理API
server:{
  proxy:{
		'/api':{
      target: 'xxxx'
    }
  }
}

const person = { name: 'zs', age: 24 }
//proxy支持对象、数组、函数、set、map
const personProxy = new Proxy(person, {
  //取值
  get(target, key, receiver) {
    if(typeof target[key] === 'string' | 'number'){
      return Reflect.get(target, key, receiver)
    }else {
      return '类型不匹配 '
    }
  },
  
  //赋值,person, 操作的属性, 所要赋的值, preson
  set(target, key, value,   receiver) {
    
    return true
  },
  
  //拦截函数调用
  apply(){
    
  },
  
})



const list: Set<Function> = new Set()
const autorun = (cb: Function) => {
  if(!list.has(cb)){
    list.add(cb)
  }
}

const observable = <T extends object>(params: T) => {
  return new Proxy(params, {
    set(target, key, value, receiver){
      const res = Reflect.set(target, key, value, receiver)
      list.forEach(fn => fn())
      return res
    }
  })
}

const person = observable({name:"zs", age:24})
autorun(() => {
  console.log('有变化了')
})

person.age = 18    => 	'有变化了'
```

![image-20230605085058857](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605085058857.png)

![image-20230605091131457](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605091131457.png)

![image-20230605091208703](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605091208703.png)

![image-20230605103212654](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605103212654.png)

![image-20230605103237173](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605103237173.png)



#### 协变，逆变，双向协变

![image-20230605104058866](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605104058866.png)

![image-20230605104116212](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605104116212.png)



![image-20230605104148361](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605104148361.png)

![image-20230605104209514](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605104209514.png)



![image-20230605104245107](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605104245107.png)

![image-20230605104302178](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605104302178.png)



#### weakMap, weakSet, set, map

![image-20230605105544434](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605105544434.png)

![image-20230605105607565](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605105607565.png)

 

![image-20230605105630106](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605105630106.png)



![image-20230605105655960](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605105655960.png)

 ```ts
 weakmap,map的区别：weakmap的key只能是引用类型
 ```



#### Partial与Pick

![image-20230605111106707](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605111106707.png)

```ts
type person = {
	name: string,
  age: number,
}

p in keyof person  => name | age
```



![image-20230605111128852](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605111128852.png)



![image-20230605111152944](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605111152944.png)



#### Record与Readonly

![image-20230605112850057](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605112850057.png)



![image-20230605112915351](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605112915351.png)

```ts
type K = 1 | 2 | 3
type Person = {
  name: string,
  age: number
}

type B = Record<K, Person>
const b: B = {
  1:{name:'zs', age" 18}
  2:{name:'ls', age" 18}
  3:{name:'wu', age" 18}
}
```



#### infer

![image-20230605114244874](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605114244874.png)

#### infer类型提取

![image-20230605144501011](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605144501011.png)

![image-20230605144524945](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605144524945.png)

#### infer递归

![image-20230605144954177](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605144954177.png)









## 编译选项

##### 自动编译文件

​	编译文件时，使用-w指令后，TS编译器会自动监视文件的变化，并在文件发生变化时对文件进行重新编译

##### 自动编译整个项目

```js
tsc -init   // 创建tsconfig.json配置文件
```



## 面向对象

 ![image-20230518114204804](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230518114204804.png)



















































t
