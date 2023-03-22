---
title: vue+swiper实现弹幕滚动效果
categories:
  - 前端学习
tags:
  - vue
  - swiper
date: 2022-08-16 15:15:52
index_img: 'https://img2.baidu.com/it/u=2198457933,2948913030&fm=253&fmt=auto&app=138&f=PNG?w=640&h=380'
---
### 效果
<img src="/img/sample/a016/a016.gif" alt="">

### 依赖版本
1. package.json

```json
    "swiper": "^3.4.2",
    "vue": "^2.5.2",
    "vue-awesome-swiper": "^3.1.3"
```
2. main.js

```js
  import VueAwesomeSwiper from 'vue-awesome-swiper'
  import 'swiper/dist/css/swiper.css'
  Vue.use(VueAwesomeSwiper)
```


### html部分
```html
<template>
  <div id="app">
    <div class="recom">
      <div class="notice-inner">
        <swiper
          ref="mySwiper"
          :options="swiperOptions"
          v-if="operatorList.length > 0"
          class="notice-warp notice-box1"
        >
          <swiper-slide
            class="notice-item"
            v-for="(item, index) in operatorList"
            :key="index"
          >
            <img :src="item.headpoart" alt="" />
            <span>{{ item.nickname }}：{{ item.content }}</span>
          </swiper-slide>
        </swiper>
      </div>
    </div>
  </div>
</template>
```


### js部分
```javascript
<script>
export default {
  data() {
    return {
      operatorList: [
        {
          content: '推荐了该商品',
          headpoart:
            'http://thirdqq.qlogo.cn/g?b=oidb&k=rUNicgjviaaXicdnhE5hsicKcg&s=640&t=1557262645',
          nickname: '韩宝妞~'
        },
        {
          content: '兑换了该商品1次',
          headpoart:
            'https://csfile.ossxrcloud.net/ydnResource/2022-01-25/155590301611_1643100097337.jpg',
          nickname: '菜菜'
        },
        {
          content: '推荐了该商品',
          headpoart:
            'https://csfile.ossxrcloud.net/ydnResource/2021-09-16/162400612511_1631762223869.jpg',
          nickname: '耳机分泥一半'
        },
        {
          content: '推荐了该商品',
          headpoart:
            'https://csfile.ossxrcloud.net/ydnImg/200X200/802dac9a93084_1641346280372.png',
          nickname: '本特利'
        },
        {
          content: '推荐了该商品',
          headpoart:
            'https://file.xinruiyun.cn/resource/2020-05-15/8349373d-9ab1-4a4d-a59c-8c65e150deb4.png',
          nickname: '哈哈哈'
        }
      ],
      swiperOptions: {
        autoplay: {
          delay: 3000
        },
        direction: 'vertical',
        loop: true,
        // width: 4.2 * parseInt(document.documentElement.style.fontSize),
        height: 0.68 * parseInt(document.documentElement.style.fontSize),
        // freeMode:true,
        slidesPerView: 'auto',
        centeredSlides: true,
        on: {
          slideChange: () => {
            // this.swiperIndex = this.$refs['mySwiper'].swiper.realIndex;
          }
        }
      },
      swiperIndex: 0
    };
  }
};
</script>
```


### css部分
```css
<style>
* {
  margin: 0;
  padding: 0;
}

.recom {
  padding: 0.28rem 0;
  height: 2.4rem;
  width: 100%;
  background: skyblue;
  /* pointer-events: none; */
}

.notice-inner {
  margin: 0 0.4rem;
  height: 2.04rem;
  overflow: hidden;
  font-size: 14px;
}

.notice-item {
  height: 0.68rem;
  background: orangered;
  font-size: 0.26rem;
  color: #ffffff;
  display: flex;
  transition-property: top;
  transition-timing-function: linear;
}

.notice-item:nth-child(2n) {
  background: pink;
}

.notice-item:nth-child(3n) {
  background: yellowgreen;
}

.notice-item.swiper-slide {
  height: 0.68rem;
}

.notice-item img {
  width: 0.48rem;
  height: 0.48rem;
  margin-right: 0.2rem;
  border-radius: 50%;
}
</style>
```