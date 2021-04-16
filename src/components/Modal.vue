<template>
    <div class="modal" >
        <div @click="editComment" class="edit-modal buttons">Edit comment</div>
        <div @click="deleteComment" class="delete-modal buttons">Delete comment</div>
    </div>

</template>

<script>
    export default {
        name: "Modal.vue",
        props:{
            modalVisible: Boolean,
        },
        methods:{
            editComment(){
            this.$emit("modal-trigger", "edit")
            },
            deleteComment(){
                if(confirm(`Are you sure that's want delete this comment ?`)){
                    this.$emit("modal-trigger", "delete")
                }
            }
        },
        computed: {

        }
    }
</script>

<style scoped>
    .modal {
        z-index:100;
        position: absolute;
        right: 10%;
        display: none;
        flex-direction: column;
        justify-content: center;
        width: 200px;
        height: 100px;
        background-color: #fff;
        border-radius: 5px;
        color: #808080;
    }

    .buttons {
        align-items: center;
        height: 50%;
        display: flex;
        padding-left: 5px;
        transition: all 0.2s
    }

    .buttons:hover {
        background-color: #f1f0f0;
        align-items: center;
        height: 50%;
        display: flex;
        padding-left: 6px;
        cursor: pointer;


    }


</style>