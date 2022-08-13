<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" 
        :mode="selectedTab === 'stored-resources' ? null : 'flat'">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')"
        :mode="selectedTab === 'add-resources' ? null : 'flat'">Add Resource</base-button>
    </base-card>
<keep-alive>
    <component :is="selectedTab"></component>
</keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue';

export default{
    components: {
        StoredResources,
        AddResource
    },
  data(){
    return{
        selectedTab: [
            'stored-resources'
            ],
    storedResources: [
                {id: 'official-guide',
                title: 'Official Guide', 
                description: 'Official Vue.js documentation', 
                link: 'https://vuejs.org/' },
                {id: 'google',
                title: 'Google', 
                description: 'How to use Google...', 
                link: 'https://www.google.com/' }
            ]
    }
  },
  methods: {
    setSelectedTab(tab){
        this.selectedTab = tab;
    },
    addResource(title,description,url){
    const newResource = {
      id: new Date().toISOString(),
      title: title,
      description: description,
      link: url
    };
    this.storedResources.push(newResource);
    this.selectedTab = 'stored-resources';
  },
  removeResource(resId){
    //this.storedResources = this.storedResources.filter(
      //(res) => res.id != resId
      //);
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    }
  },
  provide(){
    return {
        resources: this.storedResources,
        addResource: this.addResource,
        deleteResource: this.removeResource
    }
  },
  
  

}
</script>