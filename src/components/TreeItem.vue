<template>
    <div class="hello">
        <li>
            <span @contextmenu.prevent="$refs.menu.open" :class="{selected: item.isSelected,deleted: deleted}">{{ item.name }}</span>
            <button v-show="isFolder" @click="toggle">[{{ item.isOpen ? '-' : '+' }}]</button>

        </li>
        <ul v-if="item.isOpen">
            <tree-item :key="index" v-for="(child, index) in item.children" :item="child"></tree-item>
        </ul>
        <vue-context ref="menu">
            <li v-show="!isFolder">
                <a href="#" @click.prevent="makeFolder">Make folder</a>
            </li>
            <li v-show="isEmptyFolder">
                <a href="#" @click.prevent="unmakeFolder">Unmake folder</a>
            </li>
            <li v-if="isFolder">
                <a href="#" @click.prevent="makeinner">New item</a>
            </li>
            <li>
                <a href="#" @click.prevent="deleteItem">Delete</a>
            </li>
            <li v-if="!item.isSelected">
                <a href="#" @click.prevent="selectCurrent">Select</a>
            </li>
            <li v-if="item.isSelected">
                <a href="#" @click.prevent="unselectCurrent">Unselect</a>
            </li>


        </vue-context>
    </div>
</template>

<script>
    import {VueContext} from 'vue-context';

    export default {
        name: "TreeItem",
        components: {
            VueContext,
        },
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
                this.item.children.push({name: "new item", children: null, isSelected: false, isOpen: false});
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
    @import '~vue-context/dist/css/vue-context.css';

    .selected {
        color: cornflowerblue;
    }

    .deleted {
        text-decoration: line-through;
        color: red
    }
</style>