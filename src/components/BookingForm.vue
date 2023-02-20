<template>
<section>
    <h2>Book now!</h2>
    <form>
        <div class="row">
            <label for="cruise-country">Select country : </label>
            <select id="cruise-country" v-model="countryId">
                <option disabled value="-1">Select country</option>
                <option v-for="(country, index) in countrys" :value="index" :key="index">
                    {{ country.name }} 
                </option>
            </select><br><br>
            <label for="cruise-cabin">Select class : </label>
            <select id="cruise-cabin" v-model="cabinIndex">
                <option disabled value="-1">Select a cabin</option>
                <option v-for="(cabin, index) in cabins" :value="index" :key="index">
                    {{ cabin.name }} $ {{ cabin.price.toLocaleString('en-US') }}
                </option>
            </select>
        </div><br>
        <div class="row">
            <button class="button" type="button" @click="bookCabin">Book now!</button>
        </div>
    </form>
</section>
</template>

<script>
    export default {
        props: {
            cabins: Array,
            countrys: Array,
        },
        emits: [ 'bookingCreated' ],
        data() {
            return {
                cabinIndex: -1,
                countryId: -1,
            }
        },
        methods: {
            bookCabin() {
                if (this.cabinIndex < 0 && this.countryId < 0) return;
                this.$emit('bookingCreated', this.cabinIndex,this.countryId);
                this.cabinIndex = -1;
                this.countryId = -1;
            },
        }
    }
</script>

<style scoped>
h2 {
    font-size: 30px;
}

select {
    font-size: 15px;
    border-radius: 5px;
}

label {
    font-size: 20px;
}

button {
    font-size: 20px;
    border-radius: 8px;
}
button:hover { background-color: rgb(135, 191, 193); }
button:active {
    background-color: darkgray;
    box-shadow: 0 5px #666;
    transform: translateY(4px);
}
</style>