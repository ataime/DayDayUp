
参考： [https://www.bilibili.com/video/BV1Wk4y137vG](https://www.bilibili.com/video/BV1Wk4y137vG)

安装Nodejs:
```shell

以下是安装Node.js 14.x和npm的步骤：

首先，您需要下载和安装NodeSource存储库的设置RPM。使用以下命令下载设置RPM文件：
curl -sL -o '/tmp/tmp.v4Ah0VfGIP' 'https://rpm.nodesource.com/pub_14.x/el/7/aarch64/nodesource-release-el7-1.noarch.rpm'

下载完成后，使用以下命令安装设置RPM：
rpm -i --nosignature --force '/tmp/tmp.v4Ah0VfGIP'

安装完成后，您可以运行以下命令来检查是否存在其他已安装的Node.js和npm版本：
rpm -qa 'node|npm' | grep -v nodesource

这将列出不属于NodeSource存储库的Node.js和npm软件包。

最后，您可以运行以下命令来安装Node.js 14.x和npm：
sudo yum install -y nodejs

如果yum不可用，您可以使用dnf来代替：
sudo dnf install -y nodejs

如果您需要构建本机插件，还需要安装开发工具：
sudo yum install -y gcc-c++ make

如果您还想安装Yarn软件包管理器，可以运行以下命令：
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
sudo yum install -y yarn

```

CentOS 安装最新的node出现下面的错误:
```shell
[root@i-roam80di src]# node -v
node: /lib64/libm.so.6: version `GLIBC_2.27' not found (required by node)
node: /lib64/libc.so.6: version `GLIBC_2.25' not found (required by node)
node: /lib64/libc.so.6: version `GLIBC_2.28' not found (required by node)
node: /lib64/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by node)


安装低版本node，不会有问题。
# nvm install v16.13.0
这种安装方法，每次新启动终端都需要手动执行 "source /etc/profile"。


# wget https://nodejs.org/dist/v16.13.0/node-v16.13.0-linux-x64.tar.xz
# tar xf node-v16.13.0-linux-x64.tar.xz 
# mv node-v16.13.0-linux-x64 /usr/local/node
编辑 /etc/profile:
export PARH=$PATH:/usr/local/node/bin



更换源
[root@i-roam80di src]# npm config get registry
https://registry.npmjs.org/
[root@i-roam80di src]# npm config set registry http://mirrors.cloud.tencent.com/npm/
[root@i-roam80di src]# npm config get registry
```




如果不能访问上面的网络,使用下面步骤
```shell
    
    1  pwd
    2  ll
    3  yum update -y
    4  yum install -y gcc
    5  cd  /usr/local/src/
    6  ll
    7  wget http://ftp.gnu.org/gnu/glibc/glibc-2.28.tar.gz
    8  yum install -y vim wget git 
    9  wget wget http://ftp.gnu.org/gnu/glibc/glibc-2.28.tar.gz
   10  wget https://nodejs.org/dist/v18.18.0/node-v18.18.0-linux-x64.tar.xz
   11  ll
   12  tar xf node-v18.18.0-linux-x64.tar.xz  
   13  ll
   14  cd node-v18.18.0-linux-x64
   15  ll
   16  cd bin/
   17  ll
   18  ./node -v
   19  cd ..
   20  ll
   21  mv node-v18.18.0-linux-x64 /usr/local/node
   22  vim /etc/profile
   23  source /etc/profile
   24  node -v
   25  ll
   26  tar zxvf glibc-2.28.tar.gz 
   27  cd glibc-2.28
   28  ll
   29  mkdir build
   30  cd build/
   31  ll
   32  ../configure  --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin --disable-sanity-checks --disable-werror
   33  cd /usr/local/src/
   34  ll
   35  yum install -y centos-release-scl
   36  yum install -y devtoolset-8-gcc*
   37  mv /usr/bin/gcc /usr/bin/gcc-4.8.5
   38  ln -s /opt/rh/devtoolset-8/root/bin/gcc /usr/bin/gcc
   39  mv /usr/bin/g++ /usr/bin/g++-4.8.5
   40  ln -s /opt/rh/devtoolset-8/root/bin/g++ /usr/bin/g++
   41  wget http://ftp.gnu.org/gnu/make/make-4.3.tar.gz
   42  tar -xzvf make-4.3.tar.gz && cd make-4.3/
   43  ./configure  --prefix=/usr/local/make
   44  make && make install
   45  cd /usr/bin/ && mv make make.bak
   46  ln -sv /usr/local/make/bin/make /usr/bin/make
   47  ll
   48  cd ..
   49  cd  /usr/local/src/
   50  ll
   51  cd glibc-2.28
   52  ll
   53  cd bits/
   54  cd ..
   55  ll
   56  cd build/
   57  ll
   58  make all
   59  yum whatprovides libstdc++.so.6
   60  yum update -y libstdc++.x86_64
   61  cd ..
   62  ll
   63  wget http://www.vuln.cn/wp-content/uploads/2019/08/libstdc.so_.6.0.26.zip
   64  unzip libstdc.so_.6.0.26.zip
   65  yum install  -y zip*
   66  unzip libstdc.so_.6.0.26.zip
   67  yum install -y unzip
   68  unzip libstdc.so_.6.0.26.zip
   69  cp libstdc++.so.6.0.26 /lib64/
   70  cd /lib64
   71  ll
   72  cp libstdc++.so.6 libstdc++.so.6.bak
   73  rm -f libstdc++.so.6
   74  ln -s libstdc++.so.6.0.26 libstdc++.so.6
   75  cd /usr/local/src/
   76  ll
   77  cd glibc-2.28
   78  ll
   79  cd build/
   80  ll
   81  ../configure --prefix=/usr --disable-profile --enable-addons --with-headers=/usr/include --with-binutils=/usr/bin
   82  bison -V
   83  yum install bison -y
   84  bison -V
   85  ../configure --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin
   86  make 
   87  make install 
   88  node -V
   89  node -v
   90  history
   91  ldd --version
