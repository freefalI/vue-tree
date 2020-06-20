<template>
    <div id="app">
        <div class="sitebar">
            <h1>{{ msg }}</h1>

            <div class="panel">
                <control-panel :item="elems"></control-panel>
            </div>
            <tree-item :item="elems" @edit="startEditing" @unselectAll="unselectAll"></tree-item>
        </div>
        <document :item="document" v-show="editingEnabled"></document>
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

    var document = {name:'old'};

    import TreeItem from "./components/TreeItem";
    import ControlPanel from "./components/ControlPanel";
    import Document from "./components/Document";

    const unselectAllHelper = (item) => {
        for (var key in item.children) {
            unselectAllHelper(item.children[key]);
        }
        item.isSelected = false;
    }

    export default {
        name: "App",
        components: {
            TreeItem, ControlPanel, Document
        },
        data: function () {
            return {
                msg: "Application title",
                elems: elems,
                document: document,
                editingEnabled: false
            };
        },
        computed: {},
        methods: {
            startEditing:function (payload) {
                //console.log(payload)
                this.editingEnabled=true
                this.document.isSelected = true
                this.document.name = payload.name
                this.document.description = payload.name + ' description'
                this.document.content = payload.name + ' content'
            },
            unselectAll:function () {
                unselectAllHelper(this.elems);
            }
        }
    };
</script>

<style>
    .sitebar {
        width: 400px;
        float: left;
    }

    .document-area {
        float: left;
    }
</style>