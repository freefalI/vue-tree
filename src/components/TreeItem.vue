<template>
    <div class="hello">
        <li>
            <span @contextmenu.prevent="rightClickTreeItem" :class="{selected: item.isSelected,deleted: deleted}">{{ item.name }}</span>
            <button v-show="isFolder" @click="toggle">[{{ item.isOpen ? '-' : '+' }}]</button>
            <button v-show="!isFolder" @click="makeFolder">make folder</button>
            <button v-show="isEmptyFolder" @click="unmakeFolder">unmake folder</button>
            <button v-if="isFolder" @click="makeinner">make inner</button>
            <button @click="deleteItem">delete</button>
            <button v-if="!item.isSelected" @click="selectCurrent">select</button>
            <button v-if="item.isSelected" @click="unselectCurrent">unselect</button>
        </li>
        <ul v-if="item.isOpen">
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
        data: function () {
            return {
                //  isSelected:false,
                deleted: false
            };
        },

        computed: {
            isFolder: function () {
                //return this.item.children.length
//      return Array.isArray(this.item.children) && this.item.children.length
                return Array.isArray(this.item.children) //&& this.item.children.length
                //return this.item.children ===22

            },
            // isFolder:  () => item.children ==false
            //isFolder : () => !!this.item.children
            // isFolder: () => this.item.children !== undefined
            isEmptyFolder: function () {
                return Array.isArray(this.item.children) && this.item.children.length == 0

            }
        },
        methods: {
            toggle: function () {
                if (this.isFolder) {
                    this.item.isOpen = !this.item.isOpen;
                }
            },
            makeFolder: function () {
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
            unmakeFolder: function () {
                console.log('unmakeFolder');
                // this.item.children = [{ name: "test" ,children:null}];
                this.item.children = null;
            },
            makeinner: function () {
                console.log('makeinner');
                this.item.children.push({name: "new item", children: null, isSelected: false,isOpen:false});
                //this.isFolder = true;
            },
            deleteItem: function () {
                //TODO delete children
                this.item.children = null
                // this.item.name= 'deleted'
                this.deleted = true
                //this.$parent.model.children.$remove(this.model)
                // this.$destroy();
            },
            rightClickTreeItem: function () {
                console.log('context')
            },
            selectCurrent: function () {
                console.log(this.item)
                this.item.isSelected = true;
                //  console.log(  this.item)

            },
            unselectCurrent: function () {
                this.item.isSelected = false;
            }

        },
      watch: {
        // myprop: function(newVal, oldVal) { // watch it
        //   console.log('Prop changed: ', newVal, ' | was: ', oldVal)
        // }
      }
    };
</script>


<style>
    .selected {
        color: cornflowerblue;
    }

    .deleted {
        text-decoration: line-through;
        color: red
    }
</style>