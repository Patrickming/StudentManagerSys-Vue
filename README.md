# StudentManagerSys-Vue
StudentManagerSystem - use Vue 

#### 介绍

该项目是基于**Vue2**的学生成绩管理系统-前端 

整体项目名称为学生成绩管理系统，技术选型为前后端分离，前端基于Vue.js，后端基于Java语言开发，使用了SpringBoot和MyBatis框架提高开发效率和质量。主要面向高校教育中学生管理、课程管理、教师管理、成绩管理、成绩统计等需求。

对应后端请看[StudentManagerSystem - JavaApi-backend (github.com)](https://github.com/Patrickming/StudentManagerSysApi)



#### 安装教程

1. 下载依赖

```bash
npm i
```

2. 修改端口

./config/index.js
\axios\axiosHelper.js
src\vuex\store.js
修改成对应的端口
```js
host: 'localhost', 
port: 8081, 

module.exports = {
  dev: {

    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '/api': {
        target: 'http://localhost:8080/', //接口域名
        // secure: false,
        changeOrigin: true, // 如果接口跨域，需要进行这个参数配置
        pathRewrite: {
          '^/api': ''
        }
      }
    }

axios.defaults.baseURL ='http://localhost:8080/'; //配置请求地址

const state = {
  baseApi: "http://localhost:8080/",
  collapse: {},
  userInfo: JSON.parse(localStorage.getItem('userInfo')),
};
```

3. 运行项目

```bash
npm run dev
npm run start
```





#### 使用说明

##### 1 基本功能

分为3种角色：管理员、学生、教师  不同用户登录会有不同功能展示

- 用户管理
  - 新增用户信息
  - 删除用户信息
  - 修改用户信息
  - 条件查询用户信息
- 课程管理
  - 创建
  - 修改
  - 删除
  - 条件查询
- 课程表管理
  - 课程表录入
  - 课程表修改
- 成绩管理
  - 录入
  - 修改
  - 统计以及可视化

##### 2 页面展示

![image-20240115160720173.png (1995×1018) (raw.githubusercontent.com)](https://raw.githubusercontent.com/Patrickming/StudentManagerSys-Vue/main/assets/image-20240115160720173.png)

###### 管理员

![image-20240115155846971.png (2548×1304) (raw.githubusercontent.com)](https://raw.githubusercontent.com/Patrickming/StudentManagerSys-Vue/main/assets/image-20240115155846971.png)

![image-20240115160011529.png (2540×1183) (raw.githubusercontent.com)](https://raw.githubusercontent.com/Patrickming/StudentManagerSys-Vue/main/assets/image-20240115160011529.png)

![image-20240115160415597.png (2554×1137) (raw.githubusercontent.com)](https://raw.githubusercontent.com/Patrickming/StudentManagerSys-Vue/main/assets/image-20240115160415597.png)

###### 教师

![image-20240115160529178.png (2560×1161) (raw.githubusercontent.com)](https://raw.githubusercontent.com/Patrickming/StudentManagerSys-Vue/main/assets/image-20240115160529178.png)

###### 学生

![image-20240115160756611.png (2539×1095) (raw.githubusercontent.com)](https://raw.githubusercontent.com/Patrickming/StudentManagerSys-Vue/main/assets/image-20240115160756611.png)



#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request
