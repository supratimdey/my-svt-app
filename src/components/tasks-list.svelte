<script lang="ts">
  import type { Task } from '../task';

  let {
    tasks,
    toggleDone,
    removeTask,
  }: {
    tasks: Task[];
    toggleDone: (task: Task) => void;
    removeTask: (index: number) => void;
  } = $props();
</script>

<section>
  {#each tasks as task, index}
    <article class="task">
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
      <button class="outline" onclick={() => removeTask(index)}> Remove</button>
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
