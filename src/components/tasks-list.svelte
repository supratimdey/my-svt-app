<script lang="ts">
  import type { Task } from '../task';
  import { fade } from 'svelte/transition';

  let {
    tasks,
    toggleDone,
    removeTask,
  }: {
    tasks: Task[];
    toggleDone: (task: Task) => void;
    removeTask: (id: string) => void;
  } = $props();
</script>

<section>
  {#each tasks as task}
    <article class="task" transition:fade>
      <lable>
        <input
          checked={task.done}
          onchange={() => toggleDone(task)}
          type="checkbox"
        />
        <span class:done={task.done}>
          {task.title}
        </span>
      </lable>
      <button class="outline" onclick={() => removeTask(task.id)}>
        Remove</button
      >
    </article>
  {/each}
</section>

<style>
  .task {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .done {
    text-decoration: line-through;
    text-decoration-color: red;
  }
</style>
