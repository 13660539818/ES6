# ES6
A project created by ES6

### 项目构建
#### 项目构建测试中出现的问题
1. **Q：** *Failed to load external moudle @babel/register*  
   **A：** gulp版本问题，降低gulp的版本至3.9.0
   > npm install -g gulp@3.9.0
   > npm install gupl@3.9.0 --save
2. **Q：** *Requiring external module babel-register*  
   **A：** 之前一直以为这也是个问题，然后去百度发现很多人都有出现这个问题，但是都没有解决方案，后面发现它并不是问题，只是项目构建的第一个过程（应该）。
3.  webpack版本问题引发的一系列问题如下：
    * **Q：** *Configuration.module has an unknown property 'loaders.'*  
      **A：** webpack v4 官方文档:  
      > removed module.loaders
      把 "loaders" 用 "rules" 表示
    * **Q：** *Plumber found unhandled error: Error in plugin"webpack-stream"*  
    *Module not found: Error: Can't resolve 'babel' in 'D:\Chashao\practice\front-end\08-ES6' BREAKING CHANGE: It's no longer allowed to omit the '-loader' suffix when using loaders.\*\*You need to specify 'babel-loader' instead of 'babel'\*\**  
      **A：** 根据错误提示把把 "babel" 改为 "babel-loader" 表示
    * **Q：** *The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' option to 'development' or 'production' to enable defaults for each environment.*  
      **A：** webpack v4 官方文档:
      > You have to choose ( mode or --mode ) between two modes now: production or development
      在相应的位置加上代码:
      > mode: production
      ***
      综上：将"/tasks/scripts.js"里面的代码段
      ```
      .pipe(gulpWebpack({
        module:{
          loaders:[{
            test:/\.js$/,
            loader:'babel'
          }]
        }
      })
    ```
    改为
    ```
      .pipe(gulpWebpack({
        mode: "production",
        module:{
          rules:[{
            test:/\.js$/,
            loader:'babel-loader'
          }]
        }
      })
    ```  
    还有一种最简单直接的方法，就是降低webpack的版本，但我觉得这也是最愚蠢的方法，我们应该学会适应新版本的特性，在新版本的基础上找出解决的方法。

   
