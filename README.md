# docsify-samples

docsify示例


[官网文档](https://docsify.js.org/#/zh-cn/quickstart)

## 新建项目

#### 安装

```
$ npm i docsify-cli -g
```

#### 初始化

```
$ docsify init ./docs
``` 

#### 运行

```
$ cd docs
$ docsify serve

或

// 不用进入docs目录运行
$ docsify serve docs
```

## 功能

### 添加封面

- 在 `docs/index.html` 中添加 `coverpage:true` 参数开启封面渲染

```
<script>
    window.$docsify = {
      ...
      coverpage: true
    }
</script>
```

- 添加 `_coverpage.md` 封面文件

```
![logo](https://docsify.js.org/_media/icon.svg)

# 测试文档

> 测试说明

* 前端框架：vue-cli、vue-router、axios、vuex
* UI类库：Mint-UI、Vant
* 后端数据接口：Express、MongoDB

<!-- 背景图片 -->

![](_media/bg.png)

<!-- 背景色 -->

![color](#f0f0f0)

[GitHub](https://github.com/otary/docsify-samples.git)
[Get Started](#quick-start)
```
- 效果

![](./images/fenmian.png)

### 自定义侧边栏


### 自定义导航栏


### 代码高亮


### 离线模式


