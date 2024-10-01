<template>
    <section class="search" id="search">
        <div class="container">
            <h2 class="search-title">Enter the title of the movie or TV series you are looking for</h2>
            <div class="search-field">
                <input class="search-input" 
                    type="search"
                    name="search" 
                    id="film_search" 
                    placeholder="Type film title..." 
                    v-model="searchInput"
                    :onkeypress="pressKey">
                <button class="search-button" type="submit" @click="getMovies">Search</button>
            </div>
            <div class="search-results" v-if="searchResults.length > 0">
                <div class="search-results__header">
                    <div class="search-results__header-title">Search Results Total: <span>{{ totalResults }}</span></div>
                </div>
                <div class="search-results__body">
                    <FilmCard v-for="result in searchResults" :key="result.imdbID" :info="result" />
                </div>
            </div>
            <div class="search-results" v-else-if="errorText">
                {{ errorText }}
            </div>
        </div>
    </section>
</template>

<script>
    import axios from 'axios';
    import FilmCard from './FilmCard.vue';

    export default {
        components: {
            FilmCard
        },
        data() {
            return {
                searchInput: '',
                searchResults: [],
                totalResults: 0,
                errorText: ''
            }
        },
        methods: {
            pressKey(e){
                if(e.keyCode === 13){
                    this.getMovies();
                }
            },
            getMovies: function(){
                const self = this;

                axios.get('https://www.omdbapi.com/?apikey=ceb45ee3&s=' + self.searchInput)
                    .then(function(response){
                        if(response.data.Search){
                            self.searchResults = response.data.Search;
                            self.totalResults = response.data.totalResults;
                            self.errorText = '';
                        } else if (response.data.Error) {
                            self.searchResults = [];
                            self.totalResults = '';
                            self.errorText = response.data.Error;
                        }
                    })
                    .catch(function(error){
                        console.log(error);
                    })
            }
        }
    }
</script>