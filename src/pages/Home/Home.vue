<template >
    <header class="header"> 
        <Navbar/>
    </header>
    <main>
        <h1>Welcome to the Home Page</h1>
        <p>This is the main content of the home page.</p>
    </main>
</template>
<script>
import Navbar from '@/components/Navbar/Navbar.vue';
export default {
    components: {
        Navbar
    }
}
</script>
<style >
    
</style>