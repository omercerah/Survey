<template>
  <div class=" box" >
    <div class="row" style="margin-bottom:10px">
    <div class="col-11"> <p>Insert the Text:</p></div>
    <div class="col-1" >
       <q-icon class="icon" name="fa-solid fa-angle-up" @click="moveUpComponent(remover)"   />
       <q-icon class="icon" name="fa-solid fa-angle-down" @click="moveDownComponent(remover)"  />
       <q-icon class="icon" name="fa-solid fa-trash"  @click="removeComponent"  />

    
    </div>
    </div>
   <div class="row">
    <div class="col-11" >
    <div >
    <q-input
      v-model="text"
      filled
      type="textarea"
    />
   </div>
   </div>
   <div class="col self-end" style="margin-left:30px">
     <q-icon class="icon" name="fa-solid fa-check" @click="sendtoParents" />
   </div>
  </div>
  </div>

</template>

<script>

import { ref } from 'vue'

export default {
  name: "FixTextComponent.vue",
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
      text: ref(null)
    }
  },
  methods:{
      sendtoParents(){
      this.$emit("data",this.text);
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
