<template>
    <button @click="action">{{title}}</button>
</template>

<script>
    export default {
        name: "ControlPanelButton",
        props: {
            title: String,
            action: Function,
            item: Object
        },
        data: function () {
            return {};
        },

        computed: {},
        methods: {}
    };
</script>
