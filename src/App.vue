<template>
    <div class="d-flex">
        <div class="c-flex-2">
            <img class="c-img" src="@/assets/bg.jpeg" alt="Background image" /> 
        </div>
        <div class="c-flex-5 my-5">
            <router-view v-slot="{ Component }">
                <transition name="fade">
                    <component :is="Component" />
                </transition>
            </router-view>
        </div>
    </div>
</template>

<style>
.c-img {
    min-height: 100vh;
    height: 100%;
    width: 100%;
    object-fit: cover;
}

.c-flex-2 {
    flex-basis: 25%;
}

.c-flex-5 {
    flex-basis: 75%;
}

.fade-move, 
.fade-enter-active,
.fade-leave-active {
    transition: all 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

.fade-leave-active {
    position: absolute;
}
</style>
