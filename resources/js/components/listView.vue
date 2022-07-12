<template>
    <div class="mt-4" style="padding:0px 20px; min-height:400px">
        <ul class="list-group m-auto">
            <list-item
                :item="item"
                v-on:itemchanged="$emit('reloadlist')"
                v-for="item in items"
                :key="item.id"
                class="m-auto my-1 text-justify text-wrap"
                style="border-top-width:1px"
            />
        </ul>
    </div>
</template>

<script>
import listItem from "./listItem";

export default {
    components: {
        listItem
    },
    props: ["items"]
};
</script>

<style scoped></style>