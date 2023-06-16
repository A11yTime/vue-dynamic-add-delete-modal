<template>
    <base-card>
    <base-button @click="setSelestedTab('stored-resources')" :mode="storedButtonMode"> Stored Resources</base-button>
    <base-button @click="setSelestedTab('add-resource')" :mode="addResButtonMode">Add Resouce</base-button>
    </base-card>
    <keep-alive>
    <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default{
    components: {
       StoredResources,
       AddResource
    },
    data(){
        return{
            selectedTab: 'stored-resources',
            storedResources:[
                {
                    id: 'official guide',
                    title: 'Officeial Guide',
                    description: 'The official vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to google ...',
                    link: 'https://google.com'
                }
            ]
        }
    },
 
    computed: {
        storedButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },
    provide(){
       return{
        resources: this.storedResources,
        addResource: this.addResource,
        deleteResource: this.removeResource
       }
    },
    methods: {
        addResource(title, description, link){
           const newData = {
            id: new Date().toDateString(),
            title: title,
            description: description,
            link: link
           }
           this.storedResources.unshift(newData);
           this.selectedTab = 'stored-resources';
        },
        setSelestedTab(tab){
        this.selectedTab = tab
     },
     removeResource(resId){
        const resIndex = this.storedResources.findIndex((res) => res.id === resId);
        this.storedResources.splice(resIndex, 1)
     }
    }
}
</script>
<style scoped>

</style>