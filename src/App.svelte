<script>
	let tasks = [];
	let newTask = '';
  
	function addTask() {
	  if (newTask.trim() !== '') {
		tasks = [...tasks, { text: newTask, completed: false }];
		newTask = '';
	  }
	}
  
	function completeTask(index) {
	  tasks[index].completed = true;
	}
  
	function removeTask(index) {
	  tasks.splice(index, 1);
	}
  
	function toggleTask(index) {
	  if (tasks[index].completed) {
		removeTask(index);
	  } else {
		completeTask(index);
	  }
	}
  </script>
  
  <main>
	<h1>Svelte Task Manager</h1>
	<input type="text" bind:value={newTask} placeholder="Add a new task" />
	<button on:click={addTask}>Add Task</button>
	<ul>
	  {#each tasks as task, index (task.text)}
		<li
		  class:completed={task.completed}
		  on:click={() => toggleTask(index)} 
		  tabindex="0" 
		  role="button" 
		  aria-label={`Task: ${task.text}, ${task.completed ? 'completed' : 'not completed'}`} 
		>
		  {task.text}
		  <button on:click={() => removeTask(index)}>Delete</button>
		</li>
	  {/each}
	</ul>
  </main>
  
  <style>
	main {
	  text-align: center;
	  padding: 1em;
	}
  
	ul {
	  list-style: none;
	  padding: 0;
	}
  
	li {
	  display: flex;
	  justify-content: space-between;
	  align-items: center;
	  padding: 0.5em;
	  border: 1px solid #ccc;
	  margin: 0.5em 0;
	  cursor: pointer;
	}
  
	li.completed {
	  text-decoration: line-through;
	  background-color: #f0f0f0;
	}
  </style>
  