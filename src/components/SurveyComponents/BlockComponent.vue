<template>
 
  <div class="box" >
   <div class="row" >
    <div class="col-2" style="padding-top:40px" >
    <p >Block Name:</p>
    </div>
    <div class="col-9">
    <q-input v-model="question" />
    </div>
     <div class="col-1">
    <q-icon class="icon" name="fa-solid fa-angle-up" @click="btnclick(0)"  />
       <q-icon class="icon" name="fa-solid fa-angle-down" @click="btnclick2(this.list.length-1)" />
       <q-icon class="icon" name="fa-solid fa-trash" @click="removeComponent"  />
    </div>
  </div>
  <div class="row">
    <div class="col-11"></div>
    <div class="col-1">
      <q-icon class="icon" name="fa-solid fa-check" @click="sendtoParents" />
    </div>
  </div>
  </div>
 
</template>

<script>
export default {
  name: "InputComponent.vue",
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
      show:true,
      question:''
    }
  },
  methods:{
      sendtoParents(){
      this.$emit("data",this.question);
     },
     removeComponent(){
      this.list.splice(this.remover,1)
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
</style>
