<template>
        <div class="card" @click="openModal">
            <div class="comment"><span>{{comment.comment}}</span></div>
                    <Modal/>
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
            openModal(event){
                console.log(`Open modal for event ${event.target.innerHTML}`)

            }
        }
    }
</script>

<style scoped>
    *{
        line-height: 1.6;

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

</style>