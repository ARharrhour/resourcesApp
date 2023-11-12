<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resource')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
</template>
<script>
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';

export default {
  components: { AddResource, StoredResource },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resource' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  data() {
    return {
      selectedTab: 'stored-resource',
      storedResources: [
        {
          id: 'official-guide',
          title: 'official guide',
          description: 'the official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'google',
          description: 'Learn to google',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      storedResources: this.storedResources,
      addResource: this.addResource,
      deleteResources: this.deleteResources,
    };
  },
  methods: {
    setSelectedTab(e) {
      this.selectedTab = e;
    },
    addResource(title, description, link) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        link: link,
        description: description,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resource';
    },
    deleteResources(id) {
      const resources = this.storedResources.findIndex(
        (resource) => resource.id == id
      );
      this.storedResources.splice(resources, 1);
    },
  },
};
</script>
<style></style>
