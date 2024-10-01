<template>
    <div class="film-info">
        <div class="loader-wrapper" v-if="loader">
            <div class="loader">
                <div class="loader-inner"></div>
            </div>
        </div>
        <div class="film-info__body" v-else>
            <div class="film-info__poster">
                <img :src="filmInfo.Poster" :alt="filmInfo.Title">
            </div>
            <div class="film-info__content">
                <h3 class="film-info__title">{{ filmInfo.Title }}</h3>
                <div class="film-info__general">
                    <div class="">{{ filmInfo.Year }}</div>
                    <div class="">{{ filmInfo.Runtime }}</div>
                    <div class="">{{ filmInfo.Rated }}</div>
                </div>
                
                <div class="film-info__row"><b>Directed By:</b> {{ filmInfo.Director }}</div>
                <div class="film-info__row"><b>Written By:</b> {{ filmInfo.Writer }}</div>
                <div class="film-info__row"><b>Actors:</b> {{ filmInfo.Actors }}</div>

                <div class="film-info__row"><b>Country:</b> {{ filmInfo.Country }}</div>
                <div class="film-info__row"><b>Box Office:</b> {{ filmInfo.BoxOffice }}</div>
                <div class="film-info__row"><b>Released:</b> {{ filmInfo.Released }}</div>
                <div class="film-info__row"><b>Genre:</b> {{ filmInfo.Genre }}</div>
                <p class="film-info__row"><b>Plot:</b> {{ filmInfo.Plot }}</p>

                <ul class="rating-list">
                    <li class="rating-list__item" 
                        v-for="rating in filmInfo.Ratings" 
                        :key="rating.Source"
                        :class="rating.Source === 'Metacritic' ? 'critic' : rating.Source === 'Rotten Tomatoes' ? 'tomato' : 'imdb'">
                        {{ rating.Value }}
                    </li>
                </ul>

            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        props: ['filmTitle'],
        data() {
            return {
                filmInfo: '',
                rating: '',
                loader: false
            }
        },
        mounted(){
            this.getFilmInfo();
            window.addEventListener("resize", this.fixModalHeight);
        },
        methods: {
            fixModalHeight(){
                const modal = document.querySelector('.modal');
                const modalBody = document.querySelector('.modal-body');
                if(modal && modalBody){
                    if(modalBody.scrollHeight <= modal.scrollHeight * 0.9){
                        modalBody.style.overflowY = 'hidden';
                    } else {
                        modalBody.style.overflowY = 'scroll';
                    }
                }
            },
            getFilmInfo(){
                const self = this;
                this.loader = true;

                axios.get('http://www.omdbapi.com/?apikey=ceb45ee3&t=' + self.filmTitle)
                    .then(function(response){
                        self.filmInfo = response.data;
                        self.loader = false;
                    })
                    .catch(function(error){
                        console.log(error, 'error');
                        self.loader = false;
                    })
                    .finally(function(){
                        self.fixModalHeight();
                    })
            }
        }
    }
</script>