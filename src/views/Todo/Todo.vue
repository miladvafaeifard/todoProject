<template>
  <div class="todo container">
      <div>
        <h1>Vue Todo</h1>
        <div class="input-group mb-3">
          <input type="text"
               class="form-control"
               v-model="inputValue" 
               placeholder="What your mind is saying ...">
          <div class="input-group-append">
            <button type="button" 
                  class="btn btn-primary" 
                  @click="executeAdd()">Add</button>
          </div>
        </div>
      </div>
      <TodoItem v-for="(todo, key, index) in this.todos"
                :key="index" 
                :todo="todo" 
                :deleteHandle="executeDelete"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { State, Action } from 'vuex-class';

import ITodo from '@/model/todo.interface';
import TodoItem from '@/components/TodoItem';

@Component({
  components: {
    TodoItem
  }
})
export default class Todo extends Vue {
  private inputValue = '';
  @Action('Add') Add!: ({ value }: { value: string }) => void; // map this.Add() to this.$store.dispatch('Add');
  @Action('Delete') Delete!: ({ id }: { id: number }) => void; // map this.Add() to this.$store.dispatch('Add');
  @State('todos') todos!: Array<ITodo>;

  executeAdd() {
    this.Add({ value: this.inputValue });
  }

  executeDelete(id: number) {
    this.Delete({ id });
  }
}
</script>

<style scoped lang="scss">
</style>