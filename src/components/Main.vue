<template>
    <div id="header">
        <p>ランダムなカードを表示</p>
    </div>
    <div id="content">
        <button id="b_generate" @click="gen">画像表示</button>
        <img id="card" src="https://dm.takaratomy.co.jp/wp-content/card/cardthumb/dm22sp2-004.jpg">
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            list: null
        }
    },
    name: "Main.vue",
    created() {
        axios.get('https://cardpickrandom.008900011055q3f.repl.co/data/list.json')
            .then(function (response) {
                //デバッグ用にconsoleに出力
                console.log(response.data.imgpath[0])
                this.list = response.data.imgpath
            }.bind(this))
            .catch(function (error) {
                console.log(error)
            })
    },
    methods: {
        gen: function () {
            var random = Math.floor( Math.random() * 15760 );
            var el = document.getElementById("card")
            el.setAttribute("src", 'https://dm.takaratomy.co.jp/wp-content/card/cardthumb/'+this.list[random]);
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

#card {
    margin: 0 auto;
    width:100%;
    max-width: 30vw;
    min-width: 300px;
}

#header {
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
    padding: 15vh 0 0 0;
    text-align: center;
    height: 100vh;
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


</style>