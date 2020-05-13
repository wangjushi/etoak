易途网站教程文档
===

# 目录

* [目录结构](#目录结构)
* [主要使用组件](#主要使用组件)
	* [vuetify](#vuetify)
		* [Grids(栅格)](#Grids栅格)
		* [Sheets(延展纸)](#Sheets延展纸)
		* [Parallax(视差)](#Parallax视差)
		* [Hover(悬停)](#Hover悬停)
		* [Data iterators(数据迭代器)](#Data-iterators数据迭代器)
	* [echarts](#echarts)
	* [axios](#axios)
	* [vuex](#vuex)
	* [router](#router)
	* [vuescroll](#vuescroll)
	* [vue-video-player](#vue-video-player)
	* [vue-photo-preview](#vue-photo-preview)
* [环境准备](#环境准备)
	* [nodejs安装](#nodejs安装)
	* [IntelliJ IDEA安装](#intellij-idea安装)
* [无环境启动](#无环境启动)
* [编译安装](#编译安装)

## 目录结构
``` bash
|------------build          构建脚本目录

    |---------build.js             生产环境构建脚本

    |---------check-version.js 检查node、npm等版本

    |---------utils.js               构建相关工具方法

    |---------vebpack.base.conf.js     webpack基本配置

    |---------vebpack.dev.conf.js       webpack开发环境配置

    |---------vebpack.prod.conf.js     webpack生产环境配置

|------------config           项目配置

    |---------dev.env.js           开发环境变量

    |---------index.js              项目配置文件

    |---------prod.env.js         生产环境变量

|------------node_modules         node的依赖包

|------------src

    |---------api                 请求相关封装

        |------modules          各模块请求文件

        |------http.js            axios封装

        |------api.js             请求路径统一管理

    |---------assets                 资源目录，这里的资源会被webpack构建

    |---------components        		组件目录

    |---------plugins             外部插件

        |-----------vuetify.js      前端插件

        |-----------et_icon_font     自定义图标字体库

    |---------router

        |-----------index.js               前端路由

    |---------store                   内存包放各种公共资源以及静态资源

            |-----------i18n        国际化文件夹

            |-----------index.js      vuex组件

    |---------page					页面文件

    |--------Etoak.vue               易途专用根组件

    |--------main.js                 入口js文件

|------------static             纯静态资源，不会被webpack构建

|------------index.html         入口页面

|------------.babelrc            ES6语法编译配置

|-----------.editorconfig      	定义代码格式

|-----------.gitignore         	git 上传需要忽略的文件

|-----------package.json       项目基本信息
```
## 主要使用技术
当前工程使用的是vue2.5.2版本使用了很多组件和部分样式<br>
### vuetify
`vuetify` 是 Vue.js 的头号组件库，自 2016 年以来一直在积极开发。该项目的目标是为用户提供使用 Material Design specification 构建丰富且引人入胜的 web 应用程序所需的一切。它通过一致的更新周期、对以前版本的长期支持 (LTS)、响应式社区参与、丰富的资源生态系统和对高质量组件的贡献来实现这一点。<br>
#### Grids(栅格)
Vuetify 附带了一个使用 flex-box 构建的 12 点栅格系统。 网格用于在应用程序的内容中创建特定布局。其中包含 5 种媒体断点，分别用于定位特定屏幕大小或方向：xs, sm, md, lg 和 xl。 这些分辨率在下面的视口断点表中定义，可以通过自定义 Breakpoint service 进行修改。<br>
系统中大量使用了栅格进行系统的排本以适应多端系统如下代码片段:<br>
``` html
<v-col class="pa-4" cols="12" md="5">
	<v-sheet color="grey darken-3 pa-5">
	  <v-row>
		<v-col cols="12" style="height: 204px;">
		  <et-charts :option="flotDashboardChart"></et-charts>
		</v-col>
	  </v-row>
	  <v-row>
		<v-col cols="12" md="6">
		  <span class="title d-flex justify-center">￥6321</span>
		  <span class="subtitle-2 d-flex justify-center">业内平均薪资</span>
		</v-col>
		<v-col cols="12" md="6">
		  <span class="title d-flex justify-center">￥12481</span>
		  <span class="subtitle-2 d-flex justify-center">易途外包薪资</span>
		</v-col>
	  </v-row>
	</v-sheet>
</v-col>
```
```
v-row 代表行分割
v-col 代表列分割
一行可以分割为12列 可以进行嵌套分割
```
效果如下:<br>
![xg1](./img/xg1.jpg)<br>
#### Sheets(延展纸)
v-sheet 旨在为 Vuetify 中的其他 paper 组件提供支持。 它旨在用作低级组件。<br>
``` html
<v-sheet color="grey darken-3 pa-5">
  <h1 class="title">最新合作项目</h1>
  <p class="subtitle-2 font-weight-light">包括外包技术服务和独立研发项目:</p>
  <div class="adminpro-message-list">
	<ul class="message-list-menu">
	  <li v-for="item in desserts"><span :class="dessertsClass(item.num)">{{item.num}}</span> <span class="message-info">{{item.message}}</span>
		<span class="message-time">{{item.time}}</span>
	  </li>
	</ul>
  </div>
</v-sheet>
```
效果如下:<br>
![xg2](./img/xg2.jpg)<br>
#### Parallax(视差)
v-parallax 组件创建一个 3d 效果使图像显示比窗口滚动更慢。<br>
``` html
<section id="stats">
  <!-- src="https://images.unsplash.com/photo-1510915228340-29c85a43dcfe?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80" -->
  <v-parallax :height="$vuetify.breakpoint.smAndDown ? 700 : 500" src="https://images.unsplash.com/photo-1510915228340-29c85a43dcfe?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80">
	<v-container fill-height>
	  <v-row class="mx-auto">
		<v-col v-for="[value, title] of stats" :key="title" cols="12" md="3">
		  <div class="text-center">
			<div class="display-3 font-weight-black mb-4" v-text="value"></div>
			<div class="title font-weight-regular text-uppercase" v-text="title"></div>
		  </div>
		</v-col>
	  </v-row>
	</v-container>
  </v-parallax>
</section>
```
效果请看`关于我们`页面
#### Hover(悬停)
v-hover 组件为任何组件处理悬停状态提供了一个干净的接口。
``` vue
<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <v-responsive class="overflow-y-auto" :max-height="$store.state.maxHeight">
  <v-container>
    <v-row class="fill-height" align="center" justify="center">
      <template v-for="(item, i) in items">
        <v-col
          :key="i"
          cols="12"
          md="6"
          sm="12"
          dark
        >
          <v-hover v-slot:default="{ hover }" dark>
            <v-card
              class="mx-auto"
              max-width="600"
              style="width:90vw;"
              dark
            >
              <v-img
                :aspect-ratio="12/8"
                :contain="true"
                :src="item.img"
              >
                <v-expand-transition>
                  <div
                    v-if="hover && !$vuetify.breakpoint.xs"
                    class="d-flex transition-fast-in-fast-out orange darken-2 v-card--reveal display-3 white--text"
                    style="height: 100%;"
                  >
                    {{ item.category.replace("—","") }}
                  </div>
                  <div
                    v-if="hover && $vuetify.breakpoint.xs"
                    class="d-flex transition-fast-in-fast-out orange darken-2 v-card--reveal display-3 white--text"
                    style="height: 100%;font-size:2em !important;"
                  >
                    {{ item.category.replace("—","") }}
                  </div>
                </v-expand-transition>
              </v-img>
              <v-card-text
                class="pt-6"
                style="position: relative;padding-left:0px;padding-right:0px;"
              >
                <v-btn
                  absolute
                  color="orange"
                  class="white--text"
                  fab
                  large
                  right
                  top
                >
                  <v-icon>mdi-import</v-icon>
                </v-btn>
                <div class="font-weight-light grey--text title mb-2">{{ item.name }}</div>
                <h3 class="display-1 font-weight-light orange--text mb-2">{{ item.category }}</h3>
                <div class="font-weight-light title mb-2">
                  {{ item.desc }}
                </div>
                <v-bottom-navigation
                >
                  <v-btn
                    v-for="n in 6"
                    :key="n"
                    min-width="5vw"
                    style="padding-right:0px;padding-left:0px;"
                    >
                    <span>{{ item.compose[n-1] }}</span>
                    <v-icon  color="red">{{ item.icons[n-1] }}</v-icon>
                  </v-btn>
                </v-bottom-navigation>
              </v-card-text>
            </v-card>
          </v-hover>
        </v-col>
      </template>
    </v-row>
    <v-divider></v-divider>

  </v-container>
</v-responsive>
</template>
<style>
  .v-card--reveal {
    align-items: center;
    bottom: 0;
    justify-content: center;
    opacity: .5;
    position: absolute;
    width: 100%;
  }
</style>
<script>
  export default {
    data () {
      return {
        clientWidth:document.documentElement.clientWidth,
        items: [
          {
            name: '汪老师',
            category: "—易途COREJAVA讲师",
            desc: '人气颇高的美女讲师，授课严谨细致、脉络清晰，讲解声情并茂，善于拓展延伸，亲和力强，对待教学认真负责，要求严格，循循善诱，平易近人，不厌其烦，细心讲解，经验丰富，深入浅出，逻辑性强，善于总结归纳重点和难点。负责Java核心技术的教学，是无数易途学员的启蒙老师。',
            img: '../../../static/teacher/wl.png',
            compose:['JVM构成','核心语法','数据类型','运算符','面向对象','设计模式'],
            icons: ['mdi-home-search-outline','mdi-tag-heart','mdi-format-list-bulleted-type','mdi-plus','mdi-account-supervisor','mdi-grease-pencil'],
          },
          {
            name: '薄老师',
            category: '—易途数据库讲师',
            desc: '四年开发经验，曾在胜利油田项目中负责数据库迁移，并在中国移动旗下咪咕阅读参与数据库方案设计，数据实时推送，还在建筑，金融，电商，智能警务等多个行业积累了Oracle丰富的实战经验，并将整个课程都与现实工作紧密结合起来，负责Oracle数据库教学。',
            img: '../../../static/teacher/bqp.png',
            compose:['Oracle','MySQL','XML','JDBC','DBCP','连接池实现'],
            icons: ['mdi-moon-new','mdi-size-m','mdi-close-thick','mdi-lan-connect','mdi-database-import','mdi-database'],
          },
          {
            name: '张老师',
            category: '—J2EE核心技术讲师',
            desc: '六年开发经验，精通JQUERY/AJAX/XHTML等WEB前端技术，精通ICBCCTP等大型框架，曾任职上海工商银行科技部技术总监，后转向JAVA教学，兼任多家网络技术公司研发顾问。授课有着迷人的魅力，在讲解知识中，总会有出其不意的精彩亮点，深受广大学员的喜爱。 负责J2EE核心技术的教学',
            img: '../../../static/teacher/zwc.png',
            compose:['Servlet','JSP','HTML','Javascript','AJAX','JQuery'],
            icons: ['mdi-alpha-s-circle','mdi-alpha-j','mdi-language-html5','mdi-language-javascript','mdi-elevator-up','mdi-jquery'],
          },
          {
            name: '周老师',
            category: '—易途持久层框架讲师',
            desc: '八年开发经验，五年教学经验，精通UNIX/LINUX，擅长持久层深挖掘，华东地区著名MYBITIS课程专家，曾任多个企业项目组技术总监，后于2010年专注于JAVA教学。专业功底深厚，讲解精辟透彻，善于启迪学生思路，剖析底层框架架构，思路非常清晰。负责持久层框架以及表现层框架技术的教学',
            img: '../../../static/teacher/zk.png',
            compose:['Hibernate','MyBatis','IBatis','Struts','持久层缓存','框架原理'],
            icons: ['mdi-hulu','mdi-size-m','mdi-alpha-i','mdi-numeric-5-circle-outline','mdi-content-duplicate','mdi-electron-framework'],
          },
          {
            name: '卢老师',
            category: '—易途Spring框架讲师',
            desc: '企业级培训专家，曾任职中国联通系统集成分公司，负责内部商城的开发和维护工作。精通系统中设计建模，部署运行，监管和分析管理，精通Spring框架底层逻辑，精通SpringBoot、SpringCloud微服务和分布式平台技术。',
            img: '../../../static/teacher/lxl.png',
            compose:['Spring MVC','Spring','Web Service','Quartz','项目整合','微服务'],
            icons: ['mdi-code-string','mdi-size-s','mdi-recycle-variant','mdi-clock-in','mdi-arrange-bring-forward','mdi-weather-cloudy'],
          },
        ],
        length: 3,
        window: 0,
        showArrows: false,
        vertical: false,
        reverse: false,
        autorun: false,
      }
    },
    created () {
      
      setInterval(() => {
        if (!this.autorun) return
        if (++this.window >= this.length) this.window = 0
      }, 2000)
    },
  }
</script>
```
效果如下:<br>
![xg4](./img/xg4.jpg)<br>
![xg3](./img/xg3.jpg)<br>
#### Data iterators(数据迭代器)
v-data-iterator 组件用于显示数据，并将其大部分功能与 v-data-table 组件共享。功能包括排序、搜索、分页和选择。<br>
``` vue
<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <v-responsive class="overflow-y-auto" :max-height="$store.state.maxHeight">
  <v-container fluid>
    <div class="display-1 mb-2 white--text">易途高薪就业案例</div>
    <v-chip
      class="ma-2"
      label
      text-color="white"
      dark
      style="height:auto"
    >
    
      <v-icon left>mdi-twitter</v-icon>
      <div style="white-space: pre-wrap;">
      近年来易途高薪就业的案例层出不穷，我们仅以人员固定编号的形式来陈述这个事实
      </div>
    </v-chip>
    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      :page="page"
      :search="search"
      :sort-by="sortBy.toLowerCase()"
      :sort-desc="sortDesc"
      hide-default-footer
      dark
    >
      <template v-slot:header dark>
        <v-toolbar
          dark
          class="mb-1"
        >
          <v-text-field
            v-model="search"
            clearable
            flat
            solo-inverted
            hide-details
            label="查询"
          ></v-text-field>
          <template v-if="$vuetify.breakpoint.mdAndUp">
            <v-spacer></v-spacer>
            <v-select
              v-model="sortBy"
              flat
              solo-inverted
              hide-details
              :items="keys"
              label="排序"
            ></v-select>
            <v-spacer></v-spacer>
            <v-btn-toggle
              v-model="sortDesc"
              mandatory
            >
              <v-btn
                large
                depressed
                :value="false"
              >
                <v-icon>mdi-arrow-up</v-icon>
              </v-btn>
              <v-btn
                large
                depressed
                :value="true"
              >
                <v-icon>mdi-arrow-down</v-icon>
              </v-btn>
            </v-btn-toggle>
          </template>
        </v-toolbar>
      </template>

      <template v-slot:default="props">
        <v-row>
          <v-col
            v-for="item in props.items"
            :key="item.name"
            cols="12"
            sm="6"
            md="4"
            lg="3"
          >
            <v-card>
              <v-card-title class="subheading font-weight-bold"></v-card-title>

              <v-divider></v-divider>

              <v-list dense>
                <v-list-item
                  v-for="(key, index) in filteredKeys"
                  :key="index"
                >
                  <v-col cols="2"><v-icon v-if="index==1" class="pr-1">mdi-heart-outline</v-icon>
                  <span v-else>&emsp;&nbsp;&nbsp;</span></v-col>
                  <v-list-item-content :class="{ 'blue--text': sortBy === key }">{{ key }}:</v-list-item-content>
                  <v-list-item-content class="align-end" :class="{ 'blue--text': sortBy === key }">{{ item[key.toLowerCase()] }}</v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>

      <template v-slot:footer>
        <v-row class="mt-2" align="center" justify="center">
          <span class="white--text">每页显示条数</span>
          <v-menu offset-y>
            <template v-slot:activator="{ on }">
              <v-btn
                text
                class="ml-2"
                v-on="on"
              >
                {{ itemsPerPage }}
                <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(number, index) in itemsPerPageArray"
                :key="index"
                @click="updateItemsPerPage(number)"
              >
                <v-list-item-title dark>{{ number }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>

          <v-spacer></v-spacer>

          <span
            class="mr-4 white--text"
          >
            第 {{ page }} 页到 {{ numberOfPages }}
          </span>
          <v-btn
            fab
            class="mr-1"
            @click="formerPage"
            style="margin-left:15%;"
          >
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn
            fab
            class="ml-1"
            @click="nextPage"
          >
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</v-responsive>
</template>
<style></style>
<script>

  import data from '@/common/data.js';

  export default {
    data () {
      return {
        itemsPerPageArray: [8, 12 , 16],
        search: '',
        filter: {},
        sortDesc: false,
        page: 1,
        itemsPerPage: 8,
        sortBy: 'name',
        keys: [
          '编号',
          '姓名',
          '薪资',
          '所在城市',
          '企业名称',
        ],
        items: data,
      }
    },
    computed: {
      numberOfPages () {
        return Math.ceil(this.items.length / this.itemsPerPage)
      },
      filteredKeys () {
        return this.keys.filter(key => key !== `Name`)
      },
    },
    mounted(){
      
    },
    methods: {
      nextPage () {
        if (this.page + 1 <= this.numberOfPages) this.page += 1
      },
      formerPage () {
        if (this.page - 1 >= 1) this.page -= 1
      },
      updateItemsPerPage (number) {
        this.itemsPerPage = number
      },
    },
  }
</script>
```
效果如下:
![xg5](./img/xg5.png)<br>
### echarts
`echarts` 一个使用 JavaScript 实现的开源可视化库，可以流畅的运行在 PC 和移动设备上，兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等），底层依赖矢量图形库 ZRender，提供直观，交互丰富，可高度个性化定制的数据可视化图表。<br>
在et/src/components/charts目录下有封装好的Echarts组件 代码如下:
``` vue
<template>
  <div v-resize="onResize" :ref="id" style="height: 100%;"></div>
</template>

<script>
import echarts from 'echarts'
  export default {
    name: "et-charts",
    computed: {
      options() {
        return this.option
      },
    },
    props: {
      option: Object
    },
    data() {
      return {
        id:new Date().getTime(),
        charts:{}
      }
    },
    methods:{
      onResize(){
        if(this.charts.resize)
        this.charts.resize();
      }
    },
    mounted() {
      setTimeout(()=>{
        this.charts = echarts.init(this.$refs[this.id])
        this.charts.setOption(this.options)
      },200)
    },
    watch: {
      options() {
        this.charts.setOption(this.options)
      }
    }
  }
</script>

<style>
</style>
```
使用:
``` vue
<et-charts :option="flotDashboardChart"></et-charts>
methods:{
	flotDashboardChart() {
		return {
		  color: ["#03a9f4", "#0055ff"],
		  tooltip: {
			trigger: 'none',
			axisPointer: {
			  type: 'cross'
			},
			show: true
		  },
		  grid: {
			top: "0px",
			left: "0px",
			right: "0px",
			bottom: "0px"
		  },
		  xAxis: [{
			show: false,
			data: [5000,5500,6000,6500,7000,7500,8000,8500,9000,9500,10000,10500,11000,11500,12000,12500,13000]
		  }],
		  yAxis: [{
			type: 'value',
			show: false
		  }],
		  series: [{
			  type: 'line',
			  smooth: true,
			  areaStyle: {},
			  symbol: 'none',
			  data: [6000,5500,6000,6500,6000,5500,7000,7500,6000,6500,6000,6500,6500,6000,5500,6500,7000]
		  },
			{
			  type: 'line',
			  smooth: true,
			  areaStyle: {},
			  symbol: 'none',
			  data: [11500,12000,11000,12500,13000,11500,10500,11000,13000,12000,12000,10500,11000,11500,12000,12500,11500]
			}
		  ]
		}
	},
}
```
### axios
`axios` Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。<br>
对axios 进行封装:
``` js
// 在http.js中引入axios
import axios from 'axios'; // 引入axios
import routerIndex from '@/router/index'
import errorCode from "@/store/errorCode";
import store from "@/store/index";
import dialog from '@/components/dialog/index'

// 环境的切换
if (process.env.NODE_ENV == 'development') {
  axios.defaults.baseURL = 'http://127.0.0.1:8080';
} else if (process.env.NODE_ENV == 'test') {
  axios.defaults.baseURL = '';
} else if (process.env.NODE_ENV == 'production') {
  axios.defaults.baseURL = 'http://127.0.0.1:8080';
}

//设置超时时间
axios.defaults.timeout = 10000;
//设置请求头
axios.defaults.headers.post['Content-Type'] = 'application/json;charset=UTF-8';

// 请求拦截器
axios.interceptors.request.use(
  config => {
    // 每次发送请求之前判断是否存在token，如果存在，则统一在http请求的header都加上token，不用每次请求都手动添加了
    // 即使本地存在token，也有可能token是过期的，所以在响应拦截器中要对返回状态进行判断
    const token = store.state.token;
    token && (config.headers.Authorization = "Bearer "+token);
    return config;
  },
  error => {
    return Promise.error(error);
  })

// 响应拦截器
axios.interceptors.response.use(
  // 请求成功
  response => {
    const data = response.data;
    if(data.flag){ //成功

    }else{
      if((data.code >= 3000 && data.code <= 3099) && data.msg){
        dialog.alert(data.msg,'错误');
      }
    }
    return data;
  },
  // 请求失败
  error => {
    const { response } = error;
    if (response) {
      switch(response.status){
        case 401:
          routerIndex.push('/login');
          break;
        case 403:
          console.log("这是403");
          break;
        case 404:
          console.log("这是404");
          break;
        case 500:
          console.log("这是500");
          break;
        default:
          console.error("请求"+response.status);
      }
      return Promise.reject(response);
    } else {
      // 处理断网的情况
      if (!window.navigator.onLine) {
        //断网的情况 路由跳转到断网的页面
      }else{
        dialog.alert("服务器没开",'错误');
      }
      return Promise.reject(error);
    }
  });

export default axios;
```
### vuex
`vuex` Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。<br>
封装如下:
``` js
import Vue from 'vue';
import Vuex from 'vuex';
Vue.use(Vuex);
const store = new Vuex.Store({
  state: {
    token: localStorage.getItem('token') || '',
    i18nLocale: 'zhHans',
    userInfo: {},
    //菜单条状态
    drawer: false,
    maxHeight:500,
    menuItems: [{
      "id": "006",
      "permissionOrder": 7,
      "icon": "mdi-book-open-page-variant",
      "iconType": "0",
      "name": "培训业务",
      "href": "",
      "code": "peixun",
      "active": "true",
      "items": [{
        "id": "006001",
        "permissionOrder": 0,
        "icon": "mdi-teach",
        "iconType": "0",
        "name": "师资团队",
        "href": "/team",
        "code": "teacher",
        "items": null
      }, {
        "id": "006002",
        "permissionOrder": 1,
        "icon": "mdi-language-java",
        "iconType": "0",
        "name": "课程计划",
        "href": "/course",
        "code": "course",
        "items": null
      }, {
        "id": "006003",
        "permissionOrder": 2,
        "icon": "mdi-podium-gold",
        "iconType": "0",
        "name": "就业金榜",
        "href": "/work",
        "code": "gold",
        "items": null
      }]
    }, {
      "id": "007",
      "permissionOrder": 8,
      "icon": "mdi-contacts-outline",
      "iconType": "0",
      "name": "外包服务",
      "href": "",
      "code": "waibao",
      "items": [{
          "id": "007001",
          "permissionOrder": 1,
          "icon": "mdi-electron-framework",
          "iconType": "0",
          "name": "业务简介",
          "href": "/businessProfile",
          "code": "businessProfile"
        },
        {
          "id": "007002",
          "permissionOrder": 2,
          "icon": "mdi-briefcase-search-outline",
          "iconType": "0",
          "name": "服务案例",
          "href": "/serviceCase",
          "code": "serviceCase"
        },
      ]
    }, {
      "id": "008",
      "permissionOrder": 9,
      "icon": "mdi-bug-check",
      "iconType": "0",
      "name": "研发业务",
      "href": "",
      "code": "yanfa",
      "items": [{
        "id": "008001",
        "permissionOrder": 0,
        "icon": "mdi-television-guide",
        "iconType": "0",
        "name": "服务案例",
        "href": "/research",
        "code": "project",
        "items": null
      }]
    }, {
      "id": "009",
      "permissionOrder": 11,
      "icon": "mdi-alpha-e-circle",
      "iconType": "0",
      "name": "关于我们",
      "href": "/about",
      "code": "about",
      "items": []
    }, {
      "id": "010",
      "permissionOrder": 10,
      "icon": "mdi-camera-wireless",
      "iconType": "0",
      "name": "易途情节",
      "href": "",
      "code": "et",
      "items": [{
        "id": "010001",
        "permissionOrder": 0,
        "icon": "mdi-camera",
        "iconType": "0",
        "name": "精彩时刻 ",
        "href": "/plot",
        "code": "plot",
        "items": null
      }, {
        "id": "010002",
        "permissionOrder": 1,
        "icon": "mdi-video",
        "iconType": "0",
        "name": "精彩回忆",
        "href": "/video",
        "code": "video",
        "items": null
      }]
    }, {
      "id": "011",
      "permissionOrder": 12,
      "icon": "mdi-card-account-phone",
      "iconType": "0",
      "name": "联系我们",
      "href": "/contact",
      "code": "lianxiwomen",
      "items": []
    }],
  },
  mutations: {
    set_token(state, token) {
      state.token = token
      localStorage.setItem('token', token)
    },
    del_token(state) {
      state.token = ''
      localStorage.setItem('token', '')
    },
    changeI18n(state, i18n) {
      state.i18nLocale = i18n
    },
    setUserInfo(state, userInfo) {
      state.userInfo = userInfo
    },
    changeDrawerOff(state) {
      setTimeout(function() {
        state.drawer = false
      }, 500)
    },
    changeDrawerOn(state) {
      setTimeout(function() {
        state.drawer = true
      }, 500)
    },
    reverseDrawer(state) {
      state.drawer = !state.drawer
    },
    setMenuItems(state, items) {
      state.menuItems = items
    },
    setMaxHeight(state,height){
      state.maxHeight = height
    },
  }
});

export default store;
```
### router
`router` Vue Router 是 Vue.js 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建单页面应用变得易如反掌。<br>
封装如下:
``` js
import Vue from 'vue'
import Router from 'vue-router'
import store from "@/store/index";
import account from '@/page/account/index'
import index from '@/page/index/index'
import home from '@/page/home/home'
import team from '@/page/team/teacher-team'
import work from '@/page/work/work-list'
import course from '@/page/course/course'
import plot from '@/page/plot/plot-pic'
import video from '@/page/plot/plot-video'
import about from '@/page/about/index'
import contact from '@/page/contact/contact'
import research from '@/page/research/research'
import business from '@/page/waibao/businessProfile'
import serviceCase from '@/page/waibao/serviceCase'

Vue.use(Router)

const router = new Router({
  mode: 'history',
  routes: [{
      path: '/',
      component: account,
    },
    {
      path: '/login',
      component: account,
    },
    {
      path: '/index',
      component: index,
      children: [{
          path: '/home',
          component: home
        },
        {
          path: '/team',
          component: team
        },
        {
          path: '/work',
          component: work
        },
        {
          path: '/course',
          component: course
        },
        {
          path: '/plot',
          component: plot
        },
        {
          path: '/video',
          component: video
        },
        {
          path: '/about',
          component: about
        },
        {
          path: '/contact',
          component: contact
        },
        {
          path: '/research',
          component: research
        },
        {
          path: '/businessProfile',
          component: business
        },
        {
          path: '/serviceCase',
          component: serviceCase
        }
      ]
    },

  ]
})
//登录拦截 暂时去掉
/* router.beforeEach((to, from, next) => {
  const token = store.state.token
  if (to.matched.some(record => record.meta.noLogin)) {
    //路由元信息requireAuth:true，或者homePages:true，则不做登录校验
    next()
  } else {
    if (token) { //判断用户是否登录
      if (Object.keys(from.query).length === 0) { //判断路由来源是否有query，处理不是目的跳转的情况
        next()
      } else {
        let redirect = from.query.redirect //如果来源路由有query
        if (to.path === redirect) { //这行是解决next无限循环的问题
          next()
        } else {
          next({
            path: redirect
          }) //跳转到目的路由
        }
      }
    } else {
      if (to.path === "/login") {
        next({
          path: "/",
          query: {
            redirect: from.fullPath
          } //将目的路由地址存入login的query中
        })
      } else {
        next({
          path: "/",
          query: {
            redirect: to.fullPath
          } //将目的路由地址存入login的query中
        })
      }
    }
  }
  return
}) */
export default router
```
### vuescroll
`vuescroll` vuescroll 是一款基于 Vue.js 自定义滚动条的插件，它有两种模式:<br>
* native: 适用于 PC 端， 支持基本的自定义滚动条。
* slide: 适用于移动端， 支持下拉-加载，上拉刷新，轮播等。<br>
但是，这并不意味着 slide 模式只能用于移动端，只是因为移动端与 slide 模式更加契合而已。<br>
代码如下:
``` html
<v-responsive max-height="428">
  <vue-scroll>
	<v-container class="pb-5">
	  <template v-for="(item,index) in latestItems">
		<v-row no-gutters :key="index">
		  <v-col>
			<p class="body-2"><a :href="item.url" target="_blank">@{{item.name}} </a>{{item.title}}</p>
		  </v-col>
		</v-row>
		<v-row no-gutters class="pb-5 row-line mb-5">
		  <v-col cols="12" md="8" class="caption" align-self="center">
			<v-icon x-small>mdi-timer</v-icon> {{item.time}}
		  </v-col>
		  <v-col cols="12" md="4" class="d-flex flex-row-reverse" align-self="center">
			<v-menu offset-y>
			  <template v-slot:activator="{ on }">
				<v-btn text icon v-on="on" x-small>
				  <v-icon>mdi-dots-horizontal</v-icon>
				</v-btn>
			  </template>
			  <v-list dense subheader>
				<v-list-item v-for="(item, index) in item.keyWords" :key="index">
				  <v-list-item-content>{{ item }}</v-list-item-content>
				</v-list-item>
			  </v-list>
			</v-menu>
		  </v-col>
		</v-row>
	  </template>
	</v-container>
  </vue-scroll>
</v-responsive>
```
用法:
``` html
<v-responsive max-height="428">
  <vue-scroll>
  ....
  </vue-scroll>
</v-responsive>
```
效果:
![xg6](./img/xg6.png)<br>
### vue-video-player
`vue-video-player` 适用于 Vue 的 video.js 播放器组件。Video.js 是一个为HTML5世界而构建的网络视频播放器。它支持HTML5和Flash视频，以及YouTube和Vimeo（通过插件）。<br>
代码如下:
``` vue
<template>
  <v-responsive class="overflow-y-auto" :max-height="$store.state.maxHeight">
  <section>
    <v-row >
      <v-col md="6" cols="12" sm="12" v-for="(item,key) in listOptions" :key="key">
        <video-player class="video-player vjs-custom-skin"
                      ref="videoPlayer"
                      :playsinline="true"
                      :options="item">
        </video-player>
      </v-col>
    </v-row>
  </section>
</v-responsive>
</template>
<style>
  .demo{
    display: inline-block;
    width: 1920px;
    /*height: 1080px;*/
    text-align: center;
    line-height: 100px;
    border: 1px solid transparent;
    border-radius: 4px;
    overflow: hidden;
    background: #fff;
    position: relative;
    box-shadow: 0 1px 1px rgba(0, 0, 0, .2);
    margin-right: 4px;
  }

  .demo:hover{
    display: block;
  }
</style>
<script>

  import { videoPlayer } from 'vue-video-player';

  export default {
    components: {
        videoPlayer
    },
    data () {
      return {
        listOptions:[
          {
            //播放速度
            playbackRates: [0.5, 1.0, 1.5, 2.0],
            //如果true,浏览器准备好时开始回放。
            autoplay: false,
            // 默认情况下将会消除任何音频。
            muted: false,
            // 导致视频一结束就重新开始。
            loop: false,
            // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
            preload: 'auto',
            language: 'zh-CN',
            // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
            aspectRatio: '16:9',
            // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
            fluid: true,
            sources: [{
              //类型
              type: "video/mp4",
              //url地址
              src: 'http://vjs.zencdn.net/v/oceans.mp4'
            }],
            //你的封面地址
            poster: '../../../static/video/et.jpg',
            //允许覆盖Video.js无法播放媒体源时显示的默认信息。
            notSupportedMessage: '此视频暂无法播放，请稍后再试',
            controlBar: {
              timeDivider: true,
              durationDisplay: true,
              remainingTimeDisplay: false,
              //全屏按钮
              fullscreenToggle: true
            }
          },
          {
            //播放速度
            playbackRates: [0.5, 1.0, 1.5, 2.0],
            //如果true,浏览器准备好时开始回放。
            autoplay: false,
            // 默认情况下将会消除任何音频。
            muted: false,
            // 导致视频一结束就重新开始。
            loop: false,
            // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
            preload: 'auto',
            language: 'zh-CN',
            // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
            aspectRatio: '16:9',
            // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
            fluid: true,
            sources: [{
              //类型
              type: "video/mp4",
              //url地址
              src: 'http://vjs.zencdn.net/v/oceans.mp4'
            }],
            //你的封面地址
            poster: '../../../static/video/et.jpg',
            //允许覆盖Video.js无法播放媒体源时显示的默认信息。
            notSupportedMessage: '此视频暂无法播放，请稍后再试',
            controlBar: {
              timeDivider: true,
              durationDisplay: true,
              remainingTimeDisplay: false,
              //全屏按钮
              fullscreenToggle: true
            }
          },
          {
            //播放速度
            playbackRates: [0.5, 1.0, 1.5, 2.0],
            //如果true,浏览器准备好时开始回放。
            autoplay: false,
            // 默认情况下将会消除任何音频。
            muted: false,
            // 导致视频一结束就重新开始。
            loop: false,
            // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
            preload: 'auto',
            language: 'zh-CN',
            // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
            aspectRatio: '16:9',
            // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
            fluid: true,
            sources: [{
              //类型
              type: "video/mp4",
              //url地址
              src: 'http://vjs.zencdn.net/v/oceans.mp4'
            }],
            //你的封面地址
            poster: '../../../static/video/et.jpg',
            //允许覆盖Video.js无法播放媒体源时显示的默认信息。
            notSupportedMessage: '此视频暂无法播放，请稍后再试',
            controlBar: {
              timeDivider: true,
              durationDisplay: true,
              remainingTimeDisplay: false,
              //全屏按钮
              fullscreenToggle: true
            }
          },
          {
            //播放速度
            playbackRates: [0.5, 1.0, 1.5, 2.0],
            //如果true,浏览器准备好时开始回放。
            autoplay: false,
            // 默认情况下将会消除任何音频。
            muted: false,
            // 导致视频一结束就重新开始。
            loop: false,
            // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
            preload: 'auto',
            language: 'zh-CN',
            // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
            aspectRatio: '16:9',
            // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
            fluid: true,
            sources: [{
              //类型
              type: "video/mp4",
              //url地址
              src: 'http://vjs.zencdn.net/v/oceans.mp4'
            }],
            //你的封面地址
            poster: '../../../static/video/et.jpg',
            //允许覆盖Video.js无法播放媒体源时显示的默认信息。
            notSupportedMessage: '此视频暂无法播放，请稍后再试',
            controlBar: {
              timeDivider: true,
              durationDisplay: true,
              remainingTimeDisplay: false,
              //全屏按钮
              fullscreenToggle: true
            }
          }
        ],
      }
    },
    mounted() {
      
    },
    methods:{
        initVideo(){

        }
    },
    computed: {
        player() {
            return this.$refs.videoPlayer.player
        }
    }
  }
</script>
```
效果如下:<br>
![file1](README_files/1.jpg)
### vue-photo-preview
`vue-photo-preview` vue-photo-preview是基于photoswipe的vue图片预览插件<br>
代码如下:
``` vue
<template>
  <v-responsive class="overflow-y-auto" :max-height="$store.state.maxHeight">
  <v-row>
    <v-col
      v-for="(img,index) in imgList"
      :key="index"
      class="d-flex child-flex"
      cols="12"
      md="2"
      sm="2"
    >
      <v-card flat tile class="d-flex">
        <photo-card :img="img" :index="index"></photo-card>
      </v-card>
    </v-col>
  </v-row>
</v-responsive>
</template>
<style></style>
<script>

  import PhotoCard from "../../components/pic/photo-card";
  export default {
    components: {PhotoCard},
    data () {
      return {
      }
    },
    computed:{
      imgList(){
        let imgListArr = [];
        for(let i=0;i<46;i++){
          imgListArr.push("../../../static/video/img"+(i+1)+".jpg");
        }
        return imgListArr;
      }
    },
    methods: {
        imgSrc(n){
            // return "../../../static/img/dabai.jpg";
            return "https://picsum.photos/500/300?image="+n;
        },
    },
    mounted(){

    }

  }
</script>
```
效果如下:<br>
![file2](README_files/2.jpg)
## 环境准备
拿到源码后需要配置启动环境<br>
nodejs 用于Node.js是一个事件驱动I/O服务端JavaScript环境<br>
IntelliJ IDEA 开发环境`墙裂推荐`使用IDEA方便之后的后台开发,还可以使用`VS Code`,`HBuilder X`等
### nodejs安装
[nodejs下载地址](http://nodejs.cn/download/)<br>
Windows 上安装 Node.js<br>
![nodejs1](./img/nodejs1.jpg)<br>
步骤 1 : 双击下载后的安装包如下所示：<br>
![nodejs2](./img/nodejs2.png)<br>
步骤 2 : 点击以上的Run(运行)，将出现如下界面：<br>
![nodejs3](./img/nodejs3.png)<br>
步骤 3 : 勾选接受协议选项，点击 next（下一步） 按钮 :<br>
![nodejs4](./img/nodejs4.png)<br>
步骤 4 : Node.js默认安装目录为 "C:\Program Files\nodejs\" , 你可以修改目录，并点击 next（下一步）：<br>
![nodejs5](./img/nodejs5.png)<br>
步骤 5 : 点击树形图标来选择你需要的安装模式 , 然后点击下一步 next（下一步）<br>
![nodejs6](./img/nodejs6.png)<br>
步骤 6 :点击 Install（安装） 开始安装Node.js。你也可以点击 Back（返回）来修改先前的配置。 然后并点击 next（下一步）：<br>
![nodejs7](./img/nodejs7.png)<br>
安装过程：<br>
![nodejs8](./img/nodejs8.png)<br>
点击 Finish（完成）按钮退出安装向导。<br>
![nodejs9](./img/nodejs9.png)<br>
检测PATH环境变量是否配置了Node.js，点击开始=》运行=》输入"cmd" => 输入命令"path"，输出如下结果：
```
PATH=C:\oraclexe\app\oracle\product\10.2.0\server\bin;C:\Windows\system32;
C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;
c:\python32\python;C:\MinGW\bin;C:\Program Files\GTK2-Runtime\lib;
C:\Program Files\MySQL\MySQL Server 5.5\bin;C:\Program Files\nodejs\;
C:\Users\rg\AppData\Roaming\npm
```
我们可以看到环境变量中已经包含了C:\Program Files\nodejs\ 至此node环境已经安装完成
### IntelliJ IDEA安装
[IntelliJ IDEA下载地址](https://www.jetbrains.com/idea/download/#section=windows)<br>
Windows 上安装 IntelliJ IDEA<br>
![idea1](./img/idea1.jpg)<br>
![idea2](./img/idea2.jpg)<br>
步骤 1 : 双击下载后的安装包如下所示：<br>
![idea3](./img/idea3.jpg)<br>
步骤 2 : 点击以上的Next(下一步)，将出现如下界面：<br>
![idea4](./img/idea4.jpg)<br>
步骤 3 : 你可以修改目录，并点击 next（下一步）：<br>
![idea5](./img/idea5.jpg)<br>
步骤 4 : 可以选择创建桌面图标,配置关联文件等,并点击 next（下一步）：<br>
![idea6](./img/idea6.jpg)<br>
步骤 5 : 点击Install 开始安装<br>
![idea7](./img/idea7.png)<br>
安装过程：<br>
![idea8](./img/idea8.png)<br>
点击 Finish（完成）按钮退出安装向导。<br>
打开安装完成后的IDEA<br>
![idea9](./img/idea9.png)<br>
是否导入配置，我选择的是不导入<br>
后面请一路next直到激活界面，选择试用<br>
![idea10](./img/idea10.PNG)<br>
![idea11](./img/idea11.PNG)<br>
## 无环境启动
方式一:直接打开线上网站进行观看[链接](http://vue.etoak.com/)<br>
方式二:启动下载目录中的nginx-1.16.1<br>
进入目录按住Shift 点击鼠标右键<br>
![img1](./img/img1.png)<br>
选择`在此处打开 Powershell 窗口`打开命令行窗口 输入start nginx<回车>启动nginx 如下:<br>
![img2](./img/img2.jpg)<br>
在浏览器中直接访问[http://localhost:8090](http://localhost:8090)<br>
输入.\nginx.exe -s stop 停止nginx 如下:<br>
![img3](./img/img3.jpg)<br>
`或者执行nginx-1.16.1目录中的启动.bat/停止.bat`
## 编译安装
如已安装好环境请继续,如未安装好请看[环境准备](#环境准备)<br>
进入下载文件中的et目录按住Shift 点击鼠标右键<br>
![img1](./img/img1.png)<br>
选择`在此处打开 Powershell 窗口`打开命令行窗口 输入npm install<回车> 如下:<br>
![img4](./img/img4.jpg)<br>
安装完成后会在et目录下生成node_modules目录<br>
直接启动: 在Powershell窗口中直接输入npm run dev <回车> <br>
![img5](./img/img5.jpg)<br>
在浏览器中直接访问[http://localhost:8090](http://localhost:8090)<br>
`或者执行et目录中的ETInstall.bat/ETRun.bat`
在IDEA中启动:<br>
![img6](./img/img6.jpg)<br>
选择et目录<br>
![img7](./img/img7.jpg)<br>
![img8](./img/img8.jpg)<br>
![img9](./img/img9.jpg)<br>
配置node路径<br>
![img10](./img/img10.jpg)<br>
![img11](./img/img11.jpg)<br>
启动完成后在浏览器中直接访问[http://localhost:8090](http://localhost:8090)<br>