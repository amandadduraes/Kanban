<template>
  <div id="app">
    <h1>Kanban</h1>
    <hr />
    <Form v-on:saveTask="save"></Form>
    <div class="lists">

      <Stage v-for="stage in stages" :key="stage.id" 
        :tasks= "tasks"
        :stage= "stage.id"
        :title="stage.title"
        :bgColor="stage.bgColor"
        :nextStage= "stage.nextStage"
        @removeTask= "removeTask"
        @moveStage= "moveToNextStage"
        >
        
      </Stage>
    </div>
  </div>
</template>

<script>
import Form from "./Form.vue";
import Stage from './Stage.vue';
export default {
  components: {
    Form, Stage
  },
 
  data() {
    return {
      tasks: [],
      stages: [
        {
          id: 'toDo',
          title: 'To Do',
          nextStage: 'inProgress',
          bgColor: '#ff6961 '
        },
        {
          id: 'inProgress',
          title: 'In Progress',
          nextStage: 'done',
          bgColor: '#ffffe0'
        },
        {
          id: 'done',
          title: 'Done',
          nextStage: null,
          bgColor: '#9fe855'
        },
      ],
    };
  },
  methods: {
    save(task) {
      this.tasks.push({ text: task, stage: 'toDo' })
    },
    moveToNextStage(task,stage) {
      task.stage = stage;
    },
    removeTask(task) {
      const index = this.tasks.indexOf(task);
      this.tasks.splice(index, 1);
    },
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: #f7f7f7;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: crimson;
}

#app {
  width: 100vw;
  height: calc(100vh-20px);
  max-width: 960px;
  padding: 20px 10px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.lists {
  display: flex;
  justify-content: space-between;
  height: 100%;
}

#toDo {
  background-color: #ffaaaa;
}

#inProgress {
  background-color: #fff9aa;
}

#done {
  background-color: #aaffb8;
}

hr {
  margin-bottom: 10px;
  border: 1px solid lightpink;
}

h1 {
  text-align: center;
}

.list {
  min-width: 31%;
  margin: 0 1%;
  padding: 10px;
  background-color: #f0f0f0;
  border-radius: 3px;
  overflow-y: auto;
}

.list:first-child {
  margin-left: 0;
}

.list:last-child {
  margin-right: 0;
}

.to-do-list ol {
  list-style-type: decimal;
  list-style-position: inside;
  padding: 0;
  margin: 0;
}

.to-do-list ol li {
  padding: 5px;
  margin-top: 5px;
  border: 1px solid crimson;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.2x);
  display: flex;
  justify-content: space-between;
}

.to-do-list ol li .text {
  max-width: calc(100% - 60px);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.to-do-list ol li .text.completed {
  text-decoration: line-through;
}

.to-do-list ol li .actions {
  width: 45px;
  display: flex;
  vertical-align: middle;
  height: 100%;
  justify-content: flex-end;
}

.to-do-list ol li .actions button {
  width: 20px;
  padding: 2px;
  height: 20px;
  line-height: 15px;
  border-radius: 10px;
  font-size: 11px;
  border: 1px solid #ffaaaa;
  background-color: transparent;
  cursor: pointer;
}

.to-do-list ol li .actions button.next {
  color: #229966;
  border: 1px solid #229966;
  margin-left: 5px;

}

.to-do-list ol li .actions button.remove {
  border: 1px solid #992222;
  cursor: pointer;
}
</style>