<template>
    <div class="empty-msg">
        <span class="text-muted mb-3">Nothing to do...</span>
        <div class="img-container">
            <img src="https://i1.sndcdn.com/artworks-vWHZWl9O2ZfOarK1-QL9esA-t500x500.jpg" />
        </div>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
    .empty-msg {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 2rem;
        background-color: $white;
        border-radius: .5rem;
        border: 1px solid $medium-gray;
    }

    .img-container {
        height: 15rem;
        width: 15rem;

        img {
            height: 100%;
            width: 100%;
            object-fit: contain;
        }
    }
</style>
