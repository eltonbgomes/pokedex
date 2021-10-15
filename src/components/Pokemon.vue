<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure class="" @click="changeSprite">
                <img :src="currentImage" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{pokemon.id}} - {{name | upper}}</p>
                        <p class="subtitle is-6">{{pokemon.type}}</p>
                    </div>
                </div>
                <div class="content">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.pokemon.id = res.data.id;
            this.currentImage = this.pokemon.front;
            //console.log(this.pokemon);
            //console.log(res);
        })
    },
    data(){
        return {
            isFront: true,
            currentImage:'',
            pokemon: {
                type: '',
                front: '',
                back: '',
                id: ''
            }
        }
    },
    props: {
        name: String,
        url: String
    },
    filters: {
        upper: function(name){
            var newName = name[0].toUpperCase() + name.slice(1);
            return newName;
        }
    },
    methods: {
        changeSprite: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImage = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImage = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
#pokemon{
    margin-top: 2%;
}
</style>