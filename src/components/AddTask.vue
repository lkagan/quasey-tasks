<template>
  <q-card>

    <ModalHeader>Add Task</ModalHeader>

    <q-form @submit.prevent="submitForm">
      <q-card-section class="q-pt-none">
        <NameInput :task="taskToSubmit"></NameInput>
        <DateInput :task="taskToSubmit"></DateInput>
      </q-card-section>

      <q-card-actions align="right">
        <q-btn
          label="Save"
          color="primary"
          type="submit"
        />
      </q-card-actions>
    </q-form>
  </q-card>
</template>

<script>
  import {mapMutations} from 'vuex';
  import ModalHeader from "components/Modal/Header";
  import NameInput from "components/Modal/NameInput";
  import DateInput from "components/Modal/DateInput";

  export default {
    name: "AddTask",
    components: {DateInput, NameInput, ModalHeader},
    data() {
      return {
        taskToSubmit: {name: '', complete: false, date: ''},
      }
    },

    methods: {
      ...mapMutations('tasks', ['addTask']),

      submitForm() {
        this.addTask(this.taskToSubmit);
        this.$emit('close');
      }
    }
  }
</script>

<style scoped>

</style>
