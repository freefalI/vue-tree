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
    { name: "hello" ,'children':null},
    { name: "wat",'children':null },
    {
      name: "child folder",
      children: [
        {
          name: "child folder",
          children: [{ name: "hello" ,'children':null }, { name: "wat" ,'children':null }]
        },
        { name: "hello",'children':null  },
        { name: "wat" ,'children':null },
        {
          name: "child folder",
          children: [{ name: "hello" ,'children':null }, { name: "wat", children:[] }]
        }
      ]
    }
  ]
};
import TreeItem from "./components/TreeItem";
import ControlPanel from "./components/ControlPanel";

export default {
  name: "App",
  components: {
    TreeItem,ControlPanel
  },
  data: function() {
    return {
      msg: "title",
      elems: elems
    };
  },
  computed: {},
  methods: {
  }
};
</script>

