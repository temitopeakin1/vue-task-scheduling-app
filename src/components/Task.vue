<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i
        @click="$emit('delete-task', task.id)"
        class="fa fa-trash"
        aria-hidden="true"
      ></i>
    </h3>
    <p>{{ task.time }}</p>
    <p>{{ task.day }}</p>
    <p>{{ task.reminder }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>

<style scope>
.fa {
  color: #ff0000;
}

.task {
  background: #ffffff;
  margin: 5px;
  padding: 10px 2px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid blue;
}

.task h3 {
  display: flex;
  align-items: left;
  justify-content: space-between;
}
</style>
