<template>

  <main>
    <h1>Create To Do</h1>
    <TodoCreator @create-todo="createTodo"/>

    <ul class="todo-list" v-if="todoList.length > 0" >
      <draggable :list="todoList" item-key="id">
        <template #item="{ element, index}">
          <TodoItem 
            :todo="element" 
            :index="index" 
            @toggle-complete="toggleTodoComplete" 
            @edit-todo="toggleEditTodo"
            @update-todo="updateTodo"
            @delete-todo="deleteTodo"/>
        </template>
      </draggable>
    </ul>

    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" width="22" />
      <span>Add something!</span>
    </p>

    <p v-if="todoCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" width="22" />
      <span>Task Completed!</span>
    </p>
  </main>

</template>

<script setup>

  import TodoCreator from '@/components/Todo/TodoCreator.vue';
  import TodoItem from '@/components/Todo/TodoItem.vue';
  import { Icon } from '@iconify/vue';
  import { uid } from 'uid';
  import { ref, watch, computed } from 'vue';
  import Draggable from 'vuedraggable';

  const todoList = ref([]);

  watch(todoList, () => {
    setTodoListLocalStorage();
  }, {
    deep: true,
  })

  const todoCompleted = computed(() => {
    return todoList.value.every((todo) => todo.isCompleted)
  })

  const fetchTodoList = () => {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if(savedTodoList){
      todoList.value = savedTodoList;
    }
  }

  fetchTodoList();

  const setTodoListLocalStorage = () => {
    localStorage.setItem("todoList", JSON.stringify(todoList.value));
  }
  
  const createTodo = (todo) =>{
    todoList.value.push({
      id: uid,
      todo,
      isCompleted: null,
      isEditing: null,    
    });
  };

  const toggleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
  };
  
  const toggleEditTodo = (todoPos) => {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing
  };

  const updateTodo = (todoVal, todoPos) => {
    todoList.value[todoPos].todo = todoVal;
  }

  const deleteTodo = (index) => {
    todoList.value.splice(index, 1);
  }
  
</script>

<style lang="scss" scoped>


  main{
    display: flex;
    flex-direction: column;
    max-width: 500px;
    width: 100%;
    margin: 0 auto;
    padding: 40px 15px;
    justify-content: center;
    h1{
      margin-bottom: 16px;
      text-align: center;
    }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
    padding: 0;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
  }
</style>