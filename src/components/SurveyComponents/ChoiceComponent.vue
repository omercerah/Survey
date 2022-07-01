<template>
 
    <div class="box"  >

    <div class="row" >
      <div class="col-2" style="padding-top:40px ; margin-bottom: 20px;">
        <p> Insert the Question:</p>
      </div>
      <div class="col-9">
        <q-input  v-model="question" />
      </div>
      <div class="col-1">
     <q-icon class="icon" name="fa-solid fa-angle-up" @click="btnclick(0)" />
       <q-icon class="icon" name="fa-solid fa-angle-down" @click="btnclick2(this.list.length-1)" />
       <q-icon class="icon" name="fa-solid fa-trash"  @click="removeComponent"   />
      </div>
    </div>

      <div class="row">
        <div class="col-3" style="margin-top:20px">
          <p>Insert the Possible answers:</p>
        </div>
        <div class="col-3" v-for="(x,index) in inputs" :key="index" style="margin-right:10px ; display: inline-flex;"  >
          <q-input outlined v-model="text[index]"  />      
        <span> <q-icon class="icon minus" name="fa-solid fa-minus" @click="deleteAnswers(index)"/> </span>
        </div>
        <div class="col-1" style="margin-top:15px" >
         <q-icon class="icon" name="fa-solid fa-plus" @click="addmoreAnswers"   />
        </div>
         <div class="col-4"></div>
      </div>


      <div class="row">
       <div class="col-3" style="margin-top:70px">
         <p>Insert the Type:</p>
       </div>
       <div class="col-3" style="margin-top:50px">
         <q-input outlined v-model="model" />
       </div>
      </div>


       <div class="row">
       <div class="col-3" style="margin-top:70px">
         <p>Multiple:</p>
       </div>
       <div class="col-1" style="margin-top:50px">
         <q-input outlined v-model="model2" />
       </div>
       <div class="col-7"></div>
       <div class="col-1" style="margin-top:45px">
         <q-icon class="icon" name="fa-solid fa-check" @click="sendtoParents"  />
        </div>

      </div>
    </div>

</template>

<script>
import { ref } from 'vue'
export default {
  name: "ChoiceComponent",
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
        question:'',
         text: ref([]),
        model: ref(''),
         model2: ref(''),
        inputs:[]
   
    }
  },
  methods:{
      sendtoParents(){
      this.$emit("data",this.text);
      this.$emit("data2",this.question);
      this.$emit("data3",this.model);
      this.$emit("data4",this.model2);
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
  margin-left: 0px;
}
</style>
