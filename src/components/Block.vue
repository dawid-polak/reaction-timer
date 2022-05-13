<template>
    <div class="block-all">
        <div class="how-play">
            <p>In 2 second you will see green block. You have to click the block how the fastest. <br>
            Then you will see result</p>
        </div>

        <div v-if="showArea" class="title-area">
            The block will apper in this area
        </div>

        <div class="area">
            <div class="block" v-if="showBlock" @click="stopTimer">
                click me
            </div>
        </div>
    </div>
   
</template>

<script>
    export default {
        props: ['delay'],
        data() {
            return {
                showBlock: false,
                showArea: false,
                timer: null,
                reactionTime: 0
            }
        },
        mounted() {
            setTimeout(() => {
                this.showArea = true;
            }, 500)

            setTimeout(() => {
                this.showBlock = true;
                this.startTimer();
            }, this.delay)
        },
        methods: {
            startTimer() {
                this.timer = setInterval(() => {
                    this.reactionTime += 10;
                }, 10)
            },
            stopTimer() {
                clearInterval(this.timer);
                this.$emit('end', this.reactionTime);
            }
        }
    }

</script>


<style>
    .block-all .how-play {
        margin: 0px 10px 0px 10px;
    }

    .block-all .title-area {
        text-align: left;
        font-size: 10px;
        margin: 10px 0px -11px 20vw;
        color: red;
    }

    .block-all .area {
        margin: 10px auto;
        border: #2c3e50 1px solid;
        width: 60vw;
        height: 60vw;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .block-all .block {
        width: 55vw;
        height: 55vw;
        background-color: #2c3e50;
        border-radius: 10px;
        color: white;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .block-all .block:hover {
        cursor: pointer;
    }

    .block-all .block:active {
        transform: scale(0.95);
    }

    
</style>
