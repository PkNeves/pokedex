<template>
    <div>

    <div class="card">
        <div class="card-image">
            <figure>
            <img :src="pokemon.currentImage" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-left">
                
            </div>
            <div class="media-content">
                <p class="title is-4">{{ nome | filterNome }}</p>
                <p class="subtitle is-6">{{ url }}</p>
            </div>
            </div>

            <div class="content">
                <button @click="mudarImagem" class="button is-fullwidth">Mudar Imagem</button>
            </div>
        </div>
    </div>


    </div>




</template>

<script>
import axios from 'axios'

export default {
    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.currentImage = this.pokemon.front
            //console.log('front', this.pokemon.front)
            this.pokemon.back = res.data.sprites.back_default
        })
    },
    data() {
        return {
            pokemon: {
                type: '',
                front: '',
                back: '',
                currentImage: ''
            },
            isFront: true
        }
    },
    props: {
        nome: String,
        url: String,
        num: Number
    },
    filters: {
        filterNome(nome) {
            return nome[0].toUpperCase() + nome.slice(1)
        }
    },
    methods: {
        mudarImagem() {
            this.pokemon.currentImage = this.isFront ? this.pokemon.back : this.pokemon.front
            this.isFront = !this.isFront
        }
    }
}
</script>

<style scoped>
    .card {
        margin: 20px;
    }
</style>