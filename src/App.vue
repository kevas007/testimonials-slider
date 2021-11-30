<template>
  <div id="app">
    <div class="flex flex-wrap w-full font relative">
     <div class="fonts">
        <div class=" w-full center imge" v-for="(item , index) in imgs" :key="item">
        <transition name="fade">
          <img  v-if="currentSlide == index" v-bind:src="item" alt />
        </transition>
      </div>
      <div class="w-full" style="height:20px">
        <div class="absolute ico bottom-0 flex w-full justify-center">
          <div
            v-for="(item, index ) in imgs"
            :key="item"
            @click="makeActive(index)"
            class="w-10 h-10 mx-2 rounded-full cursor-pointer shadow-md"
          >
            <div
              class="w-4 h-4 mx-2 rounded-full cursor-pointer shadow-md flex justify-center items-center"
              v-for="(icon , i) in icone"
              :key="icon"
            >
              <img
                class="icones"
                :class="currentSlide == index ?  'bg-gray-300':  'bg-white' "
                v-if="index == i"
                :src="icon"
                alt
              />
            </div>
          </div>
        </div>
      </div>
     </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  methods: {
    makeActive(index) {
      this.currentSlide = index;
    }
  }, data() {
    return {
      imgs: [
        require('./assets/images/image-john.jpg'),
        require('./assets/images/image-tanya.jpg')
      ],
      icone: [
        require('./assets/images/icon-prev.svg'),
        require('./assets/images/icon-next.svg'),

      ],
      currentSlide: 0,
      interval: "",
      isTitle: true,
    }
  },
  mounted() {
    this.interval = setInterval(() => {
      this.currentSlide = this.currentSlide == 1 ? 0 : this.currentSlide + 1;
    }, 15000);
  },
  beforeUnmount() {
    clearInterval(this.interval);
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease;
}
.font{
    background-image: url('./assets/images/pattern-bg.svg');

  width: 700px;
  height: 100px;
}
.fonts{
    background-image: url('./assets/images/pattern-quotes.svg');
    width: 700px;
  height: 100px;

}

.fade-enter-from {
  opacity: 0;
  transform: translate(-100%);
}
.fade-leave-to {
  opacity: 0;
  transform: translate(100%);
}
.imge{
  position: absolute;
  overflow: hidden;
  /* right:10; */
}
.imge img{
height:100%;
width:350px;
margin-left: 50%;
margin-top: 8%;
}
.ico{
  top: 450px;
  left: 70px;
  z-index: 1;
  background: #2c3e50;
}
.icones {
  width: 100%;
  height: 30px;
  top:51%;

}
</style>
