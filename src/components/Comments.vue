<template>
    <div class="comments-body">
        <div @click="resetHandler" class="blocker"></div>

        <div class="wrapper">
            <div class="comments-header">
                <div class="think">
                    <h2>Thinking</h2>
                    <span>Seller</span>
                </div>
                <div class="change-button">
                    <button class="btn btn-change">Change Choosing Stage</button>
                </div>
            </div>
            <div class="line"></div>
            <div class="comments-add">
                <div class="add-comment">
                    <input @focus="showButtons" class="form" placeholder="Add comment here" type="text"
                           v-model="commentText">
                </div>
                <div class="comment-control-buttons hide">
                    <button :class="{ disable: !enableSaveButton }" @click="addComment" class="btn btn-save">Save
                    </button>
                    <button @click="cancelComment" class="btn btn-cancel">Cancel</button>
                </div>
            </div>
            <div class="line"></div>
            <div class="comments-view">
                <ul>
                    <li :key="comment.id" v-for="comment in reversedCommentsArr">
                        <Comment :comment="comment" @modal-trigger="triggersHandler"/>

                    </li>
                </ul>
            </div>
        </div>

    </div>
</template>

<script>
    import Comment from "@/components/Comment"

    export default {
        name: "Comments.vue",

        data() {
            return {
                commentText: "",
                commentsArr: [],
                currentUser: "Illia Piliugin",
            }
        },
        components: {
            Comment,
        },
        computed: {
            enableSaveButton() {
                if (this.commentText.length) {
                    return true
                } else {
                    return false
                }
            },
            reversedCommentsArr() {
                const arr = this.commentsArr
                return arr.reverse()
            }
        },

        methods: {

//Close modal window when user press outside modal
            resetHandler() {
                const blocker = document.querySelector(".blocker")
                blocker.style.display = "none"
                document.querySelectorAll(".modal").forEach(modal => modal.style.display = "none")

            },
            //Handler for modal delete/edit buttons
            triggersHandler(task, id) {
                const blocker = document.querySelector(".blocker")
                blocker.style.display = "none"
                // Delete task from array
                if (task === "delete") {
                    this.commentsArr.forEach((el, idx) => {
                        if (el.id === id) {
                            this.commentsArr.splice(idx, 1)
                        }
                    })
                }
                //Edit existing task
                if (task === "edit") {
                    const buttons = document.querySelector(".comment-control-buttons")
                    let commentToEdit = {}
                    this.commentsArr.forEach((comment, idx) => {
                        if (parseInt(comment.id) === id) {
                            commentToEdit = comment
                            this.commentsArr.splice(idx, 1)
                            return 1
                        }
                    })
                    this.commentText = commentToEdit.comment
                    buttons.classList.remove("hide")
                }
            },
            //Show save/cancel buttons when focus on input
            showButtons() {
                const buttons = document.querySelector(".comment-control-buttons")
                buttons.classList.remove("hide")
            },
            //Press cancel button
            cancelComment() {
                const buttons = document.querySelector(".comment-control-buttons")
                this.commentText = ""
                buttons.classList.add("hide")
            },
            //Add new comment to array
            addComment() {
                const buttons = document.querySelector(".comment-control-buttons")
                if (this.commentText !== "") {
                    const comment = {
                        id: Date.now(),
                        comment: this.commentText,
                        date: Date().substr(0, 15),
                        user: this.currentUser
                    }
                    this.commentsArr.push(comment)
                    this.commentText = ""
                    buttons.classList.add("hide")
                } else alert("Please add comment text")
            },

        }
    }
</script>

<style scoped>

    .comments-body {
        background-color: #edfcd2;
        width: 500px;
        min-height: auto;
        border-radius: 5px;
        border-left: 6px solid #61b634;
        /*border-left-color: #4ce82e;*/
        /*border-left-width: 3px;*/
    }

    .blocker {
        display: none;
        opacity: 0.3;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 10;
        height: 100%;
    }

    .wrapper {
        margin: 20px 30px;
    }

    .comments-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .think {
        color: #61b634;
        line-height: 2;
    }

    .comments-add {

    }

    .form {
        width: 100%;
        height: 35px;
        background: none;
        border: none;
        font-size: 18px;
        transition: 0.3s;
    }

    .form:focus {
        outline: none;
        margin: 10px;
        color: #000;
    }

    .comments-view {

    }

    ul {
        list-style: none;
    }

    .line {
        height: 1px;
        background-color: #dcdcdc;
        width: 100%;
        margin-top: 20px;
        margin-bottom: 5px;

    }

    /*    Buttons   */
    .btn {
        border: none;
        border-radius: 3px;
        padding: 10px 15px 10px 15px;
        transition: 0.2s;
        text-decoration: none;
        font-weight: bold;
    }

    .btn-change {
        background-color: #61b634;;
        color: #fff;
    }

    .btn-save {
        background-color: #48cccc;
        color: #ffffff;
        margin-right: 15px;
        border: 1px solid #48cccc;

    }

    .btn-cancel {
        background-color: #ffffff;;
        color: #000;
        border: 1px solid #000;
    }

    .disable {
        background-color: #b7b5b5;
        color: #fff;
        border: 1px solid #b7b5b5;
    }

    .btn:hover {
        cursor: pointer;
    }


</style>