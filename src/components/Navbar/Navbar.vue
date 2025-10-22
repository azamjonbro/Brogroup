<template >
    <nav class="navbar">
        <div class="navbar-brand">
            <router-link to="/">BROGROUP</router-link>
        </div>
        <div class="navbar-menu">
            <router-link to="/about">About</router-link>
            <router-link to="/projects">Projects</router-link>
            <router-link to="/services">Services</router-link>
            <router-link to="/pricing">Pricing</router-link>
            <router-link to="/community">Community</router-link>
        </div>
        <div class="navbar-end">
            <button @click="$router.push('/contact')">Contact</button>
        </div>
    </nav>
</template>
<script>
export default {
    
}
</script>
<style>
    
</style>