```


CentOS7安装node:
```shell
# yum install gcc gcc-c++ -y
# cd /usr/local/src/
# yum install -y  wget vim
# wget https://nodejs.org/download/release/v10.24.1/node-v10.24.1-linux-x64.tar.gz
# tar zxvf node-v10.24.1-linux-x64.tar.gz
# ./node-v10.24.1-linux-x64/bin/node -v
# mv node-v10.24.1-linux-x64 /usr/local/node
# vim /etc/profile

export PATH=$PATH:/usr/local/node/bin
   
# source /etc/profile
# node -v
```

安装 cnpm,typescript:
```shell
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
$ cnpm -v

$ cnpm i -g typescript
$ tsc -v
```
typescript代码不能直接在浏览器运行，需要转化为js代码运行。"tsc index.ts" 即可生成"index.js"转化为js文件.<br />ts是js的超集，扩展功能。
```shell
[root@vm196 vue-mall]$ cat index.ts 
var uname: string = "小红";
var num: number = 1;

num++;
console.log(num)

interface UPerson {
    uname: string,
    uage: number,
    sayHi: () => string
}

var personObj: UPerson = {
    uname: "xiaoa",
    uage: 20,
    sayHi: (): string => { return "Hi" }
}

console.log(personObj.sayHi())

[root@vm196 vue-mall]$ tsc index.ts 
[root@vm196 vue-mall]$ node index.js 
2
Hi
```


```rust
<!DOCTYPE html>
<html>
    <head>
        <title>Vue 基础</title>
    </head>

    <body>
        <div id="app">
            {{ message }}
            <span>{{message}}</span>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
        <script>
            var app = new Vue({
                el:"#app",
                data:{
                    message:"你好。"
                }
            })
        </script>
    </body>
