<template>
    <div class="modal" v-if="isOpened">
        <div @click="closeModal" class="modal-bg"></div>
        <div class="modal-body">
            <div @click="closeModal" class="modal-close"></div>
            <FilmFullInfo :film-title="title" />
        </div>
    </div>
</template>

<script>
    import FilmFullInfo from './FilmFullInfo.vue';

    export default {
        components: {
            FilmFullInfo
        },
        data(){
            return {
                isOpened: false,
                title: ''
            }
        },
        methods: {
            openModal(prop){
                document.body.style.overflow = 'hidden';
                this.isOpened = true;
                this.title = prop;
            },
            closeModal() {
                document.body.style.overflow = 'auto';
                this.isOpened = false;
                this.title = '';
            }
        }
    }
</script>