# css3
## Pretty Loader
 
  看到一个loader的效果图感觉挺有意思，花点儿时间搞一搞
- 想法

利用 css 3 keyframes创建动画，运用点儿定位
  
- 效果图
  
  ![](./image/loader.gif)
 ---
  构思步骤
  
  1. 先将静态图画出来  
  
  2. 外边框出现  
  
  3. 内块进来  
  
  4. 方块退出
  
  5. 边框原路退出
  
  
  
---

CSS3的alternate 可以完成4、5,边框的移动可以用伪元素完成

- 之后就按照1先画个草图o(*^＠^*)o
```html
          <div class="wrapper">           
            <div class="load">
                <div class="white"></div>
                <div class="orange"></div>
                <div class="red"></div>
            </div>
        </div>
```
        
- 对应样式
```css

      .load {
        position: relative;
        width: 100px;
        height: 100px;
        border: 4px solid black;
        box-sizing: border-box;
        background-color: white;
        }
      .load > div {
        position: absolute;
      }
      .red{
        top: 0;
        bottom: 0;
        left: 0;
        width: 27%;
        border-right: 4px solid black;
        background-color: #EA5664;
      }
      .orange{
        bottom:0;
        right:4px;
        left:27%;
        border-top: 4px solid black;
        background: #ECBA59;
        height:50%
      }
      .white{
         top:4px;
         width:27%;
         right:5px;
         height: 50%;
         bottom: 50%;
         border-left: 4px solid black;
         background: #fff;
      } 
```


- 图片画成最终的样子后需要加伪元素把自身边框去掉

```css
      .logo::before,.logo::after{
          content: '';
          position: absolute;
          width:100%;
          height: 100%;
          box-sizing: border-box;
          border:4px solid transparent;          
      }

      .load::before{
        top:0;
        left:0;
        border-top-color:black;
        border-right-color: black;
      }
    .load::after{
        bottom:0;
        right: 0;
        border-bottom-color:#000;
        border-left-color: #000;

    }
```

- 为before和after定制专属动画 <sub>ps:这个需要在浏览器慢慢调~</sub>


```css
    /* keyframes */
@keyframes border-before {
    0% {
      width: 0;
      height: 0;
      border-right-color: transparent;
    }
    5.99% {
      border-right-color: transparent;
    }
    6% {
        height: 0;
        width: 100%;
        border-right-color: #000;
      }
    25%,100% {
      height: 100%;
      width: 100%;
    }
}
  @keyframes border-after {
    0% ,24.99%{
      width: 0;
      height: 0;
      border-left-color: transparent;
      border-bottom-color: transparent;
    }
    25% {
        border-left-color: transparent;
        border-bottom-color: #000;

    }
    36.99%{
        border-left-color: transparent;
    }
    37% {
		      height: 0;
        width: 100%;
		      border-left-color: #000;
    }
    50%,
    100% {
      width: 100%;
      height: 100%;
    }
  }
    
```
- 内部方块的动画大同小异

```css
  @keyframes red {
    0%,
    50% {
      width: 0;
      opacity: 0;
    }
    50.01% {
      opacity: 1;
    }
    65%,
    100% {
      width: 27%;
      opacity: 1;
    }
  }

```
基本完成\(^o^)/~


[源码](./loading)<sub>其实有很多方法实现~</sub>
