## 2021-10-07

- Install Electron
    - Show simple hello world
        [Official quick start](https://www.electronjs.org/docs/tutorial/quick-start)

- Build simple foo.dll
    - `myfoolib.cc`
        ```c++
        extern "C" {
        __declspec(dllexport) double fooGetCpuTemp();
        __declspec(dllexport) double fooSumNum(double a, double b);
        }
        ```
    - Compile. Use VS x64 for compiling 64-bit library
        ```powershell
        cl /LD /DWIN64 /DWIN32 ./myclib.cc
        ```
    - Use python ctype see if it work.
        ```python
        import ctypes
        foo = ctypes.CDLL('./myclib.dll')
        foo.fooGetCpuTemp()
        ```

- Install ffi-napi for calling library API.
    ```bash
    npm i ffi-napi
    ```
- Call foo.dll from electron app
    - Error:
        - 126: dll not found
        - 127: function not found
        - 129:
- (Extra) Learning basic cmake in MSVC

### Reference
- [Calling into thread-unsafe DLLs with node-ffi](https://medium.com/doctolib/calling-into-thread-unsafe-dlls-with-node-ffi-1ef83806a50c)
- [Nodejs呼叫Dll模組的方法](https://www.itread01.com/article/1537173380.html)
- [Cmake Windows Build](https://sumo.dlr.de/docs/Installing/Windows_Build.html)
- [Windows下Cmake與VS聯合制作dll](https://www.itread01.com/content/1547759736.html)

## 2021-10-08

- `document.querySelector()`: With a querySelector statement, you can select an element based on a CSS selector. This means you can select elements by ID, class, or any other type of selector.
    - `document.querySelector(#myid);`: select by ID
    - `document.querySelector(.myclass);`: select by CSS class name
    - `document.querySelector("p.example");`: Get the first <p> element in the document with class="example"
- `document.querySelectorAll()`: a list of the document's elements that match the specified group of selectors.
- `var` hoisting: var declaration are processed before any code is execute. what the ???
    ```javascript
    // for example
    bla = 2;
    var bla;
    // ...is implicitly understood as:
    var bla;
    bla = 2;
    ```
- `let`: only in one scope. can't declare twice.
- Type of Variable:
    - Numbers
    - String
    - Boolen
    - Array
    - Object

### Reference
- [document.querySelector](https://developer.mozilla.org/zh-TW/docs/Web/API/Document/querySelector)
- [Document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)

## 2021-10-12

- Install scoop (best thing ever seen in win10 so far, maybe try chocolatey future)
    - git, nodejs, python, neovim, neovide
- maybe understood dll search order
- Create basic electron app
- Use `electron-builder` package electron app
- msvs x64 for powershell!!
- I think I need to start learning UI framewor...
- *want to update my log with my github.io*

### Reference
- [DLL search on windows](https://stackoverflow.com/questions/2463243/dll-search-on-windows)
- [dll search order](https://docs.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order)
- [electron-builder](https://github.com/electron-userland/electron-builder)
- [用 electron-builder 打包應用程式給其他人](https://ithelp.ithome.com.tw/articles/10234399)
- [Building desktop applications with Electron - electron-builder](https://medium.com/@jamzi/building-desktop-applications-with-electron-electron-builder-47484193cbcc)
- [x64 Developer PowerShell for VS 2019](https://developercommunity.visualstudio.com/t/x64-developer-powershell-for-vs-2019/943058)

## 2021-10-18
- Use wsl edit file, but use `npm` and `node` on windows host
- Want to export class and able to use in ffi-napi
    - Solve by using `virtual` as class inference and function wrapper.
- Why `__dllexport`

### Reference

- [從DLL導出C ++類 (Exporting a C++ class from a DLL)](https://zh-tw.coderbridge.com/discussions/15a8be04e5a840d18c44789d0091f1e5)
- [Why to use \__declspec(dllexport)? Seems to be working without it](https://stackoverflow.com/questions/1641172/why-to-use-declspecdllexport-seems-to-be-working-without-it)
- [What's the return type of ffi when using a constructor function from c++](https://stackoverflow.com/questions/40556955/whats-the-return-type-of-ffi-when-using-a-constructor-function-from-c) I CAN'T reproduce his code
- [ffi-napi common usage](https://github.com/node-ffi/node-ffi/wiki/Node-FFI-Tutorial#common-usage) Successful reproduce

## 2021-10-19
- wsl change default user:

    ```
    <DistributionName> config --default-user <Username>
    ```
