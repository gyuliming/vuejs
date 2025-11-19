<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
  },
  data() {
    return {
      todo: [],
      current: 'all',
      editingId: null, // 편집모드인지 아닌지 판단할 속성
    };
  },
  computed: {
    computedTodo() {
      if (this.current === 'all') {
        return this.todo;
      } else {
        return this.todo.filter((v) => v.completed);
      }
    },
  },
  methods: {
    addTodo(inputMsg) {
      const item = {
        id: Math.random(), // todo id를 고유값으로 랜덤하게 저장
        msg: inputMsg, // 할일 텍스트
        completed: false, // 할일 완료 여부
      };
      this.todo.push(item);
    },
    updateTab(tab) {
      this.current = tab;
    },
    editTodo(id) {
      this.editingId = this.editingId === id ? null : id;
    },
    saveTodo(id, newMsg) {
      if (!newMsg || !newMsg.trim()) {
        alert('할 일을 입력해주세요!');
        return;
      }
      this.todo = this.todo.map((v) =>
        v.id === id ? { ...v, msg: newMsg.trim() } : v
      );
      this.editingId = null;
    },
    deleteTodo(id) {
      this.todo = this.todo.filter((v) => v.id !== id);
    },
    updateTodo(id) {
      this.todo = this.todo.map((v) =>
        v.id === id ? { ...v, completed: !v.completed } : v
      );
    },
  },
};
</script>
<template>
  <div class="todo">
    <!-- TodoInput으로부터 전달받은 현재 todo를 TodoHeader에 전달한다 -->
    <TodoHeader :current @update-tab="updateTab" />
    <!-- TodoList 컴포넌트로 computedTodo 데이터를 전달 -->
    <TodoList
      :computed-todo="computedTodo"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
      @edit-todo="editTodo"
    />
    <TodoInput @add-todo="addTodo" />
  </div>
</template>
