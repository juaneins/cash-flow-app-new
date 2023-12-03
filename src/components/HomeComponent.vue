<script setup>
import LayoutComponent from './LayoutComponent.vue';
import HeaderComponent from './HeaderComponent.vue';
import ResumeComponent from './Resume/ResumeComponent.vue';
import MovementsComponent from './MovementsComponent.vue';
</script> 
<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent />
        </template>
        <template #resume>
            <ResumeComponent />
        </template>
        <template #movements>
            <MovementsComponent />
        </template>
    </LayoutComponent>
</template>