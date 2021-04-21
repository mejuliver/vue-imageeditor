# vue-imageeditor
vue image editor base on [camanjs](http://camanjs.com/) and [advance cropper](https://norserium.github.io/vue-advanced-cropper/) 

# import the package

```import imageeditor from '@mejuliver/vue-imageeditor';```

# insert the component

```<imageeditor @saveImage="saveImage" ref="image" accept=".jpg,.png" />```
   
# add vue instance as component and set a save image method

```
components : { imageeditor },
methods : {
  saveImage(e){
    this.imgpreview = e.src;
    this.fileimage = e.blob;         
  } 
}
```
