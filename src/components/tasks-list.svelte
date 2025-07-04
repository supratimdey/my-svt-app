<script lang="ts">
  import type { Task } from '../task';

  let {
    tasks,
    toggleDone,
  }: {
    tasks: Task[];
    toggleDone: (task: Task) => void;
  } = $props();
</script>

<section>
  {#each tasks as task}
    <article>
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
    </article>
  {/each}
</section>

<style>
  .done {
    text-decoration: line-through;
    text-decoration-color: red;
  }
</style>
