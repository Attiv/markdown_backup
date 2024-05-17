```Plain

\#ifdef DEBUG   //调试阶段

//...表示在宏里面的可变参数
//__VA_ARGS__表示宏里面的可变参数
\#define VLog(fmt, ...) NSLog((@"%s [Line %d] " fmt), __PRETTY_FUNCTION__, __LINE__, ##__VA_ARGS__);

\#else          //发布阶段

\#define SLog(...)

\#endif




// SWwift 
func VTLog<T>(message : T,file : String = \#file,funcName : String = \#function,lineNum : Int = \#line) {
    
    \#if DEBUG  
        
    let fileName = (file as NSString).lastPathComponent
        
    print("\(fileName):[\(funcName)](\(lineNum)) -\(message)")
        
    \#endif
}
```