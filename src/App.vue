<template>
  <div id="Card" class="droppable-component" draggable="true" @dragstart="drag">
    Card
  </div>
  <div id="List" class="droppable-component" draggable="true" @dragstart="drag">
    List
  </div>

  <div class="grid-container">
    <div @dragover="allowDrop" @drop="drop">
      <component
        :is="grid[0][0].componentType"
        v-bind="adjustComponent(currentSelection, 0, 0)"
      ></component>
    </div>
    <div @dragover="allowDrop" @drop="drop">
      <component
        :is="grid[0][1].componentType"
        v-bind="adjustComponent(currentSelection, 0, 1)"
      ></component>
    </div>
    <div @dragover="allowDrop" @drop="drop">
      <component
        :is="grid[0][2].componentType"
        v-bind="adjustComponent(currentSelection, 0, 2)"
      ></component>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import List from "./components/List.vue";

export default {
  name: "App",
  components: {
    Card,
    List,
  },
  data() {
    return {
      currentSelection: "",
      grid: [
        [
          { rowPosition: 0, colPosition: 0, componentType: "Card", data: "" },
          { rowPosition: 0, colPosition: 1, componentType: "List", data: "" },
          { rowPosition: 0, colPosition: 2, componentType: "Card", data: "" },
        ],
      ],
    };
  },
  methods: {
    adjustComponent(component, x, y) {
      this.grid[x][y].componentType = component;
    },
    allowDrop(ev) {
      ev.preventDefault();
    },
    drag(ev) {
      ev.dataTransfer.setData("type", ev.target.id);
    },
    drop(ev) {
      ev.preventDefault();
      var data = ev.dataTransfer.getData("type");
      this.currentSelection = data;
    },
    deleteItem(idx) {
      this.element.splice(idx, 1);
    },
  },
};
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-gap: 10px;
  background-color: #f35b21;
  padding: 10px;
  grid-auto-flow: dense;
}

.grid-container > div {
  background-color: rgba(255, 255, 255, 0.8);
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
}

.row-input,
.column-input,
.add-grid {
  margin: 15px;
  margin-bottom: 0px;
  width: 85%;
  border-radius: 10px;
}

h2 {
  text-align: center;
}

.droppable-component {
  /* margin: 15px; */
  margin-bottom: 15px;
  width: 100px;
  height: 30px;
  border-radius: 10px;
  text-align: center;
  line-height: 30px;
  background-color: #333333;
  color: white;
}

#main-drop-container,
#main-drop-container-2 {
  width: 500px;
  height: 250px;
  border: 1px solid #333333;
}
</style>
