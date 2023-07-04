<script>
import { store } from '../data/store';
export default {
    data() {
        return {
            store,
        };
    },
    created() {
        
        setTimeout(() => {
            this.isLoading = false;
        }, 1000);
    }
};
</script>

<template>
    <div v-if="store.isLoading" class="temp my-background">
        <figure>
            <span class="loading-t">Loading</span>
        </figure>
    </div>
</template>

<style scoped>
.temp {
    background-color: rgba(0, 0, 0, 1);
    position: fixed;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
}
.my-background {
    background-color: darkslategrey;
}
.loader {
    width: 200px;
    height: 200px;
}
.loading-t {
    margin-right: 30px;
    color: white;
    font-size: 60px;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>