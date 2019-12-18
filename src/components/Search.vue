<template>
    <div style="width: fit-content; margin: 0 auto;">
    <div class="container" >
        <div class="logo">
            <P>Lyrics</P>
            <p>search</p>
        </div>
        
        <v-text-field autofocus="" label="Artist" v-on:click="resetAll()" v-model="sendpara.artist" :rules="inputRules1"></v-text-field>
        <v-text-field label="Track" v-on:click="resetAll()" v-model="sendpara.track" :rules="inputRules2"></v-text-field>
        
        <div id="srch-btn">
            <v-btn class="green white--text"  v-on:click="search()" :loading="this.loading">Search</v-btn>
        </div>

        </div>
        <div class="container" v-if="this.notFound">
        <div class="notFound" >
            <h1>Sorry...</h1>
            <p>we couldn't find the lyric to 
            <span>{{this.sendpara.track}}</span>
            by <span>{{this.sendpara.artist}}</span>
            </p>
            <h2>:(</h2>
        </div>
        </div>

    
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Search",
    props: [],
    data(){
        return {
            artistEr : false,
            trackEr : false,
            notFound : false,
            loading : false,
            inputRules1: [
                v1 => v1.length > 0 || 'Enter Artist' ,
                
            ],inputRules2: [
                v2 => v2.length > 0 || 'Enter track'
            ],
            isData : false,
            sendpara:{
                artist : "",
                track : ""
            },
            recievedata: {}
        }
    },
    methods: {
        resetAll(){
            this.notFound = false;
        },
        checkNotFound(){
            if((this.sendpara.artist.length > 0 || this.sendpara.artist.length > 0) && this.recievedata == ""){
                this.notFound = true
            }
        },

        search(){
            if(this.sendpara.track == "asd"){this.sendpara.track=""}
            this.loading = true
            axios.post('https://sleepy-meadow-93949.herokuapp.com/searchlyric',this.sendpara)
            .then((response)=>{
                this.recievedata = response.data
                this.$emit("myevent", this.recievedata)
                this.loading = false
            }).catch(function (error) {
                console.log(error);
            }).finally(()=>{
                this.checkNotFound()
                this.loading = false
            })
        }
    }
}
</script>

<style scoped>
    div.container{
        padding: 15px;
        margin-top: 10px;
        width: 380px;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        border-radius: 10px;
        background-color: #faebd7b9;
    }
    #srch-btn{
        width: fit-content;
        margin: 0 auto;
    }
    .notFound{
        color: #454545;
    }
    .notFound>p{
        margin-top: -5px;
        line-height: 1.2;
    }
    .notFound{
        margin-top: 20px;
    }
    .notFound>h2{
        margin-top: -15px
    }
    p>span{
        color: #454545;
        font-weight: 700;
    }
    p>span:nth-child(1){
        font-size: 25px;
    }
    p>span:nth-child(2){
        font-weight: 22px 
    }
    h1,h2{
        color: #454545;
    }
    .logo{
        color: #454545;
    }
    .logo>p:nth-child(1){
        font-family: 'Lobster', cursive;
        font-size: 50px;
        width: fit-content;
        margin: 0 auto;
    }
    .logo>p:nth-child(2){
        margin: 0;
        padding: 0;
        font-family: 'Yanone Kaffeesatz', sans-serif;
        font-size: 30px;
        width: fit-content;
        margin: 0 auto;
        margin-top: -15px;
    }
</style>