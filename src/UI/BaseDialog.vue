<template>
    <teleport to="body">
        <dialog open>
            <base-card>
                <div class="container">
                    <h2 style="margin-bottom: 10px;">{{ title }}</h2>
                    <p>{{ description }}</p>
                    <div style="width: fit-content; margin-left: auto; margin-top: 20px;">
                        <base-button @click="ok" mode="active">Close</base-button>
                    </div>
                </div>
            </base-card>
        </dialog>
    </teleport>
</template>

<script>
import BaseButton from './BaseButton.vue'
import BaseCard from './BaseCard.vue'
export default {
    props: ['title', 'description'],
    emits: ['ok'],
    components: { BaseCard, BaseButton },
    methods: {
        ok() {
            this.$emit('ok');
        }
    }
}
</script>

<style scoped>
dialog {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border: none;
    /* background-color: transparent; */
    border-radius: 16px;
}

.container {
    background-color: white;
    display: flex;
    flex-direction: column;
    min-width: 400px;
}
</style>