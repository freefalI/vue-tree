<template>
    <div class="document-area">
        <h2>Edit document</h2>
        <span>Name</span>
        <br>
        <input type="text" name="name" v-model="item.name">
        <br>
        <span>Description</span>
        <br>
        <input type="text" name="description" v-model="item.description">
        <br>
        <span>Content</span>
        <br>
        <textarea name="content" v-model="item.content"></textarea>
        <br>
        <br>
        <button id="save-document">Save</button>
    </div>

</template>

<script>

    export default {
        name: "Document",
        props: {
            msg: String,
            item: Object
        },
        data: function () {
            return {};
        },

        computed: {},
        methods: {},
        watch: {}
    };
</script>


<style>
</style>