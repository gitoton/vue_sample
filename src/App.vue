<template>
    <AppHeader />
    <AppContact />
    <AppFooter />
</template>

<script>
    import AppHeader from "./components/AppHeader"
    import AppContact from "./components/AppContact"
    import AppFooter from "./components/AppFooter"

    export default {
        name: "App",
        components: {
            AppHeader,
            AppContact,
            AppFooter,
        },
    }
</script>

<style>
</style>