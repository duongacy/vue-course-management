<template>
    <div style="display: flex; flex-direction: column; gap: 20px;padding: 20px;">
        <base-card>
            <base-button :mode="tabItem === 'resource-list' ? 'active' : ''" @click="selectItem('resource-list')">Stored
                resources</base-button>
            <base-button :mode="tabItem === 'add-resource' ? 'active' : ''" @click="selectItem('add-resource')">Add
                Resource</base-button>
        </base-card>
        <keep-alive>
            <component :is="tabItem" :resources="storedResources"></component>
        </keep-alive>
    </div>
</template>

<script>
import BaseButton from '../../UI/BaseButton.vue'
import BaseCard from '../../UI/BaseCard.vue'
import AddResource from './AddResource.vue'
import ResourceList from './ResourceList.vue'
export default {
    components: { BaseButton, BaseCard, ResourceList, AddResource },
    provide() {
        return {
            remove: this.remove,
            add: this.add,
            update: this.update
        }
    },
    data() {
        return {
            tabItem: 'resource-list',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation.',
                    link: 'https://vuejs.org',
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to google...',
                    link: 'https://google.org',
                },
            ],
        }
    },
    methods: {
        selectItem(item) {
            this.tabItem = item;
        },
        remove(id) {
            const idx = this.storedResources.findIndex(item => item.id === id)
            if (idx === -1) return
            this.storedResources.splice(idx, 1)
        },
        add(itemWithoutId, callback) {
            try {
                const id = new Date().getTime();
                this.storedResources.push({ id, ...itemWithoutId });
                callback?.('success');
            } catch (error) {
                callback?.('fail');
            }
        },
        async update(item, callback) {
            await new Promise(rs => setTimeout(rs, 2000))
            const idx = this.storedResources.findIndex(res => res.id === item.id)
            this.storedResources.splice(idx, 1, item);
            callback?.()
        }
    }
}
</script>