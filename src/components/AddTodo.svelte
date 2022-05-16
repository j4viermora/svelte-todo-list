<script>
import {allTodos} from '../store.js'
let title = ''
let description= ''

function addTodo(){     
  let todos = JSON.parse(window.localStorage.getItem('todo-list')) || []

  console.log(todos)

  let newTodo = {
      id: new Date().getTime() ,
      title,
      description,
      date: new Date().toLocaleString(),
      updatedAt: new Date().toLocaleString(),
      completed: false,  
  }

  todos.unshift(newTodo)
  window.localStorage.setItem('todo-list', JSON.stringify(todos))

  allTodos.update((value) => {
    return [ newTodo, ...value ]
  })


  title = '',
  description = ''
}
</script>



<form on:submit|preventDefault={addTodo} >
    <div class="field">
        <label for="title" class="label">Title</label>
        <input class="input" id='title' type="text" placeholder="Add Title" bind:value={title} required/>
    </div>
    <div class="field">
        <label for="description" class="label">Description</label>
        <textarea class="textarea" placeholder="Description" bind:value={description}></textarea>
    </div>
    <button class="button is-primary" type='submit'>
        Guardar
    </button>
</form>
