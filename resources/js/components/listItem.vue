<template>
    <li class="list-group-item d-flex justify-content-between w-100">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
            class="mr-3" style="height:22px;width:22px;margin-top: 7px;"
        />
        <span @click="enableedit" v-if="!edit" key="" :class="[item.completed ? 'completed' : '', 'item']" style="font-size:22px">{{item.name}}</span>
        <input v-if="edit" v-model="item.name" type="text" v-on:keyup.enter="submitform" @keydown.esc="cancelform" style="width:400px">
        <button class="btn btn-danger ml-3" @click="removeItem()">X</button>
    </li>
</template>

<script>
export default {
    props: ["item"],
    data () {
        return {
            edit: false,
            temp: "",
        }
    },
    methods: {
        submitform() {
            this.edit = false
            this.updateCheck()
        },
        cancelform() {
            this.item.name = this.temp
            this.edit = false
        },
        enableedit() {
            this.edit = true
            this.temp = this.item.name
        },
        updateCheck() {
            axios
                .put(`api/item/${this.item.id}`, {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 200) {
                        //this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                });
        },
        removeItem() {
            axios
                .delete(`api/item/${this.item.id}`)
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                });
        }
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}
.item {
    word-break: break-all;
}
</style>