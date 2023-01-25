<template>
    <div id="header">
        <p>ランダムなカードを表示</p>
    </div>
    <div id="content">

        <div id="imgview">
            <div id="showedList">
                <p v-if="isempty">履歴なし</p>
                <div v-for="id in imghistory" @click="historyClick(id)" class="historyblock">
                    <img class="historyimg" v-bind:src="'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/'+list[id]">
                </div>
            </div>
            <button id="b_generate" @click="gen">ここを押そうね☆</button>
            <p v-html="imgnum" id="imgid"></p>
            <img id="card" :src="imgsrc">
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            list: null,
            imgnum: 0,
            imgsrc: "https://dm.takaratomy.co.jp/wp-content/card/cardthumb/dm22sp2-004.jpg",
            imghistory: [],
            isempty: true

        }
    },
    name: "Main.vue",
    created() {
        this.imgel = document.getElementById("card")
        axios.get('https://cardpickrandom.008900011055q3f.repl.co/data/list.json')
            .then(function (response) {
                //デバッグ用にconsoleに出力
                console.log(response.data.imgpath[0])
                this.list = response.data.imgpath
            }.bind(this))
            .catch(function (error) {
                alert('jsonの読み込みに失敗しました。再読み込みとかしてみて')
                console.log(error)
            })
    },
    methods: {
        historyClick: function(id){
            this.genbyid(id)
        },
        gen: function () {
            var random = Math.floor(Math.random() * 15760);
            this.imgnum = random
            this.imghistory.push(random)
            this.isempty = false
            this.imgsrc = 'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/' + this.list[random]
            var box = document.getElementById('showedList')
            box.scrollTo(0, box.scrollHeight);
        },
        genbyid: function (id){
            this.isempty = false
            this.imgsrc = 'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/' + this.list[id]

        }
    }
}


</script>

<style scoped>
body {
    margin: 0;
    padding: 0;
    font-weight: normal;
    font-family: Line_Seed_JP;

}

body.no_scroll {
    overflow: hidden;
}

.historyimg{
    height: 140px;
}

.historyblock {
    min-height: 20px;
    background-color: #e8e8e8;
    margin: 4px;
    border-radius: 3px;
    font-family: Line_Seed_JP;
    font-weight: normal;
}

#showedList {
    width: 30vw;
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(255, 255, 255, 0.47);
    border: solid 1.5px #573fec;
    border-radius: 4px;
    overflow: scroll;

}

#card {
    margin: 0 auto;
    /*width: 90%;
    max-width: 30vw;
    min-width: 300px;*/
    height: 60vh;
}

#header {
    z-index: 20;
    text-align: center;
    border-bottom: solid #000 1px;
    font-family: Line_Seed_JP;
    font-weight: bold;
    font-size: 2em;
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: auto;
    background: rgba(255, 255, 255, 0.47)
}

#content {
    padding: 12vh 0 0 0;
    text-align: center;
    max-height: 100vh;

    /*
    display: flex;
    */
}

#b_generate {
    display: block;
    font-family: Line_Seed_JP;

    margin: 50px auto 20px auto;

    padding: 5px;
    width: 200px;
    font-size: 1.4em;
    background: none;
    border-radius: 10px;
    border: none;

}

#b_generate:hover {
    background: rgba(52, 34, 86, 0.25);
    border: solid 0px;
    margin-top: 50px;
}

#imgview {
    position: relative;
}

.historyblock p {
    margin: 0;
}

#imgid{
    margin: 0;
}

</style>