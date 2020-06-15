<template>
  <div class="hello">
    <li  v-if="!deleted">
      <span  @contextmenu.prevent="rightClickTreeItem"   :class="{red: isSelected}">{{ item.name }}</span>
      <button v-show="isFolder"  @click="toggle">[{{ isOpen ? '-' : '+' }}]</button>
      <button v-show="!isFolder" @click="makeFolder">make folder</button>
      <button v-show="isEmptyFolder" @click="unmakeFolder">unmake folder</button>
      <button v-if="isFolder" @click="makeinner">make inner</button>
      <button  @click="delete1">delete</button>
      <button  v-if="!isSelected"  @click="selectCurrent">select</button>
       <button  v-if="isSelected"  @click="unselectCurrent">unselect</button>
    </li>
    <ul  v-if="isOpen">
      <tree-item :key="index" v-for="(child, index) in item.children" :item="child"></tree-item>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TreeItem",
  props: {
    msg: String,
    item: Object
  },
  data: function() {
    return {
      isOpen: false,
      isSelected:false,
      deleted:false
    };
  },

  computed: {
   isFolder: function() {
      //return this.item.children.length
//      return Array.isArray(this.item.children) && this.item.children.length
      return Array.isArray(this.item.children) //&& this.item.children.length
      //return this.item.children ===22

    },
   // isFolder:  () => item.children ==false
    //isFolder : () => !!this.item.children
   // isFolder: () => this.item.children !== undefined
  isEmptyFolder: function() {
      return Array.isArray(this.item.children) && this.item.children.length==0

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
     // this.item.children = [{ name: "test" ,children:null}];
      this.item.children = [];
      //this.item.children =22;
     // console.log(this.item.children);
      this.item.name += 1;
      //this.isOpen = 1;
      //this.isFolder = true;
      //this.item.children=0;
    },
     unmakeFolder: function() {
      console.log('unmakeFolder');
     // this.item.children = [{ name: "test" ,children:null}];
      this.item.children = null;
    },
     makeinner: function() {
      console.log('makeinner');
      this.item.children.push({ name: "new item" ,'children':null });
       //this.isFolder = true;
    },
      delete1: function() {
      console.log('delete');
      this.item.children=null
      this.item.name= 'deleted'
      this.deleted= true
      this.$destroy();
    },
    rightClickTreeItem:function(){
      console.log('context')
    },
    selectCurrent:function(){
      this.isSelected=true;
    },
      unselectCurrent:function(){
       this.isSelected=false;
    }

  }
};
</script>


<style>
.red{
  color:red
}
</style>