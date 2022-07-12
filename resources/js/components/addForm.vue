<template>
    <div class="mt-3">
        <div class="container w-100 " style="position:relative;text-align:left; padding: 7px 20px;background: #f3f3f3;">
            <button class="btn btn-primary" @click="showaddform">Create +</button>
            <input ref="form1" type="test" v-on:keyup.enter="submitform" @keydown.esc="cancelform" placeholder="Enter text.." class="border form1" v-if="shown" v-model="item.name"/>
            <button style="display:none"
                :class="[item.name ? 'active' : 'notactive']"
                @click="addItem()"
            >Add</button>
        </div>
    </div>
</template>
<script>
export default {
    data: function() {
        return {
            shown: false,
            item: {
                name: ""
            }
        };
    },
    methods: {
        submitform() {
            this.addItem()
            this.hideform()
            this.clearform()
        },
        cancelform() {
            this.hideform()
            this.clearform()
        },
        hideform() {
            this.shown = false
        },
        clearform() {
            this.item.name = ''
        },
        showaddform() {
            this.shown = true
        },
        addItem() {
            if (this.item.name == "") {
                return;
            }
            axios
                .post("api/item/store", {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 201) {
                        this.item.name = "";
                        this.$emit("reloadlist");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};
</script>

<style scoped>
.active {
    color: white;
    background-color: blue;
}
.inactive {
    color: gray;
}
.form1 {
    bottom: -50px;
    position: absolute;
    font-size: 22px;
    right: 0;
    left: 0;
    width: 349px;
    box-shadow: 1px 1px 6px #f5d5fb;
    outline: none;
    margin: 0 auto;
    z-index: 5;
}
</style>