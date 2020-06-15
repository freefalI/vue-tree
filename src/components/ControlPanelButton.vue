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
  data: function() {
    return {
      isOpen: false,
      deleted:false
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
       console.log('makeFolder');
      console.log(this.item.name);
      this.item.children = [{ name: "test" ,children:[]}];
      console.log(this.item.children);
      this.item.name += 1;
      this.isOpen = 1;
      //this.item.children=0;
    },
     makeinner: function() {
      console.log('makeinner');
      this.item.children.push({ name: "new item" });
    },
      delete1: function() {
      console.log('delete');
      this.item.children=[]
      this.item.name= 'deleted'
      this.deleted= true
    }
  }
};
</script>
