<template>
    <div>
        <CreateAnimalBtn v-if="hasKinds" :kinds="kinds" @selectkind="showCreateAnimalDialog" />
        <AnimalsGrid v-if="hasAnimals" />
        <CreateAnimalForm v-if="showForm && selectedKind" 
            :kind="selectedKind" 
            @close="closeCreateAnimalDialog"
            @createanimal = "createAnimal"
        />
    </div>
</template>
<script>
    import CreateAnimalBtn from './CreateAnimalBtns.vue'
    import AnimalsGrid from './AnimalsGrid.vue'
    import CreateAnimalForm from './CreateAnimalForm.vue'

    export default {
        components: {
            CreateAnimalBtn,
            AnimalsGrid,
            CreateAnimalForm
        },

        data: () => ({
            showForm: false,
            selectedKind: null,
            kinds: [],
            animals: []
        }),

        computed: {
            hasKinds() {
                return this.kinds.length > 0
            },
            hasAnimals() {
                return this.animals.length > 0
            }
        },

        mounted() {
            axios
                .get('/api/animal_kinds')
                .then(response => (this.kinds = response.data))

            axios
                .get('/api/animals')
                .then(response => (this.animals = response.data))
        },

        methods: {
            showCreateAnimalDialog(kind_name) {
                this.selectedKind = kind_name
                this.showForm = true
            },
            closeCreateAnimalDialog() {
                this.showForm = false
            },
            createAnimal(animalData) {
                this.showForm = false
                console.log(animalData)
                axios
                    .post('/api/animals', animalData)
                    .then(response => console.log(response))
                    .catch(error => console.log(error))
            }
        }
    }
</script>
