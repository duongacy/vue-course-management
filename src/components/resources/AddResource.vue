<template>
    <base-card>
        <form @submit.prevent="onSubmit">
            <label for="">Title</label>
            <input type="text" v-model="item.title">
            <label for="">Description</label>
            <input type="text" v-model="item.description">
            <label for="">Link</label>
            <input type="text" v-model="item.link">
            <div style="align-self: flex-start;">
                <base-button mode="active" type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
    <base-dialog v-if="showDialog" title="Something went wrong" description="Please input all required value" @ok="onOk">
    </base-dialog>
</template>
<script>
import BaseButton from '../../UI/BaseButton.vue'
import BaseCard from '../../UI/BaseCard.vue'
import BaseDialog from '../../UI/BaseDialog.vue'
export default {
    components: { BaseCard, BaseButton, BaseDialog },
    inject: ['add'],
    methods: {
        onSubmit() {
            if (this.item.description === '' || this.item.link === '' || this.item.title === '') {
                return this.showDialog = true;
            }
            this.add(this.item, this.onSuccess)
        },
        onSuccess(message) {
            alert("success");
            this.item = {
                title: '',
                description: '',
                link: ''
            }
        },
        onOk() {
            this.showDialog = false;
        }
    },
    data() {
        return {
            item: {
                title: '',
                description: '',
                link: ''
            },
            showDialog: false
        }
    }
}
</script>

<style scoped>
form {
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