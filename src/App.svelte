<script lang="ts">
  import TasksForm from './components/tasks-form.svelte';
  import TasksList from './components/tasks-list.svelte';
  import type { Task } from './task';
  import type { Filter } from './filterTypes';

  let tasks = $state<Task[]>([]);

  let message = 'Tasks App';
  let currentFilter = $state<Filter>('all');
  let totalDone = $derived(
    tasks.reduce((total, task) => total + Number(task.done), 0)
  );

  let filterdTasks = $derived.by(() => {
    switch (currentFilter) {
      case 'all': {
        return tasks;
      }
      case 'done': {
        return tasks.filter((task) => task.done);
      }
      case 'todo': {
        return tasks.filter((task) => !task.done);
      }
    }
    return tasks;
  });

  function addTask(newTask: string) {
    console.log(newTask);
    tasks.push({
      id: crypto.randomUUID(),
      title: newTask,
      done: false,
    });
  }

  function removeTask(id: string) {
    const index = tasks.findIndex((task) => task.id === id);

    tasks.splice(index, 1);
  }

  function toggleDone(task: Task) {
    task.done = !task.done;
  }
</script>

{#snippet filterButton(filter: Filter)}
  <button
    onclick={() => (currentFilter = filter)}
    class="secondary filteredButton"
    class:contrast={currentFilter === filter}
    >{filter}
  </button>
{/snippet}
<main>
  <div>
    <h1>{message}</h1>
    <TasksForm {addTask} />
    {#if tasks.length}
      <p>{totalDone} / {tasks.length} Tasks done</p>
    {:else}
      <p>Add some taska to get started</p>
    {/if}

    {#if tasks.length}
      <div class="button-container">
        {@render filterButton('all')}
        {@render filterButton('todo')}
        {@render filterButton('done')}
        <!-- <button -->
        <!--   onclick={() => (currentFilter = 'all')} -->
        <!--   class="secondary" -->
        <!--   class:contrast={currentFilter === 'all'} -->
        <!--   >All -->
        <!-- </button> -->
        <!-- <button -->
        <!--   onclick={() => (currentFilter = 'todo')} -->
        <!--   class:contrast={currentFilter === 'todo'} -->
        <!--   class="secondary" -->
        <!--   >Todo -->
        <!-- </button> -->
        <!-- <button -->
        <!--   onclick={() => (currentFilter = 'done')} -->
        <!--   class:contrast={currentFilter === 'done'} -->
        <!--   class="secondary" -->
        <!--   >Done -->
        <!-- </button> -->
      </div>
    {/if}
    <TasksList tasks={filterdTasks} {toggleDone} {removeTask} />
  </div>
</main>

<style>
  main {
    margin: 1rem auto;
    max-width: 80%;
  }
  .button-container {
    display: flex;
    justify-content: end;
    margin-bottom: 1rem;
    gap: 0.5rem;
  }
  .filteredButton {
    text-transform: capitalize;
  }
</style>
