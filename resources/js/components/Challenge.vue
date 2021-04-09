<template>
    <div class="row">
        <!-- BEGIN FILTER BY breed -->
        <div>
            <h2>
                Breeds
            </h2>
            <label
                v-for="(breed, key) in dogs.message"
                :key="key"
                @change="checkedFunc"
            >
                <input type="radio" :id="key" :value="key" v-model="checked" />
                <span class="breed_check" :for="key">{{ key }}</span>
                <div class="b-input"></div>
            </label>
        </div>
        <!-- END FILTER BY breed -->
        <div>
            <h2>
                Risultati
            </h2>

            <div>
                <img :src="select.message" alt="" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            dogs: "",
            checked: [],
            select: ""
        };
    },
    methods: {
        checkedFunc: function() {
            fetch(`https://dog.ceo/api/breed/${this.checked}/images/random`)
                .then(response => response.json())
                .then(data => {
                    this.select = data;
                });
        }
    },
    mounted() {
        fetch("https://dog.ceo/api/breeds/list/all")
            .then(response => response.json())
            .then(data => {
                this.dogs = data;
            });
    }
};
</script>
<style>
.breed_check {
    text-transform: capitalize;
}
.row {
    display: flex;
    justify-content: space-around;
}
img {
    max-width: 300px;
}
</style>
