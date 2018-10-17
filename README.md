# vue-marquee-lite


## 前言

基于vue跑马灯。

## Project setup
```
yarn install vue-marquee-lite
```

# 需要用到该组件时可以这样引入
```
<template>
    <div>
        <vue-marquee-lite
          className="paomadeng"
          :data="list"
          :space="0"
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