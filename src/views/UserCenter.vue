<template>
	<section class="real-app">
		<input
			type="text"
			class="add-input"
			autofocus="autofocus"
			placeholder="接下来要做什么?"
			@keyup.enter="addTodo"
		/>
		<a-time-picker @change="onChange" />
		<item :todo="todo"  v-for="todo in todos" :key="todo.id" @del="deleteTodo"></item>
		<tabs
			:filter="filters"
			:todos="todos"
			@toggle="toggleFilter"
			@clearAllCompleted="clearAllCompleted"
		></tabs>
	</section>
</template>

<script >
import Item from "../components/item";
import Tabs from "../components/tabs";

let id = 0;
export default {
	data() {
		return {
			todos: [],
			filters: "all",
      endTime: "2019-8-6 11:49:00",
      time:'1'
		};
	},
	components: {
		Item,
		Tabs
	},
	computed: {
		filteredTodos() {
			if (this.filters === "all") {
				return this.todos;
			}
			const completed = this.filter === "completed";
			return this.todos.filter(todo => completed === todo.completed);
		}
	},
	methods: {
		onChange(time, timeString) {
      this.time = "2019-8-5 " + timeString;
		},
		addTodo(e) {
			this.todos.unshift({
				id: id++,
				content: e.target.value.trim(),
        completed: false,
        time : e.endTime
			});
      e.target.value = "";
      console.log(this.todos)
		},
		deleteTodo(id) {
			this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1);
		},
		toggleFilter() {
			this.filter = state;
		},
		clearAllCompleted() {
			this.todos = this.todos.filter(todo => !todo.completed);
		}
	}
};
</script>