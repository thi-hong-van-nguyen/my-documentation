## Create a box shadow effect for a container when scrolling down or up.

![image](https://github.com/thi-hong-van-nguyen/my-documentation/assets/85480610/bc453e87-dc5d-48af-a2e5-47e4c3b3f5e8)

HTML
```
<div class='scroll-box-shadow'>
  <div style="padding-inline: 20px">
    <div>test test test test test</div>
    <div>test test test test test</div>
    <div>test test test test test</div>
    <div>test test test test test</div>
    <div>test test test test test</div>
    <div>test test test test test</div>
    <div>test test test test test</div>  
  </div>
</div>
```

CSS
```
.scroll-box-shadow {
  margin: 50px;
  height: 80px;
  
  width: fit-content;
  overflow: auto;
    position: relative;
    z-index: 1;
    overflow: auto;
    background: #fff no-repeat;
    background-image: linear-gradient(
            to bottom,
            rgba(0, 0, 0, 0.05) 0%,
            rgba(0, 0, 0, 0) 100%
        ),
        linear-gradient(to top, rgba(0, 0, 0, 0.05) 0%, rgba(0, 0, 0, 0) 100%);
    background-position: 0 0, 0 100%;
    background-size: 100% 14px;
}

.scroll-box-shadow:before,
.scroll-box-shadow:after {
    content: "";
    position: relative;
    z-index: -1;
    display: block;
    height: 30px;
    margin: 0 0 -10px;
    background: -webkit-linear-gradient(
        top,
        #fff,
        #fff 30%,
        rgba(255, 255, 255, 0)
    );
    background: -moz-linear-gradient(
        top,
        #fff,
        #fff 30%,
        rgba(255, 255, 255, 0)
    );
    background: linear-gradient(
        to bottom,
        #fff,
        #fff 30%,
        rgba(255, 255, 255, 0)
    );
}

.scroll-box-shadow:after {
    margin: -10px 0 0;
    background: -webkit-linear-gradient(
        top,
        rgba(255, 255, 255, 0),
        #fff 70%,
        #fff
    );
    background: -moz-linear-gradient(
        top,
        rgba(255, 255, 255, 0),
        #fff 70%,
        #fff
    );
    background: linear-gradient(
        to bottom,
        rgba(255, 255, 255, 0),
        #fff 70%,
        #fff
    );
}
```



