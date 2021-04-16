<template>
    <div class="card">
        <div class="comment"><span>{{comment.comment}}</span></div>
        <div class="info">
            <div class="icon">
                <img src="../assets/noavatar.png">
            </div>
            <div class="name">
                <h3>{{comment.user}}</h3>
            </div>
            <div class="date">
                <h3>{{comment.date}}</h3>
            </div>
            <div @click.stop="modalTrigger" class="modal-open">
                <img class="arrow-down" src="../assets/drop-down-arrow.svg">
                <div>
                    <div class="modal" ref="modal">
                        <div @click="editComment" class="edit-modal buttons">Edit comment</div>
                        <div @click="deleteComment" class="delete-modal buttons">Delete comment</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    // import Modal from "@/components/Modal"

    export default {
        name: "Comment.vue",
        components: {},
        props: {
            comment: Object
        },
        data() {
            return {
                modalVisible: false
            }
        },
        computed: {},
        methods: {

            editComment() {

                this.$emit("modal-trigger", "edit", this.comment.id)
            },
            deleteComment() {
                if (confirm(`Are you sure that's want delete this comment ?`)) {

                    this.$emit("modal-trigger", "delete", this.comment.id)
                }
            },
            // Transfer emmit to from modal to parent
            triggersHandler(task) {
                if (task === "delete") {
                    this.$emit("modal-trigger", "delete", this.comment.id)
                }
                if (task === "edit") {
                    this.$emit("modal-trigger", "edit", this.comment.id)
                }
            },
            //Show modal window
            modalTrigger() {
                const blocker = document.querySelector(".blocker")
                blocker.style.display = "block"
                this.$refs.modal.style.display = "block"
            },

        }
    }
</script>

<style scoped>
    * {
        line-height: 2;
    }


    .card {
        position: relative;
    }

    .comment {
        font-size: 16px;
    }

    .info {
        color: #a5a5a5;
        display: flex;
        align-items: center;
        font-size: 10px;
    }

    .name {
        margin: 0px 5px;
    }

    .icon img {
        width: 12px;
        height: 12px;
        margin-right: 5px;
    }

    .modal-open {
        cursor: pointer;
        padding-left: 5px;
    }

    .arrow-down {
        width: 12px;
        height: 12px;
    }

    /*  Modal  */
    .modal {
        z-index: 100;
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