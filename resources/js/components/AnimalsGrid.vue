<template>
    <div class="animals-grig">
        <div v-for="animal in animals" :key="animal.name">
            <img :src="animal.icon" alt="icon" :width="50 * animal.size">
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .animals-grig {
        margin-top: 200px;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 50px;
    }
</style>

<script>
import catSvg from '../../assets/images/cat.svg'
import dogSvg from '../../assets/images/dog.svg'

export default {
    data: () => ({
        animals: [
            {
                name: 'Simon',
                kind: 'cat',
                age: '1',
                size: '1',
                icon: catSvg
            },
            {
                name: 'Jack',
                kind: 'dog',
                age: '7',
                size: '10',
                icon: dogSvg
            }
        ]
    })
}
</script>