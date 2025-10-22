<template >
    <nav class="navbar">
        <div class="navbar-brand">
            <router-link to="/">My App</router-link>
        </div>
        <div class="navbar-menu">
            <router-link to="/about">About</router-link>
            <router-link to="/projects">Projects</router-link>
            <router-link to="/services">Services</router-link>
            <router-link to="/pricing">Pricing</router-link>
            <router-link to=""></router-link>
        </div>
        <div class="navbar-end">
            <router-link to="/login">Contact</router-link>
        </div>
    </nav>
</template>
<script>
export default {
    
}
</script>
<style>
    
</style>