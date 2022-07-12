<template>
    <div class="container w-50 m-auto m-2 text-left pt-3" style="background:white;padding: 0;">
        <div style="padding:0px 20px">
            <div>Todo CRUD <a href="/logout">(Logout)</a></div>
        </div>
        <add-form v-on:reloadlist="getItems()" />
        <list-view v-if="!empty"
            :items="items"
            v-on:reloadlist="getItems()"
            class="text-center"
        />
        <div v-if="empty" style="padding:0px 20px; min-height:400px; text-align:center; font-weight:bold; size:24px">{{text}}</div>
    </div>
</template>

<script>
import addForm from "./addForm";
import listView from "./listView";

export default {
    components: {
        addForm,
        listView
    },

    data () {
        return {
            loading: false,
            text: "",
            empty: false,
            items: []
        };
    },
    methods: {
        getItems() {
            this.empty = true
            this.text = "Loading data..."
            axios.get("api/items")
                .then(res => {
                    this.items = res.data;
                    if(this.items.length === 0 ) {
                        this.empty = true
                        this.text = "Empty. Go create one..."
                    } else {
                        this.empty = false
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    },
    created() {
        this.getItems();
    }
};
</script>

<style>
body{
    background: #c9abf9;
}
</style>
