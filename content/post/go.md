---
title: "Go 语言基础"
date: 2023-05-10T16:45:58+08:00
lastmod: 2023-05-10T16:45:58+08:00
draft: false
tags: ["Go"]
categories: ["Programming"]

---

## Go 语言基础语法
### 标识符
标识符 是一个或是多个字母(A~Z和a~z)数字(0~9)、下划线_组成的序列，但是第一个字符必须是字母或下划线而不能是数字。

### 关键字

| break | default | func | interface | select |
| :---- | :------ | :--- | :-------- | :----- |
| case | defer | go | map | struct |
| chan | else | goto | package | switch |
| const | fallthrough | if | range | type |
| continue | for | import | return | var |

还有 36 个预定义标识符：
| append | bool | byte | cap | close | complex | complex64 | complex128 | uint16 |
| :----- | :--- | :--- | :-- | :---- | :------ | :------- | :-------- | :----- |
| copy | false | float32 | float64 | imag | int | int8 | int16 | uint32 |
| int32 | int64 | iota | len | make | new | nil | panic | uint64 |
| print | println | real | recover | string | true | uint | uint8 | uintptr |

### 空格
变量的声明必须使用空格隔开
```go
var age int
```
在关键字和表达式之间要使用空格
```go
if age > 18 {
    fmt.Println("成年人")
}
```
在函数调用时，函数名和左边等号之间要使用空格，参数之间也要使用空格

```go
result := add(2, 3)
```

### 格式化字符串
Sprintf 根据格式化参数生成格式化的字符串并返回该字符串。
Printf 根据格式化参数生成格式化的字符串并写入标准输出。
```go
var name string = "张三"
var age int = 18
fmt.Sprintf("name: %s, age: %d", name, age)
var person = fmt.Sprintf("name: %s, age: %d", name, age)
fmt.Println(person)
```

## 语言数据类型
### 布尔类型
布尔类型的值只可以是常量 true 或者 false。一个简单的例子：var b bool = true。
### 字符串类型
字符串就是一串固定长度的字符连接起来的字符序列。Go 的字符串是由单个字节连接起来的。Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文本。
### 派生类型
包括：
- 指针类型（Pointer）
- 数组类型
- 结构化类型(struct)
- Channel 类型
- 函数类型
- 切片类型
- 接口类型（interface）
- Map 类型
- 管道类型
- 
### 数字类型
Go 语言支持整数、浮点数和复数，Go 语言同时支持以下这些类型的数字：
| uint8 | uint16 | uint32 | uint64 | int8 | int16 | int32 | int64 |
| :---- | :----- | :----- | :----- | :--- | :---- | :---- | :---- |
| byte | rune | uint | int | uintptr | float32 | float64 | complex64 |
| complex128 |

## 变量&常量
### 变量声明
```go
var name string
var age int
var isAdult bool
```
### 变量赋值
```go
var name string = "张三"
var age int = 18
var isAdult bool = true
```
### 变量类型推断
```go
var name = "张三"
var age = 18
var isAdult = true
```
### 短变量声明
```go
name := "张三"
age := 18
isAdult := true
// var 定义的变量可以在函数外部使用，而短变量声明定义的变量只能在函数内部使用
// := s声明与 var 定义的变量 不能在同一个作用域中使用
```
### 多变量声明
```go
var name, age, isAdult = "张三", 18, true
```
### 匿名变量
匿名变量是一个特殊的变量名，用来忽略某个值。例如，fmt.Println 函数返回两个值，一个是输出的字节数，另一个是可能的错误。但是如果你不想要第一个值，只想要第二个值，可以使用匿名变量。
```go
func main() {
    _, err := fmt.Println("Hello World")
    if err != nil {
        fmt.Println("发生错误")
    }
}
```
### 常量
常量是一个简单值的标识符，在程序运行时，不会被修改的量。常量中的数据类型只可以是布尔型、数字型（整数型、浮点型和复数）和字符串型。
```go
const name string = "张三"
const age int = 18
const isAdult bool = true
```

### iota
iota 在 const 关键字出现时将被重置为 0，const 中每新增一行常量声明将使 iota 计数一次（iota 可理解为 const 语句块中的行索引）。
常用业务场景为：枚举
```go
const (
    a = iota
    b = iota
    c = iota
)
fmt.Println(a, b, c) // 0 1 2
```
常用场景：
```go

const (
    a = iota
    b
    c
)
fmt.Println(a, b, c) // 0 1 2
```
```go
const (
    a = iota
    b = "B"
    c = iota
    d, e, f = iota, iota, iota
    g       = iota
)

fmt.Println(a, b, c, d, e, f, g) // 0 B 2 3 3 3 6
```



