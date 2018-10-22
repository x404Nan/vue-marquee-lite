# vue-marquee-lite


## 前言

基于vue跑马灯。

## Project setup
```
yarn install vue-marquee-lite
```

## 需要用到该组件时可以这样引入
```
<template>
    <div>
        <vue-marquee-lite
          className="paomadeng"
          :data="list"
        />
    </div>
</template>
<script>
import Vue from 'vue';
import vueMarquee from 'vue-marquee-lite';
import 'vue-marquee-lite/lib/vue-marquee-lite.css'
Vue.use(vueMarquee);
</script>

```

## 属性设置
```
duration  控制速率 //默认 50

className 自定义class名 //默认 marquee-wrapper

space 可控制和下个列表的间距 // 默认 0

type  动画方式 transform / position // 默认transform

```