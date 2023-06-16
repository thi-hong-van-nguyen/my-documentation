## Create equal divs in Flexbox with one scrollable
![image](https://github.com/thi-hong-van-nguyen/my-documentation/assets/85480610/e5faddaf-683b-4126-a217-92874584ac53)
2 divs with one dynamic height and the other one scrollable based on the first div height
```
<div class="container">
  <div class="dynamic-height border">
    // Less content
  </div>
  
  <div class="scrollable-container border">
    <div class="scrollable-content">
      // More content
    </div>
  </div>
</div>
```

`CSS`
```
.container {
  display: flex;
  gap: 1rem;
}

.dynamic-height {
  flex: 1;
  position: relative;
  /* Styles for the first div */
}

.scrollable-container {
  position: relative;
  flex: 1;
  overflow: hidden;
}

.scrollable-content {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  overflow-y: auto;
  /* Styles for the second div */
}
```
