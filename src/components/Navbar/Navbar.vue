<template>
    <nav class="navbar">
        <div class="navbar-brand">
            <router-link to="/">BROGROUP</router-link>
        </div>

        <div class="navbar-menu">
            <router-link to="/about">About</router-link>
            <!-- <router-link to="/projects">Projects</router-link> -->
             <router-link to="/#projects_section">Projects</router-link>
            <router-link to="/services">Services</router-link>
            <router-link to="/pricing">Pricing</router-link>
            <router-link to="/#community_section">Community</router-link>
        </div>
        <div class="navbar-end">
            <button @click="$router.push('/contact')">Contact</button>
        </div>

        <button @click="navlinkmedia = false" class="nav_bars">
            <IconComponents name="bars" />
        </button>


        <div @click.self="navlinkmedia = true" v-if="!navlinkmedia" class="nav_media_bars">
            <div class="navbar-menu">
                <div class="nav_close_btn">
                    <button @click="navlinkmedia = true">
                    <IconComponents name="x_mark" />
                </button>
                </div>
                <router-link to="/about">About</router-link>
                <router-link to="/projects">Projects</router-link>
                <router-link to="/services">Services</router-link>
                <router-link to="/pricing">Pricing</router-link>
                <router-link to="/community">Community</router-link>

                <div class="navbar_end_contact">
                    <button @click="$router.push('/contact')">Contact</button>
                </div>
            </div>
        </div>

    </nav>
</template>
<script>
import IconComponents from "@/components/Template/Icons.vue";

export default {
    components: {
        IconComponents
    },
    data() {
        return {
            navlinkmedia: true,
        };
    },
    computed: {
    },
    methods: {
    },
    mounted() {
        if (window.innerWidth < 700) {
            this.navlinkmedia = false;
        }
    }
}
</script>
<style>
.nav_media_bars {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: end;
    gap: 10px;
    top: 0;
    right: -100%;
    width: 100%;
    min-height: 100vh;
    background-color: rgba(0, 0, 0, 0.473);
    z-index: 99;
    animation: nav_animation 0.3s ease-in-out forwards;
}

@keyframes nav_animation {
    from {
        right: -100%;
    }

    to {
        right: 0;
    }
}

.nav_media_bars .navbar-menu {
    display: flex;
    flex-direction: column;
    width: 80%;
    text-align: center;
    padding-top: 60px;
    min-height: 100vh;
    padding: 60px 10px;
    border-radius: 20px 0 0 20px;
    background-color: #1827b1;
    position: relative;
}
.nav_close_btn{
    text-align: end;
    padding: 10px;
}
.nav_media_bars .navbar-menu a {
    /* border: 1px solid red; */
    padding: 10px 0;
    border-radius: 6px;
    background-color: #00005C;
}

.nav_bars {
    display: none;
}

.navbar_end_contact {
    padding: 0.75rem 1.25rem;
    background: linear-gradient(90deg, var(--color-primary) 0%, var(--primary-hover) 100%);
    color: var(--text-on-primary);
    border-radius: var(--radius-md);
    font-weight: 700;
    font-size: 0.9375rem;
    line-height: 1;
    box-shadow: 0 6px 18px rgba(176, 60, 222, 0.18);
    transition: transform var(--transition-fast), box-shadow var(--transition-fast), background-color var(--transition-fast), opacity var(--transition-fast);
    /* display: inline-flex; */
    align-items: center;
    gap: 0.5rem;
    border: none;
    text-align: center;
    -webkit-tap-highlight-color: transparent;
    color: white;
}

@media (max-width:700px) {

    .navbar-menu,
    .navbar-end {
        display: none;
    }

    .nav_bars {
        display: block;
    }


}
</style>