<template>
    <header class="header">
        <Navbar />
    </header>
    <main>
        <Hero />


        <div id="projects_section">
            <Project />
        </div>
        <div id="community_section">
            <Community />
        </div>


    </main>
</template>
<script>
import Navbar from '@/components/Navbar/Navbar.vue';
import Hero from '@/components/Hero/Hero.vue';
import Community from '@/components/Community/Community.vue';
import Project from '@/components/Project/Project.vue';

export default {
    components: {
        Navbar,
        Hero,
        Project,
        Community
    }
}
</script>
<style></style>