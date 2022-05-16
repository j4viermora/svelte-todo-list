<script>
import AddTodo from '../components/AddTodo.svelte'
import TodoItem from '../components/TodoItem.svelte'
import { allTodos } from '../store'


let todos;
allTodos.subscribe(value => {
    todos = value
})



</script>
<section>
<div class="section">
    <h2 class="title">Todo list</h2>
<AddTodo/>
</div>
<div class="section">
    {#each todos as todo }    
    <TodoItem  
     completed={todo.completed} 
     description={todo.description} 
     title={todo.title}
     id={todo.id}
     />
 {/each}
</div>
  
</section>
