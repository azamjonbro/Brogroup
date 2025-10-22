<template >
    <header class="header"> 
        <Navbar/>
    </header>
    <main>
        <Hero/>
        <Community/>
    </main>
</template>
<script>
import Navbar from '@/components/Navbar/Navbar.vue';
import Hero from '@/components/Hero/Hero.vue';
import Community from '@/components/Community/Community.vue';
export default {
    components: {
        Navbar,
        Hero,
        Community
    }
}
</script>
<style >
    
</style>