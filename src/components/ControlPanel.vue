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
            item: Object
        },
        data: function () {
            return {
            };
        },
        computed: {
        },
        methods: {
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
