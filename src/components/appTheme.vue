<template>
    <div class="themeButton">
        <button
            @click="toggle"
        >Toggle Theme</button>
    </div>
</template>
<script>

export default {
    data() {
        return {
            theme: 'light',
            themeSwitch: false
        }
    },
    methods: {
        toggle() {
            this.themeSwitch = !this.themeSwitch
            if(this.theme == 'light') this.theme = 'dark'
            else this.theme = 'light'

            this.$emit('theme', this.theme)
        }
    }
}
</script>
<style>
.themeButton {
    padding-top: 10px;
    padding-bottom: 10px;
}
</style>

