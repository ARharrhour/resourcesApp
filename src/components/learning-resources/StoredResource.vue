<template>
  <ul>
    <learning-resource
      v-for="resource in storedResources"
      :key="resource.id"
      :id="resource.id"
      :title="resource.title"
      :link="resource.link"
      :description="resource.description"
    ></learning-resource>
  </ul>
</template>
<script>
import LearningResource from './LearningResource.vue';

export default {
  inject: ['storedResources'],
  components: { LearningResource },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
