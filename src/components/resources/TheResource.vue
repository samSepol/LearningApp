<template>
  <base-card>
    <base-button @click="setSelectedTabs('stored-resource')"
      >Stored Resource</base-button
    >
    <base-button @click="setSelectedTabs('add-resource')"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component v-bind:is="selectedTab"></component>
  </keep-alive>
</template>
<stored-resource :resource="storedResources"></stored-resource>

<script>
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResource,
    AddResource
  },
  data() {
    return {
      selectedTab: 'stored-resource',
      storedResources: [
        {
          id: 'Vue',
          title: 'VueJs Progressive framework',
          description: 'one of the best framework to start with',
          link: 'https://vuejs.org'
        },
        {
          id: 'Node',
          title: 'nodejs Runtime Environment',
          description: 'Runs js outside browser',
          link: 'https://nodejs.org'
        }
      ]
    };
  },
  provide() {
    return {
      resource: this.storedResources,
      AddResource: this.AddResource,
      deleteResources: this.deleteResources
    };
  },
  methods: {
    setSelectedTabs(tab) {
      this.selectedTab = tab;
    },
    AddResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString,
        title: title,
        description: description,
        link: url
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resource';
    },
    deleteResources(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    }
  }
};
</script>
