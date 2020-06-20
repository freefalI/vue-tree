<template>
    <div class="document-area" >
        <h2>Edit document</h2>
        <span>Name</span>
        <br>
        <input type="text" name="name" v-model="item.name">
        <br>
        <span>Description</span>
        <br>
        <input type="text" name="description" v-model="item.description">
        <br>
        <span>Content</span>
        <br>
        <textarea name="content" v-model="item.content"></textarea>
        <br>
        <br>
        <button id="save-document">Save</button>
    </div>

</template>

<script>

    export default {
        name: "Document",
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
</style>