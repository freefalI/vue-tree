<template>
    <div class="panel">
        <control-panel-button :title="'Collapse all'" :action="collapseAll" :item="item"></control-panel-button>
        <control-panel-button :title="'Expand all'" :action="expandAll" :item="item"></control-panel-button>
        <control-panel-button :title="'Delete selected'" :action="deleteSelected" :item="item"></control-panel-button>
    </div>
</template>

<script>
    import ControlPanelButton from "./ControlPanelButton";

    const delSelected = (item) => {
        for (var key in item.children) {
            delSelected(item.children[key]);
        }
        if (item.isSelected) {
            console.log(item.name);
            item.children = [];
        }
    }
    const expandAllHelper = (item) => {
        for (var key in item.children) {
            expandAllHelper(item.children[key]);
        }
        item.isOpen = true;
    }
    const collapseAllHelper = (item) => {
        for (var key in item.children) {
            collapseAllHelper(item.children[key]);
        }
        item.isOpen = false;
    }
    export default {
        name: "ControlPanel",
        components: {
            ControlPanelButton
        },
        props: {
            msg: String,
            item: Object
        },
        data: function () {
            return {
                isOpen: false,
                deleted: false
            };
        },
        computed: {
            isFolder: function () {
                return this.item.children;
            }
        },
        methods: {
            toggle: function () {
                if (this.isFolder) {
                    this.isOpen = !this.isOpen;
                }
            },
            makeFolder: function () {
                console.log("makeFolder");
                console.log(this.item.name);
                this.item.children = [{name: "test", children: []}];
                console.log(this.item.children);
                this.item.name += 1;
                this.isOpen = 1;
                //this.item.children=0;
            },
            makeinner: function () {
                console.log("makeinner");
                this.item.children.push({name: "new item"});
            },
            delete1: function () {
                console.log("delete");
                this.item.children = [];
                this.item.name = "deleted";
                this.deleted = true;
            },
            deleteAll: function () {
                console.log("delete all");
                this.item.children.pop();
            },
            deleteSelected: function () {
                delSelected(this.item);
            },
            collapseAll: function () {
                collapseAllHelper(this.item);
            },
            expandAll: function () {
                expandAllHelper(this.item);
            }
        }
    };
</script>
