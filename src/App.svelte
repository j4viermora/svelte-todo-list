<script>
	import { onMount } from 'svelte'
	import { allTodos } from './store'
	import TodoList from './pages/TodoList.svelte'

	onMount(()=>{
		const todos = JSON.parse(window.localStorage.getItem('todo-list') ) || []
		allTodos.update((prev) => [...prev, ...todos])
	})
	
</script>
<TodoList/>