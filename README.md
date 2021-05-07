# vue-imageeditor
[vue image editor](https://www.npmjs.com/package/@mejuliver/vue-imageeditor) base on [camanjs](http://camanjs.com/) and [advance cropper](https://norserium.github.io/vue-advanced-cropper/) 

# Installation
```npm install --save @mejuliver/vue-imageeditor vue-advanced-cropper```  
  
the editor is using boostrap 4 for its UI so you need to add it also

```npm install --save bootstrap@4.1.1```  

then import it

```import 'bootstrap/dist/css/boostrap.min.css'```

# import the component

```import imageeditor from '@mejuliver/vue-imageeditor/imageeditor.vue';```

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
