<template>
  <div>
    <b-card v-if="showEntityCard" no-body style="max-width: 30rem">
      <template #header>
        <h4 class="mb-0">Card Entity</h4>
        <b-button-group class="mx-1">
          <b-button><b-icon icon="plus-lg" /></b-button>
          <b-button><b-icon icon="pencil-square" /></b-button>
          <b-button @click="$emit('hideEntity', false)"
            ><b-icon icon="trash"
          /></b-button>
        </b-button-group>
      </template>

      <b-card-body style="background: aliceblue">
        <div class="container">
          <div class="row">
            <NewTodo @on-addTodo="addTodo($event)" />
          </div>
          <div class="row" v-if="this.todos && this.todos.length">
            <div class="col-12">
              <ul class="list-group">
                <draggable
                  :list="todos"
                  :disabled="!enabled"
                  @start="dragging = true"
                  @end="dragging = false"
                >
                  <CardField
                    v-for="(todo, index) in todos"
                    :key="index"
                    :todoString="todo.fieldName"
                    :completed="todo.completed"
                    :dataType="todo.dataType"
                    @on-delete="deleteTodo(todo)"
                    @on-toggle="toggleTodo(todo)"
                    @on-edit="editTodo(todo, $event)"
                  />
                </draggable>
              </ul>
            </div>
          </div>
        </div>
      </b-card-body>

      <b-card-body> </b-card-body>
    </b-card>
  </div>
</template>

<script>
import CardField from "./CardFields.vue";
import NewTodo from "./NewTodo.vue";
import draggable from "vuedraggable";
import axios from "axios";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "CardEntity",
  components: {
    CardField,
    NewTodo,
    draggable,
  },
  props: {
    showEntityCard: Boolean,
  },
  data() {
    return {
      apiUrl: "http://localhost:3000/fields",
      enabled: true,
      dragging: false,
      todos: [],
    };
  },
  computed: {
    draggingInfo() {
      return this.dragging ? "under drag" : "";
    },
  },
  methods: {
    async addTodo(entity) {
      try {
        await axios
          .post(this.apiUrl, {
            id: uuidv4(),
            fieldName: entity.todo,
            completed: false,
            dataType: entity.option,
          })
          .then((res) => {
            console.log("response", res);
          });
        await this.getCardFields();
      } catch (error) {
        console.log("error", error);
      }
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    async editTodo(todo, newTodoString) {
      todo.fieldName = newTodoString;
      const url = `http://localhost:3000/fields/${todo.id}`;
      try {
        await axios.put(url, {
          fieldName: newTodoString,
          completed: todo.completed,
          dataType: todo.dataType,
        });
        this.getCardFields();
      } catch (error) {
        console.log("error", error);
      }
    },
    async deleteTodo(deleteTodo) {
      const url = `http://localhost:3000/fields/${deleteTodo.id}`;
      try {
        await axios.delete(url).then((res) => {
          if (res) this.getCardFields();
        });
      } catch (error) {
        console.log("error", error);
      }
    },
    async getCardFields() {
      try {
        await axios.get(this.apiUrl).then((response) => {
          this.todos = response.data;
        });
      } catch (error) {
        console.log("error", error);
      }
    },
  },
  created() {
    this.getCardFields();
  },
};
</script>

<style scoped>
.cardEntity {
  background-color: coral;
  color: blanchedalmond;
}
.card-header-nested {
  background: #bdcedbad;
  border-radius: 4px;
  text-align: left;
  width: 30%;
}
.card-header {
  display: flex;
  justify-content: space-between;
}
</style>
