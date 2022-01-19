<template>
    <div class="card" >
        <img :src="datos.cover_image" class="card-img-top" alt="...">
        <div class="card-body">
            <h5 class="card-title">{{ datos.title }}</h5>
            <p class="card-text">{{ datos.description }}</p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        datos: Object
    }

}
</script>

<style>

</style>