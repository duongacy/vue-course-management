<template>
    <base-card>
        <div class="root" v-if="!isEditing">
            <div class="left-content">
                <h3>
                    {{ resource.title }}
                </h3>
                <p>{{ resource.description }}</p>
                <a :href="resource.link">Read more...</a>
            </div>
            <base-button @click="turnOnEdit">Edit</base-button>
            <base-button @click="remove(resource.id)">Delete</base-button>
        </div>
        <div v-else>
            <h3 style="margin-bottom: 8px;">Edit</h3>
            <form class="edit" @submit.prevent="onEditSubmit">
                <label for="">Title</label>
                <input type="text" v-model="resourceState.title">
                <label for="">Description</label>
                <input type="text" v-model="resourceState.description">
                <label for="">Link</label>
                <input type="text" v-model="resourceState.link">
                <div style="align-self: flex-start;">
                    <base-button mode="active" :disabled="isLoading" type="submit">
                        {{ isLoading ? 'Updating' : 'Update' }}
                    </base-button>
                </div>
            </form>
        </div>
    </base-card>
</template>

<script>
import BaseButton from '../../UI/BaseButton.vue'
import BaseCard from '../../UI/BaseCard.vue'
export default {
    components: { BaseCard, BaseButton },
    props: {
        resource: {
            id: String,
            title: String,
            description: String,
            link: String
        }
    },
    inject: ['remove', 'update'],
    data() {
        return {
            isEditing: false,
            resourceState: this.resource,
            isLoading: false
        }
    },
    methods: {
        turnOnEdit() {
            this.isEditing = true
        },
        onEditSubmit() {
            this.update(this.resourceState, this.onEditSuccess)
            this.isLoading = true
        },
        onEditSuccess() {
            this.isEditing = false
            this.isLoading = false
        }
    }

}
</script>

<style scoped>
a {
    text-decoration: none;
    color: #ce5c00;
}

a:hover {
    color: #c89300;
}

.root {
    display: flex;
    align-items: flex-start;
}

.left-content {
    flex-grow: 1;
    display: flex;
    gap: 8px;
    flex-direction: column;
}

.edit {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

input {
    height: 30px;
    border: #ccc solid 1px;
    padding-inline: 16px;
}

input:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}
</style>