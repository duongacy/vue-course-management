<template>
    <button :class="mode" :type="type" @click="click">
        <slot></slot>
    </button>
</template>

<script>
export default {
    props: ['mode', 'type'],
    emits: ['click'],
    methods: {
        click() {
            this.$emit('click')
        }
    }
}
</script>

<style scoped>
button {
    padding: 0.75rem 1.5rem;
    font-family: inherit;
    cursor: pointer;
    border: transparent;
    background-color: transparent;
}

button:hover {
    background-color: #edd2ff;
}

button.active {
    background-color: #3a0061;
    border: 1px solid #3a0061;
    color: white;
}

.active:hover {
    background-color: #270041;
    border-color: #270041;
}
</style>