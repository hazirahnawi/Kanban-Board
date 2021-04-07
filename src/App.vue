<template>
  
  <div class="container mt-5">
    <h1 class="text-center f2">~KANBAN BOARD~</h1>

    <!-- <div :style="{ backgroundColor: backgroundcolor }" id="wrapper"> -->
    <div id="h">
    <div class="row mt-5">
      <div class="col form-inline">        
        <b-form-input v-model="newTask" placeholder="Enter Task" @keyup.enter="add"></b-form-input>
        <img src="./image/plus.png" contain height="50px" width="50px" v-on:click="add">
        <draggable v-model="trashZone" class="dropzone trashzone" :options="trashOptions">
            <div slot="footer" class="footer">
          <img src="./image/delete.png" contain height="50px" width="50px">
      </div>
        </draggable>

      </div>
    </div>
    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 alert alert-secondary">
          <h3 class="text-center f1">Backlog</h3>
          <draggable class="list-group kanban-column" :list="arrBackLog" group="tasks">
            <div class="list-group-item" v-for="element in arrBackLog" :key="element.name">
              {{element.name}}
            </div>  
          </draggable>  
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-primary">
          <h3 class="text-center f1">To Do</h3>
          <draggable class="list-group kanban-column" :list="arrToProgress" group="tasks">
            <div class="list-group-item" v-for="element in arrToProgress" :key="element.name">
              {{element.name}}
            </div>  
          </draggable>  
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-warning">
          <h3 class="text-center f1">In Progress</h3>
          <draggable class="list-group kanban-column" :list="arrTested" group="tasks">
            <div class="list-group-item" v-for="element in arrTested" :key="element.name">
              {{element.name}}
            </div>  
          </draggable>  
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h3 class="text-center f1">Done</h3>
          <draggable class="list-group kanban-column" :list="arrDone" group="tasks">
            <div class="list-group-item" v-for="element in arrDone" :key="element.name">
              {{element.name}}
            </div>  
          </draggable>  
        </div>
      </div>
    </div>
  </div>
  </div>
  <!-- </div> -->
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: 'App',
  components: {
    draggable
  },
  data() {
    return{
      newTask: "",
      arrBackLog: [],
      arrToProgress: [],
      arrTested: [],
      arrDone: [],
      trashZone: [],

      trashOptions: {
        group: {
          name: 'trash',
          draggable: '.dropitem',
          put: () => true,
          pull: false
        }
      }

      }
    },
    methods: {
      add() {
        if(this.newTask) {
          this.arrBackLog.push({name: this.newTask});
          this.newTask="";
          }
        }
       } 
}
</script>

<style>
.kanban-column{
  min-height: 300px;
}
@font-face {
  font-family: "Chinchilla";
  src: local("Chinchilla"), 
  url(./fonts/Chinchilla/Chinchilla.ttf) format("truetype");
}

@font-face {
  font-family: "coffee";
  src: local("coffee"), 
  url(./fonts/coffee/coffee.otf) format("opentype");
}

.f1{
  font-family: "coffee", Helvetica, Arial;
  font-size: 50px;
  
}

.f2{
  font-family: "Chinchilla", Helvetica, Arial;
  font-size: 80px;
  color: darkslategray;
}

.dropzone {
  /* border: 1px dotted red; */
  /*margin: .5rem;*/
  min-height: 5vh;
  width: 20%;
  position: absolute; right: 20px;
}

.trashzone .footer {
  display: block;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 170px;
}

#h {
  width: 100%;
  height: 100%;
  /* background-color: rgb(21, 76, 121); */
  background-image: url("~@/image/bg.jpg");
  padding: 3px 30px;
  margin-bottom: 40px;
  border-radius: 10px;
}




</style>
