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

##### 循环
######  while循环
	while (   ) {
						
	}
######  for循环
	for i in a.iter() {  
	        println!("值为 : {}", i);  
	}
######  loop 循环
	loop{
	
		break;
	}			
	使用break中断循环和返回值 break i;


						
##### 闭包
	`语法声明：
	let closure_name = |参数列表| 表达式或语句块;`
	





































