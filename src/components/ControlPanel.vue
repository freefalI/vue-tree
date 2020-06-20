<template>
  <div class="panel">
    <control-panel-button :title="'button1'" :action="deleteAll" :item="item"></control-panel-button>
    <control-panel-button :title="'Delete selected'" :action="deleteSelected" :item="item"></control-panel-button>
  </div>
</template>

<script>
import ControlPanelButton from "./ControlPanelButton";
function delSelected(item) {

  // item.$refs.children.forEach(col => {
  //     // Do something with `col`
  //     console.log(col)
  //   })


  // console.log(item);
  //
  // console.log(item.children);
  // console.log(item.isSelected);
  for (var key in item.children) {
    // console.log(item.children[key]);
    delSelected(item.children[key]);
  }
  if (item.isSelected) {
    console.log(item.name);
    item.children = [];
  }
}
/*
const toggleTreeClosed = (rootNode: NodeType) => {
  rootNode.showChildren = false;
  rootNode.children.forEach(child => toggleTreeClosed(child));
};*/

export default {
  name: "ControlPanel",
  components: {
    ControlPanelButton
  },
  props: {
    msg: String,
    item: Object
  },
  data: function() {
    return {
      isOpen: false,
      deleted: false
    };
  },

  computed: {
    isFolder: function() {
      return this.item.children;
    }
  },
  methods: {
    toggle: function() {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
    },
    makeFolder: function() {
      console.log("makeFolder");
      console.log(this.item.name);
      this.item.children = [{ name: "test", children: [] }];
      console.log(this.item.children);
      this.item.name += 1;
      this.isOpen = 1;
      //this.item.children=0;
    },
    makeinner: function() {
      console.log("makeinner");
      this.item.children.push({ name: "new item" });
    },
    delete1: function() {
      console.log("delete");
      this.item.children = [];
      this.item.name = "deleted";
      this.deleted = true;
    },
    deleteAll: function() {
      console.log("delete all");
      this.item.children.pop();
    },
    deleteSelected: function() {
      //this.item.children.pop()
      //array_walk_recursive
      delSelected(this.item);
    }
  }
};
</script>
