<script setup>
import {ref,reactive} from "vue";
const slides = [
  {
    id:1,
    title:'Slide One',
    description:'Slide One description',
    imageUrl:'../src/assets/images/bird-1.jpg',
  },
  {
    id:2,
    title:'Slide Two',
    description:'Slide Two description',
    imageUrl:'../src/assets/images/bird-2.jpg',
  },
  {
    id:3,
    title:'Slide Three',
    description:'Slide Three description',
    imageUrl:'../src/assets/images/bird-3.jpg',
  },
  {
    id:4,
    title:'Slide Four',
    description:'Slide Four description',
    imageUrl:'../src/assets/images/bird-4.jpg',
  },
  {
    id:5,
    title:'Slide Five',
    description:'Slide Five description',
    imageUrl:'../src/assets/images/bird-5.jpg',
  },{
    id:6,
    title:'Slide Six',
    description:'Slide Six description',
    imageUrl:'../src/assets/images/bird-6.jpg',
  },
]

const slide = reactive({
  imgUrl:slides[0].imageUrl, index:0
})

function changeImage(indexNumber){
  slide.imgUrl = slides[indexNumber].imageUrl
  slide.index = indexNumber
}

function nextImage(){
  if (slide.index < slides.length-1){
    slide.imgUrl = slides[slide.index+1].imageUrl
    slide.index = slide.index+1
  }else {
    slide.imgUrl = slides[0].imageUrl
    slide.index = 0
  }
}
//
function prevImage(){
  if ((slide.index <= slides.length-1) && (slide.index > 0)){
    slide.imgUrl = slides[slide.index-1].imageUrl
    slide.index = slide.index-1
  }else {
    slide.imgUrl = slides[slides.length-1].imageUrl
    slide.index = slides.length-1
  }
}

setInterval(()=>{
  nextImage()
},4000)

</script>

<template>
  <section class="bg-light pt-100 pb-100">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h1 class="fw-bold">Image Carousel Module-4 Assignment</h1>
        </div>
        <div class="col-lg-9" style="position: relative">
          <img :src="slide.imgUrl" id="show" class="img-fluid slide-height slide-animation" alt="">
          <div class="dot-wrapper">
            <span class="dot" v-for="(mySlide,key) in slides" :class="slide.imgUrl==mySlide.imageUrl ? 'active-dot':''" :key="key" @click="changeImage(key)"></span>
          </div>

          <div class="navigation">
            <button class="btn btn-secondary me-2 rounded-0" @click="prevImage()"><i class="fa fa-arrow-left"></i></button>
            <button class="btn btn-secondary rounded-0" @click="nextImage()"><i class="fa fa-arrow-right"></i></button>
          </div>

        </div>
        <div class="col-lg-3 d-md-block d-sm-none">
          <div class="row slide-info">
            <template v-for="(mySlide,key) in slides" :key="key">
              <div class="col-lg-4 col-md-2 p-1" :class="slide.imgUrl==mySlide.imageUrl ? 'active-thumbnail':''" @click="changeImage(key)"><img class="img-fluid p-1" :src="mySlide.imageUrl" alt="Icon"></div>
            </template>

<!--            <div class="col-10">-->
<!--              <h5>{{ mySlide.title }}</h5>-->
<!--              <p>{{ mySlide.description }}</p>-->
<!--            </div>-->
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.dot-wrapper{
  position: absolute;
  left: 25px;
  bottom: 5px;
}
.dot{
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: #ffffff;
  z-index: 10000;
  display: inline-block;
  margin-right: 5px;
}

.active-dot{
  background-color: #444444;
}

.navigation{
  position: absolute;
  right: 25px;
  bottom: 15px;
}
.slide-height{
  width: 100%;
  height: auto;
}
.active-thumbnail{
  border: 2px solid #888888;
  box-sizing: border-box;
}
.slide-animation{
  animation-name: animation;
  animation-duration: 4s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
@keyframes animation {
  0% {opacity: 0.2;}
  20% {opacity: 1.0;}
  80% {opacity: 1.0;}
  100% {opacity: 0.2;}
}
</style>
