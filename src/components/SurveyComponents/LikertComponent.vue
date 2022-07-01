<template>

    <div class="box"  >
    <div class="row" >
      <div class="col-2" style="padding-top:40px">
        <p>Insert the Question:</p>
      </div>
      <div class="col-9" >
        <q-input v-model="question" />
      </div>
      <div class="col-1">
      <q-icon class="icon" name="fa-solid fa-angle-up" @click="btnclick(0)" />
       <q-icon class="icon" name="fa-solid fa-angle-down"  @click="btnclick2(this.list.length-1)" />
       <q-icon class="icon" name="fa-solid fa-trash" @click="removeComponent"   />
      </div>

    </div>

      <div class="row">
        <div class="col-2" style="margin-top:20px">
          <p>Insert the Answers:</p>
        </div>
        <div class="col-2" v-for="(x,index) in inputs" :key="index" style="display:inline-flex" >
         <q-input outlined v-model="text[index]"    />
           <q-icon class="icon minus" name="fa-solid fa-minus" @click="deleteAnswers(index)"  />
          
        </div>
        <div class="col-1">
       <q-icon class="icon plus" name="fa-solid fa-plus" @click="addmoreAnswers"  />
        </div>
        <div class="col-1" style="margin-top:15px">
       
        </div>

      </div>
      <div class="row">
      <div class="col-2" style="margin-top:60px"> Range:</div>
      <div class="col-7" style="margin-top:30px">
      <q-select v-model="selectedRange"  :options="range" />
      </div>
        <div class="col-2">

      </div>
      <div class="col-1" style="margin-top:120px">
    <q-icon class="icon" name="fa-solid fa-check" @click="sendtoParents" />
      </div>
      </div>
    </div>

</template>

<script>

import { ref } from 'vue'
export default {
  name: "Likert Component.vue",
  props: {
    btnclick: {
      type: Function
    },
    btnclick2: {
      type: Function
    },
    list: {
      type: Array
    },
    remover:{
      type:String
    }
  },
  data(){
    return{
      selectedRange: ref(null),
      range: [
        '0-5', '0-10', '0-15', '0-20', '0-25'
      ],
      question:'',
      show:true,
     text: ref([]),
     inputs:[1]

    }
  },
  methods:{
      sendtoParents(){
      this.$emit("data",this.text);
      this.$emit("data2",this.question);
      this.$emit("data3",this.selectedRange);
     },
     removeComponent(){
      this.list.splice(this.remover,1)
     },
     addmoreAnswers(){

      let lastindex=this.inputs.length;
      this.inputs.push({index:lastindex+1});
     },
     deleteAnswers(index){

       //let answer=this.inputs.index;
       this.inputs.splice(index,1);
       this.text.splice(index,1);
     
      }


  }
}
</script>

<style scoped>
.box{
border: 1px solid black;
margin-top: 10px;
padding: 10px;
}
.icon{
  font-size: 25px;
}
.icon:hover{
  color:blue
}
.minus{
  margin-top: 15px;
  margin-left: 20px;
  margin-right:10px
}
.plus{
  margin-top: 15px;
  margin-left: 20px;
  
}
</style>
