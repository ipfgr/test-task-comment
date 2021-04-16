<template>
<div class="blocker" @click="resetHandler"></div>
        <div class="card">
            <div class="comment"><span>{{comment.comment}}</span></div>
            <div class="info">
                <div class="icon">
                    <img src="../assets/noavatar.png" >
                </div>
                <div class="name">
                    <h3>{{comment.user}}</h3>
                </div>
                <div class="date">
                    <h3>{{comment.date}}</h3>
                </div>
                <div @click.stop="modalTrigger" class="modal-open">
                        <img class="arrow-down" src="../assets/drop-down-arrow.svg" >
                    <Modal @modal-trigger="triggersHandler"/>
                </div>
            </div>
        </div>
</template>

<script>
    import Modal from "@/components/Modal"

    export default {
        name: "Comment.vue",
        components:{
          Modal,
        },
        props: {
            comment: Object
        },
        data() {
            return{
            }
        },
        methods:{
             //Close modal window when user press outside modal
            resetHandler(){
                const blocker = document.querySelector(".blocker")
                blocker.style.display = "none"
                const modal = document.querySelector(".modal")
                modal.style.display = "none"

            },
           // Transfer emmit to from modal to parent
           triggersHandler(task){
               if(task === "delete"){
                 this.$emit("modal-trigger","delete",this.comment.id)
               }
               if (task === "edit"){
                   this.$emit("modal-trigger","edit",this.comment.id)
               }
            },
            //Show modal window
            modalTrigger(){
                const blocker = document.querySelector(".blocker")
                blocker.style.display = "block"
                const modal = document.querySelector(".modal")
                modal.style.display = "block"
            },

        }
    }
</script>

<style scoped>
    *{
        line-height: 2;

    }

    .blocker{
            display:none;
            background-color: grey;
            opacity: 0.3;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            z-index: 10;
            height: 100%;
        }

    .card{
    position:relative;
    }
    .comment{
        font-size: 16px;

    }
    .info{
        color: #a5a5a5;
        display:flex;
        align-items: center;
        font-size: 10px;
    }
    .name{
        margin: 0px 5px;
    }
    .icon{

    }
    .icon img{
        width:12px;
        height:12px;
        margin-right:5px;
    }

    .modal-open{
        cursor: pointer;
        padding-left:5px;
    }

    .arrow-down{
        width: 12px;
        height: 12px;
    }


</style>