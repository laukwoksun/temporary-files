##### 变量作用域
```
// 修复错误
fn main() {
    println!("{}, world", x); 
}

fn define_x() {
    let x = "hello";
}
```
1. 因为答案的函数返回的值是String类型，而"hello"在Rust中是另一种类型：&str（本身是一个字符串切片）。所以，为了让返回值的类型和签名的返回类型一致，需要通过.to_string()方法将String类型转换为&str类型。
```
fn main() {
    let x = define_x();
    println!("{}, world", x);
}

fn define_x() -> String {
    let x = "hello".to_string();
    x
}
```
2. 如果要返回&str的话，应该是这样的：
```
fn main() {
    println!("{}, world",define_x());
}

fn define_x<'a>() -> &'a str {
    let x = "hello";
    x
}
```