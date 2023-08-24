1.编程式路由跳转到当前路由（参数不变），多次执行会抛出navigationuplicated的警告错误？
 --路由跳转有两种形式：声明式导航，编程式导航
 --声明式导航是没有这类问题的，因为vue-router底层已经处理好了
 1.1 为什么编程式导航进行路由跳转的时候就有这种警告错误？
 最新的vue-router引入了promise 
 function push () {
    return new Promise ((resolve,reject)) => {
        
    }
 }
 1.2 通过给push方法传递相应的成功，失败回调函数，可以捕获到当前的错误，可以解决
 1.3 通过下面的代码可以解决错误
this.$router.push({ name: "search", params: { keyword: this.keyword }, query: { k: this.keyword.toUpperCase() } }, () => { }, (err) => {  console.log(err) })
这种写法：治标不治本，将来在别的组件当中，push｜replace，编程式导航还是有类似的问题

1.4
this:当前组件实例（search）
this.$router属性：当前的这个属性，属性值VueRouter类的一个实例，当在入口文件注册路由的时候，给组件
实例添加$router|$route属性
push:VueRouter类的一个实例

function VueRouter() {

}
原型对象的方法
VueRouter.prototype.push = function(){
 函数的上下文为VueRouter类的一个实例
}
let $router = new VueRouter();
$router.push(xxx);

this.$router.push();

2:Home模块组件拆分
--先把静态页面完成
--拆分出静态组件
--获取服务器数据进行展示
--动态业务

3:三级联动组件完成
--由于三级联动，在home，search，detail，把三级联动注册为一个全局组件。
好处：只需要注册一次，就可以在项目任意地方使用。

4:完成其余静态组件
HTML + css + 图片资源---【结构，样式，图片资源】

5:postman接口测试
--如果服务器返回code字段200，代表服务器返回成功
--所有接口的前缀都有/api前缀

6:axios 二次封装
XMLHttpRequest, fetch, JQ,axios
6.1 为什么需要进行二次封装axios？
请求拦截器，相应拦截器。
请求拦截器：可以在发请求之前处理一些业务
相应拦截器：当服务器数据返回以后，可以处理一些事情
安装： npm install --save axios
6.2 在项目当中，经常API文件夹【axios】
接口当中，路径都带有/api
 baseURL:"/api"
 6.3 axios可以参考npm｜git 关于axios文档

 7：接口统一管理
 项目很小：完全可以在组件的生命周期函数中发请求
 项目很大：封装进行统一管理

 7.1跨域问题
 什么是跨域：协议，域名，端口号不同的请求，称为跨域请求
 解决跨域的方法 ：JSONP CROS 代理
 现在用代理解决这个问题

 8:nprogress进度条的使用
 --安装插件
npm install --save nprogress -S
-S 表示添加到生产环境的依赖
start：进度条开始
done：进度条结束
进度条颜色可以修改的

9:Vuex状态管理库
9.1 是官方提供的一个插件：状态管理库，集中式管理项目中组件共用的数据
切记：并不是全部的项目都需要Vuex，如果项目很小，完全不需要Vuex，如果项目很大，组件很多，数据很多，数据维护很费劲，那么就用Vuex

Vuex几个核心
state
mutations
acitons
getters
modules
安装Vuex：npm install --save vuex@3.6.2 -S 
vue2中，要用vuex的3版本
vue3中，要用vuex的4版本
默认的npm i vuex是安装的最新版本4。要指定安装版本：npm i vuex@3
9.2 vuex基本使用

9.3 vuex实现模块式开发
如果项目过大，组件过多，接口也很多，数据也很多，可以让vuex实现模块式开发
模拟state存储数据
{
   home:{},
   search:{}
}

10:完成typeNav三级联动展示数据业务