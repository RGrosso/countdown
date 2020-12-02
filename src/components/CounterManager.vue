<template>
    <main>
        <div v-for="d in this.counters" :key="d.id"> 
               <Counter :dateObj= "d"/>
        </div>
    </main>
</template>

<script>
import Counter from '@/components/Counter.vue';
export default {
    components: {
        Counter
    },
    data: () => ({
        counters: [
            {
                year:2020,
                month:11,
                date: 25,
                hour: 23,
                minute: 0,
                second: 0,
                ms: 0,
                id: 0,
            },
            {
                year:2019,
                month:11,
                date: 25,
                hour: 23,
                minute: 0,
                second: 0,
                ms: 0,
                id: 1,
            }
            ],
    }),
}
</script>

<style lang="scss" scoped>

</style>