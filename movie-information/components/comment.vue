<template>
<div style="margin-top:24px">
    <p class="topic">Comment</p>
    <a-row style="margin-top:24px" v-for="(i,index) in comment" :key="index">
        <div v-if="i">
            <a-col :xs="5" :sm="4" :md="2" :lg="2" :xl="2" :xxl="2">
                <div>
                    <img src="~assets/img/profile.png" alt="">
                </div>
            </a-col>
            <a-col :xs="19" :sm="20" :md="22" :lg="22" :xl="22" :xxl="22">
                <div style="margin-left:8px">
                    <p class="comment_topic">comment {{i.count}}</p>
                    <p class="comment_text">{{i.text}}</p>
                </div>
            </a-col>
        </div>
    </a-row>
    <a-row style="margin-top:46px">
        <a-col :xs="5" :sm="4" :md="2" :lg="2" :xl="2" :xxl="2">
            <div>
                <img src="~assets/img/profile.png" alt="">
            </div>
        </a-col>
        <a-col :xs="19" :sm="20" :md="22" :lg="22" :xl="22" :xxl="22">
            <div style="margin-left:8px">
                <textarea type="text" v-model="text"></textarea>
                <button @click="post()">Add Comment</button>
            </div>
        </a-col>
    </a-row>

</div>
</template>

<script>
export default {
    data() {
        return {
            comment: [],
            text: '',
            count: 0
        }
    },
    methods: {
        post() {
            this.count += 1
            this.comment.push({
                text: this.text,
                count: this.count
            })
        }
    }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.topic {
    font-style: normal;
    font-weight: 800;
    font-size: 32px;
    line-height: 38px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #FFFFFF;
}

img {
    width: 48px;
    height: 48px;
    border-radius: 50%;
}

.comment_topic {
    font-style: normal;
    font-weight: bold;
    font-size: 20px;
    line-height: 24px;
    /* identical to box height, or 120% */
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FADB14;

}

.comment_text {
    margin: 16px 0;
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* or 150% */
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: #FFFFFF;
    word-break: break-all;
}

textarea {
    width: 100%;
    height: 142px;
    padding: 8px;
    background: rgba(255, 255, 255, 0.25);
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* or 150% */
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
    border: none;
    resize: none;
}

button {
    margin-top: 24px;
    width: 160px;
    height: 40px;
    background: #FADB14;
    border-radius: 3px;
    box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.25);
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #262626;
    border: none;

}
</style>