</html>
```

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2348733/1641634299508-9750fe30-0042-4366-b591-e25d8884d485.png#averageHue=%23bb9867&clientId=u89b77ff8-78cc-4&from=paste&height=633&id=u163d7521&originHeight=1266&originWidth=2262&originalType=binary&ratio=1&rotation=0&showTitle=false&size=454038&status=done&style=none&taskId=ufe9b63b0-4993-4925-afea-9323cbbf1dd&title=&width=1131)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2348733/1641634229721-76b23bb6-4802-47e8-a08c-2ad09669eb4a.png#averageHue=%23f5f5f5&clientId=u89b77ff8-78cc-4&from=paste&height=129&id=u0a039fe1&originHeight=258&originWidth=850&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27071&status=done&style=none&taskId=u4535b5b1-2d76-4cdd-b82c-0a77284bd53&title=&width=425)

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Vue 基础</title>
    </head>

    <body>
        <div id="app">
            {{ message }}
            <h2 v-text="school.name + 'KKKK'"></h2>   <!-- v-text 是vue指令 -->
            <h2>{{school.name}} {{school.mobile}} </h2>   <!-- 使用双括号 -->
            <ul>
                <li>{{campus[0]}}</li>
                <li>{{campus[1]}}</li>
                <li>{{campus[2]}}</li>
            </ul>
            <input type="button" value="v-on测试" v-on:click="doIt" />  <!-- 事件绑定 -->
            <input type="button" value="v-on测试" @click="doIt" /> <!-- 简写事件绑定 -->
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
        <script>
            var app = new Vue({
                el:"#app",
                methods:{
                    doIt:function(){
                        alert(this.message);    // 这里的 this 是Vue对象
                        console.log(this);
                    }
                },
                data:{
                    message:"你好啊",
                    school:{
                        name:"黑马",
                        mobile:"111",
                    },
                    campus:["北京","上海","广州"]
                }
            })
        </script>
    </body>
</html>

```

安装Vue
```shell
[root@vm196 opt]$ npm install -g vue@next
[root@vm196 opt]$ npm install -g @vue/cli



[root@i-roam80di ~]# vue create gin-vue

Vue CLI v5.0.8
? Please pick a preset: 
  Default ([Vue 3] babel, eslint) 
  Default ([Vue 2] babel, eslint) 
❯ Manually select features 

Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to proceed)
 ◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
 ◉ Router
 ◉ Vuex
 ◉ CSS Pre-processors
❯◉ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing



Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, TS, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 
❯ 3.x 
  2.x 


Vue CLI v5.0.8
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, Router, Vuex, CSS Pre-processors, Linter
? Choose a version of Vue.js that you want to start the project with 3.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Sass/SCSS (with dart-sass)
? Pick a linter / formatter config: Airbnb
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? No


[root@vm196 opt]$ ll
total 8
drwxr-xr-x.  6 root root  251 Sep 27 16:39 app
drwxr-xr-x. 15 root root  220 Sep 27 16:31 node_modules
-rw-r--r--.  1 root root 7313 Sep 27 16:31 package-lock.json

[root@vm196 opt]$ cd app/ && cnpm i
[root@vm196 app]$ npm run serve
```


```shell
[root@vm196 app]$ yarn add postcss-loader postcss-pxtorem -D
[root@vm196 app]$ yarn add autoprefixer@9.8.6 -D 
[root@vm196 app]$ cnpm i less --save-dev
[root@vm196 app]$ cnpm install less-loader@7.3.0 --save-dev
```

ESLint是代码规范，VSCode使用 eslint插件，规范代码。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1696844684968-d1b284a8-4c1e-4c8e-b7f7-fa1fe5d3d037.png#averageHue=%231f1e1e&clientId=uf9b6cb8e-23d8-4&from=paste&height=271&id=uc0a42ef4&originHeight=541&originWidth=1205&originalType=binary&ratio=2&rotation=0&showTitle=false&size=119016&status=done&style=none&taskId=u6c9fccde-1288-4d44-be2b-6d227861b8a&title=&width=602.5)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1696844721923-45e031c9-0568-4297-a51a-43d2495c2ca7.png#averageHue=%231e1d1d&clientId=uf9b6cb8e-23d8-4&from=paste&height=264&id=u4f22885f&originHeight=528&originWidth=969&originalType=binary&ratio=2&rotation=0&showTitle=false&size=107065&status=done&style=none&taskId=u0147a08f-de8c-4283-9319-5c18d26e4e7&title=&width=484.5)


