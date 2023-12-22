<script setup>
import { computed, ref, onMounted } from 'vue';

import LayoutComponent from './LayoutComponent.vue';
import HeaderComponent from './HeaderComponent.vue';
import ResumeComponent from './Resume/ResumeComponent.vue';
import MovementsComponent from './Movements/MovementsComponent.vue';
import ActionComponent from './ActionComponent.vue';
import GraphicComponent from './Resume/GraphicComponent.vue';

const amount = ref(null);

const movements = ref([]);

onMounted(() => {
    const localStoreMovements = JSON.parse(localStorage.getItem("movements"));

    if (Array.isArray(localStoreMovements)) {
        movements.value = localStoreMovements?.map(m => {
            return { ...m, time: new Date(m.time) };
        });
    }
    
})

const amounts = ref(computed(() => {
    const lastDays = movements.value
    .filter(m => {
        const today = new Date();
        const oldDate = today.setDate(today.getDate() - 30);       
        return m.time > oldDate;
    })
    .map(m => m.amount);
    return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0,i);
        return lastMovements.reduce((sum, movement) => {
            return sum + movement;
        }, 0);
    })
}));

const totalAmount = computed(() => {
    return movements.value.reduce((suma, m) => {
        return suma + m.amount;
    }, 0);
});

const create = (movement) => {
    movements.value.push(movement);
    save();
}

const remove = (id) => {
    const index = movements.value.findIndex(m => m.id === id);
    movements.value.splice(index, 1);
    save();
}

const save = () => {
    localStorage.setItem("movements", JSON.stringify(movements));
}

</script> 
<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent />
        </template>
        <template #resume>
            <ResumeComponent 
                :label="'Ahorro Total'" 
                :total-amount="totalAmount" 
                :amount="amount">
                <template #graphic>
                    <GraphicComponent :amounts="amounts" />
                </template>
                <template #action>
                    <ActionComponent @create="create"/>
                </template>
            </ResumeComponent>
        </template>
        <template #movements>
            <MovementsComponent 
                :movements="movements"
                @remove="remove"
                />
        </template>
    </LayoutComponent>
</template>