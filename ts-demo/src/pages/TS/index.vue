<script setup lang="ts">
import { ref } from 'vue'

//原始数据类型
let num: number = 1
let isDone = false
let myName: string = 'Tom'
let myFavoriteNumber: any = 'seven'

//任意值
let anyThing: any = 'hello'
console.log(anyThing.name)
let anyThing1: any
console.log(anyThing?.name)
let something //等价于 let something: any

//类型推论
let a = 1 //等价于 let a: number = 1
// a = '2' 会报错

//联合类型
let test: string | number
test = 1
test = '22'
function getString(something: string | number): string {
  return something.toString() //访问联合类型的属性时，需要访问共有属性  something.length会报错
}

//接口
interface IPerson {
  name: string
  age: number
  sex?: number //可选属性
  [propName: string]: any //任意属性
  readonly id: number //只读属性
}
let tom: IPerson = {
  name: 'Tom',
  age: 25,
  id: 111
}

//数组的类型
const arr1: number[] = []
const arr2: Array<number> = [] //使用数组泛型表示
interface NumberArray {
  //使用接口表示
  [index: number]: number
}
const arr3: NumberArray = [1, 1, 2, 3, 5]
const arr4 = ref<Array<number>>([1, 2, 3])

//函数的类型
function sum(x: number, y: number, z?: string, w: string = 'cat'): number {
  //z?:string 可选参数 后面不允许再添加必选参数
  // w: string = 'cat' TypeScript 会将添加了默认值的参数识别为可选参数
  return x + y
}

//类型断言

let b = {} as any
b.name = 111

//类型别名
type Name = string
type Age = number
type Other = Name | Age

//元祖
let toms: [string, number] = ['1', 2]
toms.push('3')
console.log(toms)
// toms.push(true)  只能添加添加联合元素

//enum 枚举
enum Days {
  Sun = 2, //不赋值会从0开始
  Mon,
  Tue,
  Wed,
  Thu,
  Fri,
  Sat
}
console.log(Days.Sun)
console.log(Days[0])

//泛型
function createArray<T = string>(length: number, value: T): Array<T> {
  let result: T[] = []
  for (let i = 0; i < length; i++) {
    result[i] = value
  }
  return result
}
console.log(createArray(3, 'a'))

function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]]
}
console.log(swap(['1', 2]))

//泛型约束
interface Lengthwise {
  length: number
}
function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length)
  return arg
}
// loggingIdentity(7)   传入的参数必须包含length

function copyFields<T extends U, U>(target: T, source: U): T {
  for (let id in source) {
    target[id] = (<T>source)[id]
  }
  return target
}

let x = { a: 1, b: 2, c: 3, d: 4 }

copyFields(x, { b: 10, d: 20 })
</script>

<template>
  <div>
    {{ num }}
  </div>
</template>

<style scoped></style>
