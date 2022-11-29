<!-- Componente para o Logo: -->
<template>
<div><img :src="logo" :alt="description"></div>

</template>
<script>
    export default {
    name: 'LogoDesign',
        data() {
            return {
                logo: "/img/logo.png",
                description: "Logo Vue JS"
            }
        }
}
</script>
