<template>
    <div style="display: flex; flex-direction: column; gap: 20px;">
        <resource-item v-for="resource in resources" :resource="resource" :key="resource.id"></resource-item>
    </div>
</template>

<script>
import ResourceItem from './ResourceItem.vue'
export default {
    components: { ResourceItem },
    props: ['resources']
}
</script>
