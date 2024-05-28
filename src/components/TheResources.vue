<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Store</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
        <keep-alive>
        <component :is="selectedTab"></component>
        </keep-alive>
    </base-card>
</template>

<script>
    import StoredResources from './StoredResources.vue';
    import AddResource from './AddResource.vue';
    export default {
        components: {
            StoredResources,
            AddResource
        },
        data() {
            return {
                selectedTab: 'stored-resources',
                storedResource : [
                    {
                        id: 'official-guide',
                        title: ' Official Guide',
                        description: 'The offical Vue.js documentation',
                        link: 'https://vuejs.org'
                    },
                    {
                        id: 'google',
                        title: ' Google',
                        description: 'Learn to google...',
                        link: 'https://google.com'
                    },
                ]
            }
        },
        provide() {
            return {
                resources: this.storedResource,
                addResource: this.addResource,
                removeResource:this.removeResource,
            }
        },
        computed: {
            storedResButtonMode() {
                return this.selectedTab === 'stored-resources' ? null : 'flat';
            },
            addResButtonMode() {
                return this.selectedTab === 'add-resource' ? null : 'flat';
            }
        },
        methods: {
            setSelectedTab(value) {
                this.selectedTab = value;
            },

            addResource(title, description, link) {
                const newResource = {
                    id: new Date().toISOString(),
                    title: title,
                    description:description,
                    link: link
                };

                this.storedResource.unshift(newResource);
                this.selectedTab = 'stored-resources';
            },
            removeResource(resId) {
                const resIndex = this.storedResource.findIndex(res => res.id === resId);
                this.storedResource.splice(resIndex, 1);
            }
        }
    }
</script>