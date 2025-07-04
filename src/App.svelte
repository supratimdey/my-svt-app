<script lang="ts">
  import TasksForm from './components/tasks-form.svelte';
  import TasksList from './components/tasks-list.svelte';
  import type { Task } from './task';

  let tasks = $state<Task[]>([]);

  let message = 'Tasks App';

  let totalDone = $derived(
    tasks.reduce((total, task) => total + Number(task.done), 0)
  );

  function addTask(newTask: string) {
    console.log(newTask);
    tasks.push({
      id: crypto.randomUUID(),
      title: newTask,
      done: false,
    });
  }

  function toggleDone(task: Task) {
    task.done = !task.done;
  }
</script>

<main>
  <div>
    <h1>{message}</h1>
    <TasksForm {addTask} />
    <p>{totalDone} / {tasks.length} Tasks done</p>
    <TasksList {tasks} {toggleDone} />
  </div>
</main>

<style>
  main {
    margin: 1rem auto;
    max-width: 80%;
  }
</style>
