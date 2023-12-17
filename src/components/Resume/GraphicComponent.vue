<script setup>
import { toRefs, defineProps, computed } from 'vue';

const props = defineProps({
    amounts: {
        type: Array,
        default: () => []
    }
});

const { amounts } = toRefs(props);

const amountToPixels = (amount) => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);

    return `${min} ${max}`;
};

const points = computed(() => {
    const total = amounts.value.length;

    return Array(total).fill(100).reduce((points, amount, index) => {
        const x = (300 / total) * (index + 1);
        const y = amountToPixels(amount);
        console.log("y: ", y);
        return `${points} ${x} ${y}`;
    }, "0,100");

});

</script>
<template>
    <div>
        <svg view-box="0 0 300 200">
            <line stroke="#C4C4C4" stroke-width="2" x1="0" y1="100" x2="300" y2="100" />
            <polyline fill="none" stroke="#0689b0" stroke-width="2" :points="points" />
            <line stroke-width="2" stroke="#04b500" x1="200" y1="0" x2="200" y2="200" />
        </svg>
        <p>Últimos 30 días</p>
    </div>
</template>


<style scoped>
svg {
    width: 100%;
}

p {
    text-align: center;
}
</style>