安装Bootstrap；<br />[https://bootstrap-vue.org/docs](https://bootstrap-vue.org/docs)
```shell
[root@i-roam80di gin-vue]# npm install vue bootstrap bootstrap-vue

```
```shell
[root@i-roam80di gin-vue]# node -v
v18.18.0

使用nvm管理node版本:

#从官网下载安装
官网地址：https://github.com/nvm-sh/nvm/archive/refs/tags/v0.39.1.tar.gz

#将压缩包上传至服务器，如我当前位置/nvm

#新建服务器nvm地址
mkdir /root/.nvm

#将压缩包解压至/root/.nvm
tar -zxvf nvm-0.39.1.tar.gz --strip-components 1  -C /root/.nvm

#编辑文件
vim ~/.bashrc

#写入配置
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm

#刷新配置
source ~/.bashrc

#判断nvm是否安装
nvm -v

nvm ls-remote
nvm install v10.14.2
node -v

```


```shell
[root@i-roam80di ~]# npm install --save axios
[root@i-roam80di ~]# vue create demo
[root@i-roam80di demo]# vue add element

```

npm 创建项目
```shell
[root@vm197 work]$ npm init vue@latest
Need to install the following packages:
  create-vue@3.7.5
Ok to proceed? (y) y

Vue.js - The Progressive JavaScript Framework

✔ Project name: … wwsc
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit Testing? … No / Yes
✔ Add an End-to-End Testing Solution? › No
✔ Add ESLint for code quality? … No / Yes

Scaffolding project in /opt/work/wwsc...

Done. Now run:

  cd wwsc
  npm install
  npm run dev


启动后输出：
01:23:57 [vite] vite.config.js changed, restarting server...
01:23:57 [vite] server restarted.

  ➜  Local:   http://127.0.0.1:5173/
  ➜  Network: use --host to expose

不可以使用IP访问，需要修改"vite.config.js"文件，才能使用IP访问.
```

```shell
[root@vm197 wwsc]$ vim vite.config.js

export default defineConfig({
	// 添加：
  server: {
      host: '0.0.0.0'
  },
  
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})
~
```

element-plus 组件按需导入：
```shell
[root@vm197 wwsc]$ npm install element-plus --save
[root@vm197 wwsc]$ npm install -D unplugin-vue-components unplugin-auto-import


编辑 "vite.config.js"：
import { fileURLToPath, URL } from 'node:url'

import vue from '@vitejs/plugin-vue'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'
import { defineConfig } from 'vite'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    AutoImport({
      resolvers:[ElementPlusResolver()],
    }),
    Components({
      resolvers:[ElementPlusResolver()],
    }),
  ],
  server:{
    host: '0.0.0.0'
  },
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})


修改App.vue:
<script setup>
</script>

<template>
  <header>
    <el-button  type="primary"> 按钮 </el-button>
  </header>
</template>

<style scoped>
</style>


```
[root@vm197 wwsc]$ npm run dev<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697017593444-a677ecc9-8bfa-481d-8cc1-543401299693.png#averageHue=%23f2f2f2&clientId=u6470f622-8e99-4&from=paste&height=81&id=ueec8e805&originHeight=161&originWidth=453&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15561&status=done&style=none&taskId=u40bde69c-175e-4e5f-904f-a14cc420c7a&title=&width=226.5)

```shell
Sass（Syntactically Awesome Style Sheets）是一种 CSS 预处理器，
它扩展了 CSS 的功能并增加了许多有用的特性。Sass 提供了变量、嵌套规则、Mixin、函数、继承等功能，
使得 CSS 更易于维护和扩展。
安装sass:
[root@vm197 wwsc]$ npm i sass -D 
```
修改 "vite.config.js"文件:
```shell
import { fileURLToPath, URL } from 'node:url'

import vue from '@vitejs/plugin-vue'
import AutoImport from 'unplugin-auto-import/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'
import Components from 'unplugin-vue-components/vite'
import { defineConfig } from 'vite'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    AutoImport({
      resolvers:[ElementPlusResolver()],
    }),
    Components({
      resolvers:[ElementPlusResolver({importStyle:"sass"})],
    }),
  ],
  server:{
    host: '0.0.0.0'
  },
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },
  css:{
    preprocessorOptions:{
      scss:{
        additionalData:`
        @use "@/styles/element/index.scss" as *;
        `
      }
    }
  }
})

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697037256211-07269f05-895c-4d9c-b238-2847026063a1.png#averageHue=%23ebf2f1&clientId=u6ce25337-6615-4&from=paste&height=112&id=ub23ec3a5&originHeight=224&originWidth=778&originalType=binary&ratio=2&rotation=0&showTitle=false&size=18082&status=done&style=none&taskId=uc7fd9c52-b2f3-42e3-9abf-dce187574c4&title=&width=389)<br />安装 axios:
```shell
[root@vm197 wwsc]$ npm i axios
[root@vm197 vue-wwsc]$ npm i @vueuse/core
```


```shell
utils/http.js中使用axios:

import axios from "axios";
const http = axios.create({
    baseURL:'https://dog.ceo',
    timeout:5000
})

// axios 请求拦截器
http.interceptors.request.use(config => {
    return config
},e=>Promise.reject(e))

// axios 响应拦截器
http.interceptors.response.use(res => res.data,e=>{
    return Promise.reject(e)
})

export default http

----------------------------------------
apis/testApi.js中定义方法
import http from "../utils/http";

export function getCategoryAPI(){
    return http.get("/api/breeds/image/random")
}

----------------------------------------
main.js中调用函数:
import { getCategoryAPI } from './apis/testApi'
getCategoryAPI().then(res => {
    console.log(res)
})

```

![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697037872397-ea57fd1d-b9ba-4c66-a135-a69bf11636d5.png#averageHue=%23fcfafa&clientId=u6ce25337-6615-4&from=paste&height=428&id=u9c7e1156&originHeight=856&originWidth=1712&originalType=binary&ratio=2&rotation=0&showTitle=false&size=181839&status=done&style=none&taskId=u7ab495cb-716c-4e9d-ba09-d5aa4dd1417&title=&width=856)<br />项目地址：[https://github.com/ataime/vue-wwsc.git](https://github.com/ataime/vue-wwsc.git)



语法解析：
```shell
ref 是 Vue 3 中的一个函数，用于创建一个响应式的数据引用。它接收一个初始值作为参数，并返回一个响应式的引用对象。
使用 ref 可以将普通的 JavaScript 值转换为响应式的引用，这样当引用的值发生变化时，相关的界面会自动更新。


import { ref } from 'vue'
const count = ref(0)
console.log(count.value) // 输出: 0
count.value++ // 修改引用的值
console.log(count.value) // 输出: 1


<script setup> 是 Vue 3 中的一个新特性，它可以让你更轻松地编写单文件组件。它是一个语法糖，可以自动为你的组件生成一个包含响应式数据、计算属性和方法的对象。
<template>
  <div>{{ count }}</div>
  <button @click="increment">Increment</button>
</template>

<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>
在模板中，我们可以直接使用 count 和 increment，而不需要在选项中定义它们。
使用 <script setup> 可以让你的代码更简洁、更易读，同时也可以提高性能。

```

```shell
defineProps 是 Vue 3 中的一个函数，用于定义组件的 props 属性。

import { defineProps } from 'vue'

export default {
  props: defineProps({
    name: {
      type: String,
      required: true
    },
    age: {
      type: Number,
      default: 18
    }
  }),
  mounted() {
    console.log(this.name) // 输出 prop name 的值
    console.log(this.age) // 输出 prop age 的值
  }
}
需要注意的是，在 Vue 3 中，props 是只读的，不能在组件内部直接修改它们的值。如果需要在组件内部修改 prop 的值，可以使用 defineEmits 和 emit 来实现父子组件之间的通信。

```
```shell
export default 是 JavaScript 中的一个语法，用于导出一个模块的默认值。

在 Vue 3 中，可以使用 export default 导出一个组件、一个函数或一个对象作为模块的默认值。这样在其他地方引入该模块时，可以直接使用默认值，而不需要指定具体的导出名称。

下面是一个使用 export default 导出组件的示例：

// MyComponent.vue
<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hello, Vue!'
    }
  }
}
</script>

