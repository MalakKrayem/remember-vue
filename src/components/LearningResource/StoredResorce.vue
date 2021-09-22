<template>
  <ul>
    <ResourceItem
      v-for="resource in resources"
      :key="resource.id"
      :id="resource.id"
      :title="resource.title"
      :description="resource.description"
      :link="resource.link"
    ></ResourceItem>
  </ul>
</template>

<script>
import ResourceItem from "@/components/LearningResource/ResourceItem.vue";

export default {
  inject: ["resources"],
  components: {
    ResourceItem,
  },
};
</script>

<style lang="scss" scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
