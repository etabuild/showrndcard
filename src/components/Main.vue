<template>
    <div id="header">
        <p>ランダムなカードを表示</p>
    </div>
    <div id="content">
        <button id="b_generate" @click="gen" >画像表示</button>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data:{
        list: []
    },
    name: "Main.vue",
    created() {
        axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
            .then(function(response){
                //デバッグ用にconsoleに出力
                console.log(response.data.bpi)
                this.bpi = response.data.bpi
            }.bind(this))
            .catch(function(error){
                console.log(error)
            })
    },
    methods: {
        gen: function(){
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

#header {
    text-align: center;
    border-bottom: solid #000 1px;
    font-family: Line_Seed_JP;
    font-weight: bold;
    font-size: 2em;
    margin: 6px;
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: auto;
    background: rgba(255, 255, 255, 0.47)
}

#content {
    padding: 15vh 150px 0 150px;
    text-align: center;
    height: 100vh;
}

#b_generate {
    font-family: Line_Seed_JP;

    margin-top: 50px;
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