在上面的示例中，我们使用 export default 导出了一个名为 MyComponent 的组件。其他地方可以直接引入该组件，并使用它。

// App.vue
<template>
  <div>
    <my-component></my-component>
  </div>
</template>

<script>
import MyComponent from './MyComponent.vue'

export default {
  components: {
    MyComponent
  }
}
</script>

在上面的示例中，我们在 App.vue 中引入了 MyComponent 组件，并在 components 选项中注册它。
```


Vue 组合式API:
```shell
<script setup>
import { onMounted, ref } from "vue";
const count = ref(0);
function increment() {
  count.value++;
}
onMounted(() => {
  console.log("++++++++++");
});
</script>

<template>
  <button @click="increment">{{ count }}</button>
</template>
```

Vue 选项式API:
```shell
<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    increment() {
      this.count++;
    },
  },
  mounted() {
    console.log("+++++++++");
  },
};
</script>

<template>
  <button @click="increment">{{ count }}</button>
</template>

```
```shell
在属性里使用v-bind才能使用变量，在标签里使用 {{}} 访问变量。

<template>
  <div v-bind:id="vid" v-bind:title="vtitle">测试{{ vid }}</div>
</template>

简写:
<template>
  <div :id="vid" :title="vtitle">测试{{ vid }}</div>
