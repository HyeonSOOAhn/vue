<template>
    <div class="black-bg" v-if="모달창열렸니==true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width : 100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <input v-model.number="month">
      <p> {{month}}개월 선택함 : {{원룸들[누른거].price * month}}</p>
      <button @click="close">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name : 'Modal',
    data(){
      return{
        month : 3,
      }
    },
    watch : {
      month(a){
       if(a>=13){
         alert("13이상 입력하지 마셈");
         this.month = 1;
       }else if(isNaN(a)){
          alert("글자 쓰지 마삼");
          this.month = 1;
       }
      }
    },
    props : {
      원룸들 : Array,
      누른거 : Number,
      모달창열렸니 : Boolean,
    },
    methods : {
      close(){
        this.$emit("closeModal");
      }
    },

    updated() {
    if(this.month<3&&this.month!=""){
      alert("3개월부터만 하셈");
      this.month=3;
    }
  },
}
</script>

<style>

</style>