## 定义方法

Rust 使用 impl 来定义方法，例如以下代码：

```Rust
struct Circle {
    x: f64,
    y: f64,
    radius: f64,
}

impl Circle {
    // new是Circle的关联函数，因为它的第一个参数不是self，且new并不是关键字
    // 这种方法往往用于初始化当前结构体的实例
    fn new(x: f64, y: f64, radius: f64) -> Circle {
        Circle {
            x: x,
            y: y,
            radius: radius,
        }
    }

    // Circle的方法，&self表示借用当前的Circle结构体
    fn area(&self) -> f64 {
        std::f64::consts::PI * (self.radius * self.radius)
    }
}
```

## self、&self 和 &mut self

在 area 的签名中，我们使用 &self 替代 rectangle: &Rectangle，&self 其实是 self: &Self 的简写（注意大小写）。在一个 impl 块内，Self 指代被实现方法的结构体类型，self 指代此类型的实例，换句话说，self 指代的是 Rectangle 结构体实例

1. self 表示 Rectangle 的所有权转移到该方法中，这种形式用的较少
2. &self 表示该方法对 Rectangle 的不可变借用
3. &mut self 表示可变借用

## 关联函数

定义在 impl 中且没有 self 的函数被称之为关联函数： 因为它没有 self，不能用 f.read() 的形式调用，因此它是一个函数而不是方法，它又在impl 中，与结构体紧密关联，因此称为关联函数。

在之前的代码中，我们已经多次使用过关联函数，例如 String::from，用于创建一个动态字符串。
```Rust
impl Rectangle {
    fn new(w: u32, h: u32) -> Rectangle {
        Rectangle { width: w, height: h }
    }
}
```

## 为枚举实现方法
```Rust
#![allow(unused)]
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

impl Message {
    fn call(&self) {
        // 在这里定义方法体
    }
}

fn main() {
    let m = Message::Write(String::from("hello"));
    m.call();
}
```