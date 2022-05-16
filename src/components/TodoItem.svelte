<script>
import {allTodos} from '../store'

    export let title;
    export let description;
    export let completed;
    export let id;
    
    let todos;
    allTodos.subscribe((value) => {
        todos = value
    })

    function removeTodo(){
        const todosUpdated = todos.filter(todo => todo.id !== id);
        allTodos.set(todosUpdated)
        window.localStorage.setItem('todo-list', JSON.stringify(todos))
    }

    function changeStatus(){
        allTodos.update(prev => {
            let updated = prev.map(todo => {
                if(todo.id === id){
                    return {
                        ...todo, 
                        completed : !todo.completed
                    }
                }else{
                    return todo
                }
            })
            return [...updated]
        })
        window.localStorage.setItem('todo-list', JSON.stringify(todos))
    }


</script>


<article key class="card mt-2">
    <div class="card-content">
            <div class="is-flex is-justify-content-space-between ">
                <div >
                    <h4 class="title is-5">
                       {title}
                    </h4>
                    <p>
                        {description}
                    </p>
                </div>
                <div class="buttons">
                   <button on:click={removeTodo} class="button is-danger">
                       Eliminar
                   </button>
                   <!-- <button class="button is-warning">
                       Editar
                   </button> -->
                   <button class=" button { completed ? 'is-success' : '' }" on:click={changeStatus}>{completed ? 'Completado' :  'Completar'}</button>
                </div>
            </div>
    </div>
</article>

