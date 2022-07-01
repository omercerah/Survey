<template>
 
  <div class="box" >
   <div class="row" >
    <div class="col-3" style="padding-top:40px" >
    <p >Insert the Question:</p>
    </div>
    <div class="col-8">
    <q-input v-model="question" />
    </div>
     <div class="col-1">
    <q-icon class="icon" name="fa-solid fa-angle-up" @click="moveUpComponent(remover)"  />
       <q-icon class="icon" name="fa-solid fa-angle-down" @click="moveDownComponent(remover)" />
       <q-icon class="icon" name="fa-solid fa-trash"  @click="removeComponent"   />

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
    
      question:''
    }
  },
  methods:{
      sendtoParents(){
      this.$emit("data",this.question);
     },
     removeComponent(){
      this.list.splice(this.remover,1)
     },
    moveDownComponent(remover) {
      if (remover > 0) {
        [this.list[remover], this.list[remover - 1]] = [this.list[remover - 1], this.list[remover]]
      }

    },
    moveUpComponent(remover){
      if(remover<this.list.length){
        [this.list[remover], this.list[remover+1]]=[this.list[remover+1],this.list[remover]]
      }

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
