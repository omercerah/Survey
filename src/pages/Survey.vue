<template>
  <q-page>

    <div class="row box">
      <div class="col-3">
        <label> MANYDESIGNS SURVEY</label>
      </div>
      <div class="col-1" style="margin-top:30px">
        <label>NAME:</label>
      </div>
      <div class="col-8">
        <q-input v-model="Name"/>
      </div>
      <q-btn color="primary" label="AddComponent" @click="show"/>
    </div>

    <div v-for="(x ,index) in addedComponents" :key="index">
      <fix-text-component :btnclick="this.moveUpComponent" :btnclick2="this.moveDownComponent" :list="addedComponents" :remover="index" @data="x.text=$event"  v-show="x.selectedComponentType.id == 1"></fix-text-component>
      <input-component :btnclick="this.moveUpComponent" :btnclick2="this.moveDownComponent" :list="addedComponents" :remover="index"  @data="x.question=$event" v-show="x.selectedComponentType.id == 2"></input-component>
      <choice-component :btnclick="this.moveUpComponent" :btnclick2="this.moveDownComponent" :list="addedComponents" :remover="index"   @data="x.text=$event" @data2="x.question=$event" @data3="x.model=$event" @data4="x.model2=$event" v-show="x.selectedComponentType.id == 3"></choice-component>
      <block-component :btnclick="this.moveUpComponent" :btnclick2="this.moveDownComponent" :list="addedComponents" :remover="index"  @data="x.question=$event" v-show="x.selectedComponentType.id == 4"></block-component>
      <likert-component :btnclick="this.moveUpComponent" :btnclick2="this.moveDownComponent" :list="addedComponents" :remover="index"    @data="x.text=$event" @data2="x.question=$event" @data3="x.selectedRange=$event" v-show="x.selectedComponentType.id == 5"></likert-component>
    </div>

    <button @click="moveUpComponent(0)"> Move up first</button>
    <button @click="moveDownComponent(this.addedComponents.length-1)"> Move down last</button>

    


    <q-dialog ref="dialog" >
      <q-card class="q-dialog-plugin">
        <q-toolbar style="width:410px;">
          <q-toolbar-title>What kind of Component do you want?</q-toolbar-title>
        </q-toolbar>

        <q-card-section class="q-pt-none row">
          <q-select square outlined v-model="selectedComponentType" :options="componentTypes" option-value="id"
                    option-label="type" style="width:150px"></q-select>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn
            no-caps
            color="primary"
            rounded
            unelevated
            flat
            label="Cancel"
            @click="onCancelClick"
          />
          <q-btn
            no-caps
            color="primary"
            type="submit"
            @click="addComponent"
            rounded
            unelevated
            label="Save"
          />
        </q-card-actions>
      </q-card>



    </q-dialog>

    <br>


    <code>{{this.addedComponents}}</code>

  </q-page>
</template>


<script>
import {ref} from 'vue'
import InputComponent from 'components/SurveyComponents/InputComponent'
import ChoiceComponent from 'components/SurveyComponents/ChoiceComponent'
import BlockComponent from 'components/SurveyComponents/BlockComponent'
import FixTextComponent from 'components/SurveyComponents/FixTextComponent'
import LikertComponent from 'components/SurveyComponents/LikertComponent'

export default {
  components: {LikertComponent, InputComponent, ChoiceComponent, BlockComponent, FixTextComponent},

  data() {
    return {
      selectedComponentType: ref(null),
      Name: '',
      componentTypes: [

        {
          id: 1, type: 'FixTextComponent'
          
        },
        {
          id: 2, type: 'InputComponent',
            
             
         
        },
        {
          id: 3, type: 'ChoiceComponnet',
          
        },
        {
          id: 4, type: 'BlockComponent'
        },
        {
          id: 5, type: 'LikertComponent'
        }

      ],
      addedComponents: []

    }
  },
  methods: {

    show() {
      this.$refs.dialog.show();
    },
    hide() {
      this.$refs.dialog.hide();
    },

    onCancelClick() {
      this.hide();
    },

    addComponent() {
      this.addedComponents.push({selectedComponentType: this.selectedComponentType});
      this.hide();
    },
    /*
    moveDownComponent(index) {
      if (index > 0) {
        [this.addedComponents[index], this.addedComponents[index - 1]] = [this.addedComponents[index - 1], this.addedComponents[index]]
      }

    },
    moveUpComponent(index){
      if(index<this.addedComponents.length){
        [this.addedComponents[index], this.addedComponents[index+1]]=[this.addedComponents[index+1],this.addedComponents[index]]
      }

    } */

  }
}
</script>


<style scoped>
.box {
  border: 1px solid black;
  margin-top: 10px;
  padding: 10px;
}

.box2 {
  border: 1px solid black;

  margin-top: 10px;
}

.box3 {
  border: 1px solid black;
  margin-top: 10px;
}

.box4 {
  border: 1px solid black;
  margin-top: 30px;
  margin-bottom: 10px;
  margin-left: 15px;
  margin-right: 40px;
  padding: 12px;
}

.icon {
  font-size: 25px;
}
</style>
