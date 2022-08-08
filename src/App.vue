<template>
  <div class="container">
    <h1>Carousel</h1>
    <div 
    class="carousel">
      <img
      v-for="(image, index) in photos"
      :key="index"
      class="image-class"
      :id="index"
      :src="image"
      >
    </div>
    <div class="dot-container">
    </div>
  </div>
</template>

<script>
import photo from './assets/photo-1.jpg'
import photoTwo from './assets/photo-2.jpg'
import photoThree from './assets/photo-3.jpg'

export default {
  name: 'App',
  components: {
    
  },
  data(){
    return {
      dots: 0,
      dotsArray: [],
      photos: [
        photo,
        photoTwo,
        photoThree
                ]
      }
  },
  methods:{
      setupListeners(){
      const dots = document.querySelectorAll('.dots')
      const dotsArray = [...dots]
      dotsArray.forEach(d => {
        console.log(d);
        d.addEventListener('click', this.hookImagesToDot)
        d.addEventListener('click', this.highlightSelectedDot)
      })
    },
    createDots(){
      const numberOfDots = this.photos.length
      for (let i = 0; i < numberOfDots; i += 1){
        const newButtons = document.createElement('button')
        newButtons.classList.add('dots')
        newButtons.value = i
        newButtons.setAttribute('selected', false)
        console.log(newButtons.value);
        const buttonContainer = document.querySelector('.dot-container')
        buttonContainer.append(newButtons)
      }
    },
    hookImagesToDot(e){
      console.log(e.target.value);
      const photosArray = document.querySelectorAll('.image-class')
      photosArray[e.target.value].scrollIntoView({behavior: "smooth"})
    },
    highlightSelectedDot(e){
      const dots = document.querySelectorAll('.dots')
      dots.forEach(d => {
        d.setAttribute('selected', false)
      })
      e.target.setAttribute('selected', true)
      

    }
  },
  mounted(){
    this.createDots()
      const numberOfDots =  document.querySelectorAll('.image-class')
      const dotsArray = [...numberOfDots]
      dotsArray[1].scrollIntoView({behavior: "smooth"});

      this.dots = this.dotsArray.length
      console.log(this.dots);
      console.log(this.dotsArray);
      this.setupListeners();
  }
}
</script>

<style>
.image-class{
  min-width: 500px;
}

.container {
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.carousel {
  overflow-x: auto;
  display: flex;
  height: 80vh;
  width: 500px;
}

.dots {
  border:none;
  cursor: pointer;
  height: 14px;
  width: 14px;
  margin: 0 4px;
  background-color: black;
  border-radius: 50%;
  display: inline-block;
}

.dots[selected='true'] {
  background-color: hotpink;
}

.dot-container {
  margin-top: 15px;
  display: flex;

}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
