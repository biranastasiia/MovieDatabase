<template>
    <div class="film-card">
        <div class="film-card__poster">
            <img :src="filmData.Poster" :alt="filmData.Title">
        </div>
        <div class="film-card__info">
            <div class="film-card__info-link" @click="openFilmModal"></div>
            <div class="film-card__info-title">{{ filmData.Title }} &lpar;{{ filmYear }}&rpar;</div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['info'],
        data() {
            return {
                filmData: this.info
            }
        },
        computed: {
            filmYear(){
                if(this.info){
                    if(this.info.Year[this.info.Year.length-1] === "–"){
                        let year = this.info.Year.split('');
                        year.splice(4, 0, ' ');
                        year.push(' ...');
                        return year.join('');
                    } else {
                        return this.info.Year
                    }
                } else {
                    return null
                }
            }
        },
        methods: {
            openFilmModal(){
                this.$root.$refs.modal.openModal(this.filmData.Title);
            }
        }
    }
</script>