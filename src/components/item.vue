<template>
	<div>
		<input type="checkbox" class="toggle" v-model="todo.completed" />
		<label>{{todo.content}}</label>
		<button class="destroy" @click="deleteTodo">删除</button>
		<button @click="printDetails">显示</button>
	</div>
</template>
<script>
export default {
	data() {
		return {
		};
	},
	props: {
		todo: {
			type: Object,
			require: true
    },
	},
	methods: {
		deleteTodo() {
			// 往父组件传递 del 方法，参数为当前id
			this.$emit("del", this.todo.id);
		},
		printDetails() {
			console.log(this.todo.content);
		}
	}
};
</script>

