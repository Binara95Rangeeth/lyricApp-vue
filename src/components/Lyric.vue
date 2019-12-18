<template>
    <div class="container">
        <h1>{{searchData.track?searchData.track.name:""}}</h1>
        <p>by <span>{{searchData.artist?searchData.artist.name:""}}</span></p>
        <hr>
        <p class="lyric" style="white-space: pre-line;">{{searchData.track?searchData.track.text:""}}</p>
    </div>
</template>

<script>
export default {
    name: 'Lyric',
    props:[
        'searchData'
    ],
    data(){
        return {
        }
    }
}
</script>

<style scoped>
    
    div.container{
        margin: 0 auto;
        margin-top: 10px;
        padding: 10px;
        width: 380px;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        border-radius: 10px;
        background-color: #faebd7b9; 
        color: #454545
    }
    span{
        font-weight: 700;
    }
    .lyric{
        margin-top: 10px;
    }
    hr{
        padding: 0;
        margin: 0;
        margin-top: -5px;
        border: 1px solid black;
    }
</style>