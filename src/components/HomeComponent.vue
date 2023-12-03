<script setup>
import LayoutComponent from './LayoutComponent.vue';
import HeaderComponent from './HeaderComponent.vue';

</script> 
<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent />
        </template>
    </LayoutComponent>
</template>