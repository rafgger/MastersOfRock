<template>
  <div class="home">

    <list-tasks
      v-if="$store.state.tasks.length"
    />

    <no-tasks
      v-else
    />

    <button-done-sorting
      v-if="$store.state.sorting"
    />

  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {
    'list-tasks': require('@/components/BucketList/ListTasks.vue').default,
    'no-tasks': require('@/components/BucketList/NoTasks.vue').default,
    'button-done-sorting': require('@/components/BucketList/ButtonDoneSorting.vue').default
  }
}
</script>