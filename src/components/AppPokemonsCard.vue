<script>
export default {
    props: {
        id: Number,
        name: String,
        img: String,
        type: String,
    },
};
</script>

<template>
    <div :class="`c-pokemon ${type}`">
        <div class="my-f">
            <img class="img-fluid" :src="img" :alt="name" />
        </div>
        <div># {{ id }}</div>
        <div>
            <strong>{{ name }}</strong>
        </div>
        <div>
            <em>{{ type }}</em>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@use '../assets/scss/vars' as *;
.c-pokemon {
    background-color: white;
    text-align: center;
    border-radius: 20px;
    padding: 0.5rem 1rem;

    .my-f {
        background-color: white;
        border-radius: 50%;
        width: 100px;
        height: 100px;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: auto;
        overflow: hidden;
        margin-bottom: 2rem;
    }
    
    @each $type,
    $color in $types {
        &.#{$type} {
            background-color: $color;
        }
    }
}
</style>