<template>
    <div id="header">
        <p>ランダムなカードを表示</p>
    </div>
    <div id="content">

        <div id="imgview">
            <div id="showedListWrapper">
                <p v-if="isempty" id="historytitle">履歴なし</p>
                <p v-if="isempty==false" id="historytitle">履歴</p>
                <div id="showedList">



                    <div v-for="id in imghistory" @click="historyClick(id)" class="historyblock">
                        <p class="historylabel" v-html="'imgid: '+id"></p>
                        <img class="historyimg"
                             v-bind:src="'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/'+list[id]">
                    </div>
                </div>
            </div>
            <button id="b_generate" @click="gen">ここを押そうね☆</button>
            <p v-html="'imgid: '+imgnum" id="imgid"></p>
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
        historyClick: function (id) {
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
        genbyid: function (id) {
            this.isempty = false
            this.imgnum = id
            this.imgsrc = 'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/' + this.list[id]

        }
    }
}


</script>

<style scoped>

#historytitle {
    color:#fff;
    position: absolute;
    top: 0;
    left: 30%;
    right: 30%;
    border-radius: 4px;
    border: solid 2px #000;
    /*
    width: 60px;
    */
    z-index: 19;
    background: rgba(87, 63, 236, 0.68)


}

#showedListWrapper{
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 30vw;
}


body {
    margin: 0;
    padding: 0;
    font-weight: normal;
    font-family: Line_Seed_JP;

}

body.no_scroll {
    overflow: hidden;
}

.historyimg {
    height: 140px;
    padding: 8px;
}

.historylabel {
    position: absolute;
    top: 10px;
    left: 10px;
    background-color: rgba(232, 232, 232, 0.71);
    font-size: 0.8em;
}

.historyblock {
    min-height: 20px;
    background-color: #e8e8e8;
    margin: 7px;
    border-radius: 8px;
    font-family: Line_Seed_JP;
    font-weight: normal;
    border: solid 2px #fff;
    position: relative;

}

.historyblock:hover {
    border: solid 2px #000000;
}


#showedList {
    padding-top: 40px;
    width: 30vw;
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(255, 255, 255, 0.47);
    border: solid 2px #573fec;
    border-radius: 10px;
    overflow-y: scroll;
    overflow-x: hidden;

}

#card {
    margin: 0 auto;
    /*width: 90%;
    max-width: 30vw;
    min-width: 300px;*/
    height: 60vh;
}

#header {
    color: #573fec;
    z-index: 20;
    text-align: center;
    border-bottom: solid #000 1px;
    font-family: Line_Seed_JP;
    font-weight: 900;
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
    font-family: Line_Seed_JP;

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
    transition: .2s
}

#b_generate:hover {
    /*background: #6737FFFF;*/
    border: solid 0px;
    margin-top: 50px;
    text-shadow: #6737FFFF 0px 0 10px;
    transition: .1s;
}

#imgview {
    position: relative;
}

.historyblock p {
    margin: 0;
}

#imgid {
    margin: 0;
}

</style>