</template>

```


打开Vue-UI工具:
```shell
[root@vm197 ~]$ vue ui
🚀  Starting GUI...
🌠  Ready on http://localhost:8000
```


###### defineProps()
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697596565316-8a6ea195-51ca-4b08-9bec-e6ee241eef47.png#averageHue=%23fbfafa&clientId=udcb14ab1-3bc9-4&from=paste&height=744&id=u49a8b34d&originHeight=1488&originWidth=2414&originalType=binary&ratio=2&rotation=0&showTitle=false&size=355826&status=done&style=none&taskId=ua7e09b79-320b-4438-a51c-6d690aa5ef8&title=&width=1207)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697596586068-4c24fe3c-0c47-4680-9185-5f1ab1f668f0.png#averageHue=%23fbfbfb&clientId=udcb14ab1-3bc9-4&from=paste&height=704&id=u379c07f7&originHeight=1408&originWidth=2328&originalType=binary&ratio=2&rotation=0&showTitle=false&size=312184&status=done&style=none&taskId=u92bcce3f-79f3-4b19-950a-6c3e0691480&title=&width=1164)


###### Emits
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697596784641-f190209a-1633-48c6-b376-60fe81a470c7.png#averageHue=%23fbfafa&clientId=udcb14ab1-3bc9-4&from=paste&height=676&id=uae52b5c5&originHeight=1352&originWidth=2380&originalType=binary&ratio=2&rotation=0&showTitle=false&size=356700&status=done&style=none&taskId=u72a851a9-2b02-4940-8344-b82f6410d3a&title=&width=1190)

![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697596818143-aae97d98-3145-48f0-8ebf-3b6d0bb86422.png#averageHue=%23fafafa&clientId=udcb14ab1-3bc9-4&from=paste&height=613&id=u3b9b7e15&originHeight=1226&originWidth=2334&originalType=binary&ratio=2&rotation=0&showTitle=false&size=302118&status=done&style=none&taskId=ud1311234-c21e-4ec8-8a56-41839b66622&title=&width=1167)



![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697597411608-e56d086a-08f2-4913-a1e2-6c7c32e053f6.png#averageHue=%23fcfbfb&clientId=udcb14ab1-3bc9-4&from=paste&height=754&id=uaf0aa9aa&originHeight=1508&originWidth=2084&originalType=binary&ratio=2&rotation=0&showTitle=false&size=355057&status=done&style=none&taskId=u0763dd61-ae67-4e71-866a-5f22b109588&title=&width=1042)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697597423048-f571fa57-6a30-4399-912c-db0d6e493b7d.png#averageHue=%23d28766&clientId=udcb14ab1-3bc9-4&from=paste&height=605&id=ue89adf2e&originHeight=1210&originWidth=1956&originalType=binary&ratio=2&rotation=0&showTitle=false&size=231412&status=done&style=none&taskId=ue9b09b66-baf5-492c-b639-aeb35074ff1&title=&width=978)


![image.png](https://cdn.nlark.com/yuque/0/2023/png/2348733/1697598332869-b9f98a93-fb2c-4fb9-8ab7-040b0305f513.png#averageHue=%23fbfafa&clientId=udcb14ab1-3bc9-4&from=paste&height=782&id=ub86004a7&originHeight=1564&originWidth=2686&originalType=binary&ratio=2&rotation=0&showTitle=false&size=468867&status=done&style=none&taskId=u8b62e875-3335-47d5-9edb-b350f285f88&title=&width=1343)



## VUE 项目部署
```shell
nvm use 16 ,  切换node版本，node > 16 在 centos7 上报错，node vue 等不能使用。

vue create aaa , 创建项目aaa.
cd aaa && npm run serve , 运行项目.

npm run build 或 yarn build。这会生成一个dist目录。
dist目录中的文件上传到你的Web服务器。
对于Nginx：配置一个服务，指向你的dist目录。确保所有请求都转发到index.html。
```














 
