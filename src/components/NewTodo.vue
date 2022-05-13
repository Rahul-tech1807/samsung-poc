<template>
  <form
    @submit.prevent="addTodo()"
    style="display: flex; margin-bottom: 11px; justify-content: space-evenly"
  >
    <input
      v-model="newTodo"
      placeholder="+ New Field"
      type="text"
      style="text-align: center"
      class="form-control col-6"
    />
    <b-form-select
      id="inline-form-custom-select-pref"
      class="col-3"
      v-model="selectedOption"
      :options="options"
      :value="null"
    >
      <template #first>
        <b-form-select-option :value="null" disabled
          >-- Please select an option --</b-form-select-option
        >
      </template>
    </b-form-select>
    <b-button type="submit" pill variant="outline-success"
      ><b-icon icon="check" scale="2"
    /></b-button>
  </form>
</template>

<script>
export default {
  name: "NewTodo",
  data() {
    return {
      newTodo: "",
      options: ["String", "Integer", "Complex", "Date"],
      selectedOption: null,
    };
  },
  methods: {
    addTodo() {
      console.log(this.newTodo);
      const entity = {
        option: this.selectedOption,
        todo: this.newTodo,
      };
      if (this.newTodo.length > 1 && this.selectedOption != null) {
        this.$emit("on-addTodo", entity);
        this.newTodo = "";
        this.selectedOption = null;
      } else {
        this.makeToast();
      }
    },
    makeToast() {
      this.$bvToast.toast("Please Enter & Select some value", {
        title: "Error Message",
        variant: "danger",
        solid: true,
      });
    },
  },
};
</script>

<style scoped></style>
