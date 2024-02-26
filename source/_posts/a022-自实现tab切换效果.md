---
title: 自实现tab切换效果
categories:
  - 前端学习
tags:
  - 切换居中
  - 下划线动画
date: 2023-11-24 21:04:25
index_img: https://img2.baidu.com/it/u=3975996938,3844591049&fm=253&fmt=auto&app=138&f=GIF?w=1200&h=480
---

### 效果

<img src="/img/sample/a022/a022.gif" alt="">

### 描述
类似于vant组件库的tab组件，可以实现超长自动滚动居中，下划线动态移动

### 代码部分

TabScroll.jsx

```javascript
import React, { Component } from 'react';

class TabScroll extends Component {
    nav = ['标签1', '标签2', '标签3', '标签4', '标签5', '标签6', '标签7']
    state = {
        navIndex: 0
    }

    render() {
        const { navIndex } = this.state
        return (
            <div className='tab-scroll'>
                <div className='tab'>
                    {this.nav.map((item, index) =>
                        <div
                            key={index}
                            className={['tab-item', navIndex === index ? 'cur' : ''].join(' ')}
                            onClick={() => {
                                this.setState({ navIndex: index })

                                const curTabDom = document.querySelectorAll('.tab-item')[index]

                                //点击居中
                                const scrollDom = document.querySelector('.tab')
                                const left = curTabDom.offsetLeft - (scrollDom.offsetWidth - curTabDom.offsetWidth) / 2
                                scrollDom.scrollTo({ left, behavior: 'smooth' });

                                //横线移动
                                const line = document.querySelector('.line')
                                line.style = ` transform: translateX(${curTabDom.offsetLeft + (curTabDom.offsetWidth / 2) - line.offsetWidth}px);transition-duration: 0.2s;`;
                            }}
                        >
                            <span>{item}</span>
                        </div>)
                    }
                    <i className='line'></i>
                </div>
                <h3>内容{navIndex + 1}</h3>
            </div>
        );
    }
}

export default TabScroll;
```

index.less

```less
.tab-scroll {
  .tab {
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
    overflow-x: scroll;
    position: relative;

    &::-webkit-scrollbar {
      width: 0;
      display: none;
    }

    .tab-item {
      flex-shrink: 0;
      width: 100px;
      height: 40px;
      line-height: 40px;
      text-align: center;
      background: #e0e0e0;
      border-right: 1px solid #fff;
      position: relative;

      // &.cur {
      //   background: skyblue;
      // }
    }

    .line {
      z-index: 2;
      position: absolute;
      bottom: 0;
      left: 25px; //第一个tab-line到左侧距离
      width: 50px;
      height: 6px;
      border-radius: 3px;
      background-color: pink;
    }
  }
}
```
