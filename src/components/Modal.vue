<template>
    <div class="modal hide">
        <div @click="editComment" class="edit-modal buttons">Edit comment</div>
        <div @click="deleteComment" class="delete-modal buttons">Delete comment</div>
    </div>
</template>

<script>
    export default {
        name: "Modal.vue",
        methods:{
            editComment(){
                console.log("Edit")
            },
            deleteComment(){
                console.log("Delete")
            }
        }
    }
</script>

<style scoped>
    .modal {
        position: absolute;
        right: 10%;
        top: 0;
        display: flex;
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