## 运算符
### 算术运算符
| 运算符 | 描述 | 实例 |
| :----- | :--- | :--- |
| + | 相加 | A + B 输出结果 30 |
| - | 相减 | A - B 输出结果 -10 |
| * | 相乘 | A * B 输出结果 200 |
| / | 相除 | B / A 输出结果 2 |
| % | 求余 | B % A 输出结果 0 |
| ++ | 自增 | A++ 输出结果 11 |
| -- | 自减 | A-- 输出结果 9 |

### 关系运算符
| 运算符 | 描述 | 实例 |
| :----- | :--- | :--- |
| == | 检查两个值是否相等，如果相等返回 True 否则返回 False。 | (A == B) 为 False。 |
| != | 检查两个值是否不相等，如果不相等返回 True 否则返回 False。 | (A != B) 为 True。 |
| > | 检查左边值是否大于右边值，如果是返回 True 否则返回 False。 | (A > B) 为 False。 |
| < | 检查左边值是否小于右边值，如果是返回 True 否则返回 False。 | (A < B) 为 True。 |
| >= | 检查左边值是否大于等于右边值，如果是返回 True 否则返回 False。 | (A >= B) 为 False。 |
| <= | 检查左边值是否小于等于右边值，如果是返回 True 否则返回 False。 | (A <= B) 为 True。 |

### 逻辑运算符
| 运算符 | 描述 | 实例 |
| :----- | :--- | :--- |
| && | 逻辑 AND 运算符。 如果两边的操作数都是 True，则为 True，否则为 False。 | (A && B) 为 False。 |
| \|\| | 逻辑 OR 运算符。 如果两边的操作数有一个 True，则为 True，否则为 False。 | (A \|\| B) 为 True。 |
| ! | 逻辑 NOT 运算符。 如果条件为 True，则为 False，否则为 True。 | !(A && B) 为 True。 |

### 位运算符
| 运算符 | 描述 | 实例 |
| :----- | :--- | :--- |
| & | 参与运算的两数各对应的二进位相与。（两位均为1才为1） | (A & B) 结果为 12, 二进制为 0000 1100 |
| \| | 参与运算的两数各对应的二进位相或。（两位有一个为1就为1） | (A \| B) 结果为 61, 二进制为 0011 1101 |
| ^ | 参与运算的两数各对应的二进位相异或。（两位不一样则为1） | (A ^ B) 结果为 49, 二进制为 0011 0001 |
| << | 左移n位就是乘以2的n次方。 | A << 2 结果为 240 ，二进制为 1111 0000 |
| >> | 右移n位就是除以2的n次方。 | A >> 2 结果为 15 ，二进制为 0000 1111 |

### 赋值运算符
| 运算符 | 描述 | 实例 |
| :----- | :--- | :--- |
| = | 简单的赋值运算符，将一个表达式的值赋给一个左值 | C = A + B 将 A + B 的运算结果赋值给 C |
| += | 相加后再赋值 | C += A 等于 C = C + A |
| -= | 相减后再赋值 | C -= A 等于 C = C - A |
| *= | 相乘后再赋值 | C *= A 等于 C = C * A |
| /= | 相除后再赋值 | C /= A 等于 C = C / A |
| %= | 求余后再赋值 | C %= A 等于 C = C % A |
| <<= | 左移后赋值 | C <<= 2 等于 C = C << 2 |
| >>= | 右移后赋值 | C >>= 2 等于 C = C >> 2 |
| &= | 按位与后赋值 | C &= 2 等于 C = C & 2 |
| ^= | 按位异或后赋值 | C ^= 2 等于 C = C ^ 2 |
| \|= | 按位或后赋值 | C \|= 2 等于 C = C \| 2 |

### 其他运算符
| 运算符 | 描述 | 实例 |
| :----- | :--- | :--- |
| & | 返回变量存储地址 | &a; 将给出变量的实际地址。 |
| \* | 指针变量。 | \*a; 是一个指针变量 |

### 运算符优先级
| 优先级 | 运算符 |
| :----- | :--- |
| 7 | ^ |
| 6 | \* / % << >> & &^ |
| 5 | + - \| ^ |
| 4 | == != < <= >= > |
| 3 | <\- |
| 2 | && |
| 1 | \|\| |
| 0 | = += -= \*= /= %= <<= >>= &= ^= \|= |










