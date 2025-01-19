## 环境搭建

### **1、Rust**

[**https://forge.rust-lang.org/infra/other-installation-methods.html**](https://forge.rust-lang.org/infra/other-installation-methods.html)

### **2、Visual Studio**

在 Rust 针对 Windows 上的 MSVC 目标平台进行编译时，它依赖于 Visual Studio 自带的链接器 `link.exe` 来完成最终的链接步骤生成可执行文件。需要在安装过程中的 “工作负载” 选项里，确保勾选 **“**使用 C++ 的桌面开发**“**。

上面环境配置好，可以在终端：

### **3、编辑器**

**VSCode**

项目路径下里面新建一个新的文件夹 .vscode （如果有这个文件夹就不需要新建了）。在新建的 .vscode 文件夹里新建两个文件 tasks.json 和 launch.json，文件内容如下：

task.json：

```
{ 
    "version": "2.0.0", 
    "tasks": [ 
        { 
            "label": "build", 
            "type": "shell", 
            "command":"cargo", 
            "args": ["build"] 
        } 
    ] 
}
```

launch.json：

```
{   
    "version": "0.2.0",   
    "configurations": [   
        {   
            "name": "(Windows) 启动",   
            "preLaunchTask": "build",   
            "type": "cppvsdbg",   
            "request": "launch",   
            "program": "${workspaceFolder}/target/debug/${workspaceFolderBasename}.exe",   
            "args": [],   
            "stopAtEntry": false,   
            "cwd": "${workspaceFolder}",   
            "environment": [],   
            "externalConsole": false   
        },   
        {   
            "name": "(gdb) 启动",   
            "type": "cppdbg",   
            "request": "launch",   
            "program": "${workspaceFolder}/target/debug/${workspaceFolderBasename}.exe",   
            "args": [],   
            "stopAtEntry": false,   
            "cwd": "${workspaceFolder}",   
            "environment": [],   
            "externalConsole": false,   
            "MIMode": "gdb",   
            "miDebuggerPath": "这里填GDB所在的目录",   
            "setupCommands": [   
                {   
                    "description": "为 gdb 启用整齐打印",   
                    "text": "-enable-pretty-printing",   
                    "ignoreFailures": true   
                }   
            ]   
        }   
    ]   
}
```

然后就开始使用 VSCode 左栏的 "运行"调试。

如果你使用的是 MSVC 选择 "(Windows) 启动"。

如果使用的是 MinGW 且安装了 GDB 选择"(gdb)启动"，gdb 启动前请注意填写 launch.json 中的 "miDebuggerPath"。

### **4、Cargo**

Cargo 除了创建工程以外还具备构建（build）工程、运行（run）工程等一系列功能，构建和运行分别对应以下命令：

- `cargo new <project-name>`：创建一个新的 Rust 项目。
    
- `cargo build`：编译当前项目。
    
- `cargo run`：编译并运行当前项目。
    
- `cargo check`：检查当前项目的语法和类型错误。
    
- `cargo test`：运行当前项目的单元测试。
    
- `cargo update`：更新 Cargo.toml 中指定的依赖项到最新版本。
    
- `cargo --help`：查看 Cargo 的帮助信息。
    
- `cargo publish`：将 Rust 项目发布到 crates.io。
    
- `cargo clean`：清理构建过程中生成的临时文件和目录。

### 5、输出到命令行

使用 rustc 命令编译 runoob.rs 文件：

```
 rustc runoob.rs   # 编译 runoob.rs 文件
```

编译后会生成 **runoob** 可执行文件：

```
 ./runoob    # 执行 runoob
```



---



## 代码相关

##### `let s1 = String::from("hello")`
这里 “ String::from ” 是指String类库的from方法


 ##### Rust 有两种主要的错误处理方式：Result<T, E> 和 Option<T>

###### Result
```
enum Result<T, E> {
    Ok(T),
    Err(E),
}

fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err(String::from("Division by zero"))
    } else {
        Ok(a / b)
    }
}

if let Ok(result) = divide(88, 0) {
	println!("Result: {}", result);
} else {
	println!("An error occurred");
}
```

###### Option
```
fn get_element(index: usize, vec: &Vec<i32>) -> Option<i32> {
    if index < vec.len() {
        Some(vec[index])
    } else {
        None
    }
}
```
##### 字符串
1. 字符串字面量（`&str`）
字符串字面量是不可变的，它们在编译时被硬编码到程序的二进制文件中。它们的类型是 `&str`，是对存储在二进制文件中的字符串切片的引用。		
						`let str: &str = "Hello, Rust!";`

 2. `String` 类型
`String` 类型是可变的，存储在堆上，可以在运行时修改其内容。	
`let mut string_var = String::new(); `
`//String::from("Hello, Rust!");` 
`string_var.push_str("Hello, Rust!");`  
					
##### 数组
						
在 Rust 中，数组的长度是固定的，一旦声明，其长度不能更改。如果需要一个可变长度的数据结构，可以考虑使用 `Vec`（向量），它是动态数组，可以根据需要添加或删除元素。
`let arrary:[i32; 5] = [1, 2, 3, 4, 5];`
 `let mut vec = !vec(1,2,3,4,5)`
```
fn main() {
    let mut iter = (1..5).into_iter(); 
    while let Some(val) = iter.next() { 
        println!("{}", val); 
    }
}
```
- 代码解释（详细）：
`首先，使用 (1..5).into_iter() 创建了一个从 1 到 4 的迭代器。`
`在 while let Some(val) = iter.next() 中，每次调用 iter.next()：`
`第一次调用 iter.next() 会返回 Some(1)，将 1 绑定到 val，并打印 1。`
`第二次调用会返回 Some(2)，将 2 绑定到 val，并打印 2，以此类推。`
`当迭代器遍历完所有元素后，iter.next() 会返回 None，循环结束`。
- 总结：
`Some 是 Option 枚举的一个变体，用于表示可能存在的值。`
`while let Some(val) = iter.next() 是一种方便的方式，利用模式匹配来遍历迭代器，直到迭代器耗尽（返回 None）。`
`迭代器的 next 方法允许你逐个访问元素，并且通过 Some 和 None 来表示是否还有元素可访问，这是 Rust 中处理可能不存在的值的安全和简洁的方式，避免了许多其他语言中使用 null 或 nil 可能导致的空指针错误。`					

##### 所有权
###### 1. 所有权
`每个值在任意时刻只能有一个所有者。`
`当所有者超出作用域时，值会被删除。`
###### 2. 引用
`在 Rust 中，引用是一种指向数据的指针，允许你使用已经存在的数据而无需拥有其所有权。`
###### 3. 借用
`借用是创建引用的动作或过程，是一种机制，用于在不获取所有权的情况下使用数据。可以说引用是借用的结果。借用允许引用数据而不获取所有权，通过 & 符号实现。`
```
- 借用是一种操作或概念，通过借用可以创建引用。引用是借用的产物，是指向数据的指针。
```
###### 4. 解引用操作 
`在 Rust 中，解引用操作是通过 * 运算符来实现的，它允许你访问引用所指向的值。当你有一个引用（如 &T 或 &mut T）时，解引用操作会让你得到引用所指向的实际值。`
```
fn main() { 
	let x = 5; 
	let reference = &x; // 创建一个对 x 的引用 
	let dereferenced_value = *reference; // 解引用操作 
	println!("x 的值是: {}", x); 
	println!("引用指向的值是: {}", reference); 
	println!("解引用后的值是: {}", dereferenced_value); 
}
```
解释：
let x = 5;：定义一个变量 x，其值为 5。
let reference = &x;：创建一个对 x 的引用。这里 reference 是 &i32 类型，它存储了 x 的地址，而不是值本身。
let dereferenced_value = *reference;：使用 * 运算符对 reference 进行解引用操作，得到 x 的实际值。这里 dereferenced_value 是 i32 类型，其值为 5。
































