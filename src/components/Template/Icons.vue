<template>
    <div v-if="iconExists" v-html="getIcon(name)" style="cursor: pointer; display: flex; align-items: center"></div>

    <div v-else>
        <span>❌ Icon not found</span>
    </div>
</template>

<script>
export default {
    name: "IconComponents",
    props: {
        name: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            icons: {
                bars:`<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M3 4.5H21M3 9.5H21M3 14.5H21M3 19.5H21" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>`,
                x_mark:`<svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24" fill="none">
  <path d="M7 17L17 7M17 17L7 7" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
</svg>`
            },
        };
    },
    computed: {
        iconExists() {
            return this.icons[this.name] !== undefined;
        },
    },
    methods: {
        getIcon(name) {
            return this.icons[name] || "";
        },
    },
};
</script>