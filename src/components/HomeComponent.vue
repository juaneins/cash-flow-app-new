<script setup>
import { ref } from 'vue';

import LayoutComponent from './LayoutComponent.vue';
import HeaderComponent from './HeaderComponent.vue';
import ResumeComponent from './Resume/ResumeComponent.vue';
import MovementsComponent from './Movements/MovementsComponent.vue';
import ActionComponent from './ActionComponent.vue';
import GraphicComponent from './Resume/GraphicComponent.vue';

const amount = ref(null);
const amounts = ref([100, 200, 500, 200, -400, -600, -300, 0, 300, 500]);
const movements = ref([
    {
        id: 1,
        title: "Movimiento",
        description: "Deposito de salario",
        amount: 1000,
    },
    {
        id: 2,
        title: "Movimiento 1",
        description: "Deposito de honorarios",
        amount: 500,
    },
    {
        id: 3,
        title: "Movimiento 3",
        description: "Comida",
        amount: -100,
    },
    {
        id: 4,
        title: "Movimiento 4",
        description: "Colegiatura",
        amount: 1000,
    },
    {
        id: 5,
        title: "Movimiento 5",
        description: "Reparación equipo",
        amount: 1000,
    },
],);




</script> 
<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent />
        </template>
        <template #resume>
            <ResumeComponent :label="'Ahorro Total'" :total-amount="45250" :amount="amount">
                <template #graphic>
                    <GraphicComponent :amounts="amounts" />
                </template>
                <template #action>
                    <ActionComponent />
                </template>
            </ResumeComponent>
        </template>
        <template #movements>
            <MovementsComponent :movements="movements" />
        </template>
    </LayoutComponent>
</template>