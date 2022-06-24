<template>
    <div ref="animal" class="animal" v-bind:style="maxAnimalSizeCss">
        <span class="animal__title">{{ animal.name }}</span>
        <img :src="animal.icon" alt="icon" :width="animalSize">
    </div>
</template>
<script>

export default {
    props: {
        animal: Object,
        size: Number,
        sizeDelta: Number,
        ageTime: Number,
        kind: Object
    },

    data: () => ({
        interval: null,
    }),

    methods: {
        ageEvent() {
            this.interval = setInterval(() => {
                this.$emit('age', this.animal.name)
            }, 1000 * this.ageTime)
        }
    },

    computed: {
        animalSize() {
            return this.sizeDelta * this.size
        },
        maxAnimalSizeCss() {
            return {width: this.sizeDelta * this.kind.max_size + 'px'}
        }
    },

    mounted() {
        if (this.animal.age < this.kind.max_age) {
            this.ageEvent()
        }

        this.$refs.animal.addEventListener('mouseover', this.hoverAnimal)
    },
    
    updated() {
        if (this.animal.age == this.kind.max_age) {
            clearInterval(this.interval)
        }
    },


    beforedestroyed() {
        clearInterval(this.interval)
        this.$refs.animal.removeEventListener('mouseover', this.hoverAnimal)
    }
}
</script>
<style lang="scss" scoped>
    .animal {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .animal__title {
        box-sizing: border-box;
        display: flex;
        align-items: center;
        height: 32px;

        padding: 0 12px;

        border-radius: 8px;
        background-color: rgb(250, 250, 250, .8);

        font-size: 16px;
        margin-bottom: 24px;
    }
</style>