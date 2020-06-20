<template>
    <div id="app">
        <h1>{{ msg }}</h1>

        <div class="panel">
            <control-panel :item="elems"></control-panel>
        </div>
        <tree-item :item="elems"></tree-item>
    </div>
</template>

<script>
    var elems = {
        name: "root",
        children: [
            {name: "hello", children: null, isSelected: false, isOpen: false},
            {name: "wat", children: null, isSelected: false, isOpen: false},
            {
                name: "child folder",
                isSelected: false,
                isOpen: false,
                children: [
                    {
                        name: "child folder2",
                        isSelected: false,
                        isOpen: false,
                        children: [{name: "hello4", children: null, isSelected: false, isOpen: false}, {
                            name: "wat",
                            children: null,
                            isSelected: false,
                            isOpen: false
                        }]
                    },
                    {name: "hello5", children: null, isSelected: false, isOpen: false},
                    {name: "wat4", children: null, isSelected: false, isOpen: false},
                    {
                        name: "child folder3",
                        isSelected: false,
                        isOpen: false,
                        children: [{name: "hello6", children: null, isSelected: false, isOpen: false}, {
                            name: "wat43",
                            children: [],
                            isSelected: false,
                            isOpen: false

                        }]
                    }
                ]
            }
        ],
        isSelected: false,
        isOpen: true
    };
    import TreeItem from "./components/TreeItem";
    import ControlPanel from "./components/ControlPanel";

    export default {
        name: "App",
        components: {
            TreeItem, ControlPanel,
        },
        data: function () {
            return {
                msg: "title",
                elems: elems
            };
        },
        computed: {},
        methods: {}
    };
</script>

<style>
</style>