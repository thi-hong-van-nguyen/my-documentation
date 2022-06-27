JS file
```
<div class='animation-bar'>
  <span style="width:60%"></span>
</div>
```

CSS file
```
body {
  background: #f7e6ff;
  /*   width:100%; */
}
.animation-bar {
  position: relative;
  /*   height: 16px; */
  display: block;
  padding: 3px;
  /*   font-size: 30px; */
  /*   line-height: 30px; */
  border-radius: 30px;
  background: white;
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.25),
    0 1px rgba(255, 255, 255, 0.5);
}

.animation-bar span {
  position: relative;
  display: inline-block;
  vertical-align: middle;
  height: 20px;
  border-radius: 10px 0 0 10px;
  overflow: hidden;
  background-color: #82469e;
  background-size: 100%;
  background-image: linear-gradient(to bottom, #d695f5, #82469e);
  animation: progress-bar 6s ease;
}

.animation-bar span::after {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  content: "";
  background-size: 100%;
  background-image: linear-gradient(
    45deg,
    #fff 25%,
    rgba(0, 0, 0, 0) 25%,
    rgba(0, 0, 0, 0) 50%,
    #fff 50%,
    #fff 75%,
    rgba(0, 0, 0, 0) 75%,
    rgba(0, 0, 0, 0)
  );
  background-size: 30px 30px;
  opacity: 0.5;
  animation: progress-bar-after 0.5s infinite linear;
}

@keyframes progress-bar {
  0% {
    width: 0%;
  }

  100% {
    width: 60%;
  }
}

@keyframes progress-bar-after {
  0% {
    background-position: 0 100%;
  }
  100% {
    background-position: 30px 100%;
  }
}

```
