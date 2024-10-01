<template>
    <Header />
    <div class="wrapper">
         <Search />
    </div>
    <Footer />
    <Modal ref="modal" />
</template>

<script>
    import Header from './components/Header.vue';
    import Search from './components/Search.vue';
    import Footer from './components/Footer.vue';
    import Modal from './components/Modal.vue';

    export default {
        components: {
            Header,
            Search,
            Footer,
            Modal
        }
    }
</script>