<template>
  <v-app>
    <BarComponent  @child-emit="childClickHandler"/>


    <v-main>
      <DraggableComponent :tables="tables" @draggable-end="dragEndHandler" @rename-click="renameClickHandler" />
      <div>
        {{await_name}}<br>
      </div>


      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import BarComponent from "@/components/BarComponent.vue";
import {ModelManager} from "@/scripts/model/modelManager.js";
import DraggableComponent from "@/components/DraggableComponent.vue";

export default {
  name: 'App',
  components: {
    HelloWorld,
    BarComponent,
    DraggableComponent,
  },
  data: () => ({
    await_name:"hoge",
    tables:[],
    //
  }),
  mounted(){
    const handler = () => {
      console.log( )
    }
    ModelManager.getInstance().load().then(result =>{
      this.await_name = result.data.data.name
      this.tables = result.data.data.tables;
    })
    handler()
  },
  methods:{
    childClickHandler(){
      console.log("child click");
    },
    dragEndHandler(){
      //console.log("dragEndHandler")

    },
    renameClickHandler(data)
    {
      this.tables = data.items;
      let obj = this.tables.find(v => v.id == data.id);
      if(obj)
      {
        obj.name = obj.form;
        obj.form = "";
      }

    }
  }
};
</script>
