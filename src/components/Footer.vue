<template>
  <footer class="footer">
    <div class="footer-body">
        <div class="container">
            <a href="#" class="logo">
                <img src="../assets/images/icons/movie_logo.png" alt="movie_logo">
                <span class="logo-title">Movie-Land</span>
            </a>
            <div class="footer-right-column">
                <div class="footer-menu">
                    <div class="footer-menu__header">
                        <div class="footer-menu__title">Support</div>
                        <div class="footer-menu__toggler" @click="toggleMenu"></div>
                    </div>
                    <ul class="footer-menu__list">
                        <li class="footer-menu__list-item"><a href="#">Help</a></li>
                        <li class="footer-menu__list-item"><a href="#">Advisories</a></li>
                        <li class="footer-menu__list-item"><a href="#">Status</a></li>
                    </ul>
                </div>
                <div class="footer-menu">
                    <div class="footer-menu__header">
                        <div class="footer-menu__title">Company</div>
                        <div class="footer-menu__toggler" @click="toggleMenu"></div>
                    </div>
                    <ul class="footer-menu__list">
                        <li class="footer-menu__list-item"><a href="#">About</a></li>
                        <li class="footer-menu__list-item"><a href="#">Blog</a></li>
                        <li class="footer-menu__list-item"><a href="#">Press</a></li>
                    </ul>
                </div>
                <div class="footer-menu">
                    <div class="footer-menu__header">
                        <div class="footer-menu__title">Terms &amp; Policies</div>
                        <div class="footer-menu__toggler" @click="toggleMenu"></div>
                    </div>
                    <ul class="footer-menu__list">
                        <li class="footer-menu__list-item"><a href="#">Terms of Use</a></li>
                        <li class="footer-menu__list-item"><a href="#">Advisories</a></li>
                        <li class="footer-menu__list-item"><a href="#">Privacy</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
    <div class="footer-underline">
        <div class="container">
            <div class="copyright">&copy; All Rights Reserved</div>
        </div>
    </div>
  </footer>
</template>

<script>
export default ({
    data () {
        return {
            currInd: 0
        }
    },
    methods: {
        toggleMenu(e){
            const menuList = document.querySelectorAll('.footer-menu__list');
            const menuTogglers = document.querySelectorAll('.footer-menu__toggler');
            const ind = Array.from(menuTogglers).indexOf(e.target);
            const menuHeight = menuList[ind].style.height;

            if(menuHeight && menuHeight.charAt(0) != 0){
                menuList.forEach(el => el.style.height = '0px');
            } else {
                menuList.forEach(el => el.style.height = '0px');
                menuList[ind].style.height = menuList[ind].scrollHeight + 'px';
            }
        }
    }
})
</script>
