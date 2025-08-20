# 🧩 PointerTracker – LLVM Pass for Memory Access Tracing  

![LLVM](https://img.shields.io/badge/LLVM-14+-blue?logo=llvm)  
![C++](https://img.shields.io/badge/C++-17-orange?logo=cplusplus)  
![Clang](https://img.shields.io/badge/Clang-Compiler-lightgrey?logo=clang)  
![License](https://img.shields.io/badge/License-Educational-green)  

---

## 📌 Overview  
**PointerTracker** is a custom **LLVM Function Pass** that instruments programs to monitor memory accesses at runtime.  
For each function, it logs the function name and records the **hexadecimal addresses** of every memory read and write.  
The results are output in **CSV format**, making analysis simple and structured.  

This project is important because it enables:  
- 🔍 **Debugging** → Identify memory access patterns causing segmentation faults or memory leaks.  
- 🔐 **Security Analysis** → Detect suspicious memory behavior that could indicate vulnerabilities.  
- ⚡ **Performance Profiling** → Study memory locality and optimize cache performance.  
- 📖 **Program Comprehension** → Gain deeper insights into how compiled programs actually interact with memory.  

---

## 🚀 Features  
- LLVM-based **automatic instrumentation** (no source code modification needed).  
- Runtime logging of pointer addresses for every function.  
- **CSV output** for easy visualization and analysis.  
- Lightweight and compiler-integrated, suitable for research and educational use.  

---

## 🛠️ Requirements  
- **LLVM 14+**  
- **Clang**  
- **CMake**  
- **Ninja (optional)**  

---

## ⚙️ Usage  

### 1. Compile C to LLVM IR  
```bash
clang -Xclang -disable-O0-optnone -S -emit-llvm test.c -o test.ll
```

### 2. Run the PointerTracker Pass  
```bash
opt -load-pass-plugin ./PointerTracker.so -passes="function(pointer-tracker)" test.ll -o instrumented.ll
```

### 3. Compile Instrumented IR  
```bash
clang instrumented.ll -o test_exec
```

### 4. Run Executable  
```bash
./test_exec
```

---

## 📊 Example Output  

Input C code:  
```c
#include <stdio.h>
void foo() {
    int x = 10;
    int *p = &x;
    printf("%p\n", (void*)p);
}
int main() {
    foo();
    return 0;
}
```

CSV Output:  
```
foo,0x7ffe1234
main,0x7ffe5678
```

---

## 🔮 Future Enhancements  
- Add support for **multi-threaded logging**.  
- Extend to **loop-level and module-level analysis**.  
- Provide **real-time visualization** of memory access.  
- Export results in multiple formats (JSON, XML).  

---

## 📜 License  
This project is licensed for **educational and research purposes only**.  
