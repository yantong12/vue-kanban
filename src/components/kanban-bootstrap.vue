<template>
  <div class="container mt-5">
    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 alert alert-primary">
          <h3>Backlog</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrBacklog"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="ele in arrBacklog"
              :key="ele.name"
            >
              {{ ele.name }}
            </div>
          </draggable>
          <a
            href=""
            @click.prevent="onAddingNewBlock = !onAddingNewBlock"
            v-if="!onAddingNewBlock"
            >+ Add new block</a
          >
          <b-form-input
          v-model="newTask"
          placeholder="Enter Task"
          @keyup.enter="add"
          v-if="onAddingNewBlock"
          @blur="onInputLostfocus()"
        ></b-form-input>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-secondary">
          <h3>In Progress</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrInProgress"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="ele in arrInProgress"
              :key="ele.name"
            >
              {{ ele.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-warning">
          <h3>Tested</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrTested"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="ele in arrTested"
              :key="ele.name"
            >
              {{ ele.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h3>Done</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrDone"
            group="tasks"
          >
            <div class="list-group-item" v-for="ele in arrDone" :key="ele.name">
              {{ ele.name }}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  components: {
    draggable,
  },
  data() {
    return {
      onAddingNewBlock: false,
      newTask: "",
      arrBacklog: [
        { name: "Code Sign Up page" },
        { name: "Test DashBoard" },
        { name: "style Reg" },
        { name: "Help with Designs" },
      ],
      arrInProgress: [],
      arrTested: [],
      arrDone: [],
    };
  },
  methods: {
    onInputLostfocus(){
      this.add();
      this.onAddingNewBlock = false;
    },
    add() {
      if (this.newTask) {
        this.arrBacklog.push({ name: this.newTask });
        this.newTask = "";
        this.onAddingNewBlock = false;
      }
    },
  },
};
</script>

<style scoped>
.kanban-column {
  min-height: 300px;
}
</style>