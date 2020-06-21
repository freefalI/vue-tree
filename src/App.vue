<template>
    <div id="app">
        <div class="sitebar">
            <h1>{{ msg }}</h1>

            <div class="panel">
                <control-panel :item="elems"></control-panel>
            </div>
            <tree-item :item="elems" @edit="startEditing" @unselectAll="unselectAll"></tree-item>
        </div>
        <document :item="document" v-show="editingEnabled" @saveDocument="saveDocument"></document>
    </div>
</template>

<script>
    var document = {name: 'old'};

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
                elems: {},
                document: document,
                editingEnabled: false
            };
        },
        mounted: function () {

            let api = 'http://127.0.0.1/api/tree';
            this.axios.get(api).then((response) => {
                console.log(response.data.data[0])
                this.elems = response.data.data[0]

            })
        },
        computed: {},
        methods: {
            startEditing: function (payload) {
                console.log(payload)
                console.log(3)
                if (payload.id) {
                    let api = 'http://127.0.0.1/api/documents/' + payload.id;
                    this.axios.get(api).then((response) => {
                        this.document = response.data
                    })
                } else {
                    this.document.name = payload.name
                    this.document.description = ''
                    this.document.content = ''
                }
                this.editingEnabled = true
                this.document.isSelected = true
            },
            unselectAll: function () {
                unselectAllHelper(this.elems);
            },
            saveDocument: function (payload) {
                console.log(payload)
                if (payload.id) {
                    let api = 'http://127.0.0.1/api/documents/' + payload.id;
                    this.axios.put(api, payload).then((response) => {
                        console.log(response.data)
                    })
                } else {
                    let api = 'http://127.0.0.1/api/documents';
                    //   payload.parentId = this.$parent.item.id
                    this.axios.post(api, payload).then((response) => {
                        console.log(response.data)
                    })
                }
                //todo refactor this - reload tree structure
                let api = 'http://127.0.0.1/api/tree';
                this.axios.get(api).then((response) => {
                    console.log(response.data.data[0])
                    this.elems = response.data.data[0]

                })
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