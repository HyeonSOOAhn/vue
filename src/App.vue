<template>
  <transition name="fade">
  <Modal @closeModal="모달창열렸니 = false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니 = "모달창열렸니"/>
  </transition>

  <div class="menu">
    <a v-for="a in 메뉴들" :key="a">{{a}}</a>
  </div>

  <Discount v-if="showDiscount=true" :discount="discount"/>

  <button @click="ascSort">가격낮은순정렬</button>
  <button @click="desSort">가격높은순정렬</button>
  <button @click="nameSort">이름순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="모달창열렸니 = true; 누른거 = $event" v-for="원룸 in 원룸들" :key="원룸" :원룸="원룸"/>
  


</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './card.vue';

export default {
  name: 'App',
  data(){
    return {
      discount : 30,
      showDiscount : true,
      원룸들오리지널 : [...data],
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },

  methods: {
    increase(){
      this.신고수++;
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    },
    ascSort(){
      this.원룸들.sort(function(a,b){
        return a.price - b.price;
      });
    },
    desSort(){
      this.원룸들.sort(function(a,b){
        return b.price - a.price;
      });
    },
    nameSort(){
      this.원룸들.sort(function(a,b){
        return a.title<b.title ? -1 : a.title>b.title ? 1:0;
      });
    },
  },

  mounted() {
    setInterval(() => {
        this.discount--;
      }, 1000);
  },


  

  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
.fade-leave-from{
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}

.fade-enter-from{
  transform: translate(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  transform: translate(0px);
}

body{
  margin: 0;
}
div{
  box-sizing: border-box;
}

.discount{
  background: #eee;
  padding: 10%;
  margin: 10px;
  border-radius: 5px;
}

.black-bg{
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg{
  width: 50%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img{
  width: 100%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding: 15;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}
</style>
