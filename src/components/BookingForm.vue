<template>
<section>
    <h2>Book now!</h2>
    <form>
        <div class="row">
            <label for="cruise-country">From : </label>
            <select id="cruise-country" v-model="fromId">
                <option disabled value="-1">Select country</option>
                <option v-for="(country, index) in from" :value="index" :key="index">
                    {{ country.name }} 
                </option>
            </select>&emsp; 
            <label for="cruise-country">To : </label>
            <select id="cruise-country" v-model="toId">
                <option disabled value="-1">Select country</option>
                <option v-for="(country, index) in to" :value="index" :key="index">
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
        </div><br>
    </form>
</section>
</template>

<script>
    export default {
        props: {
            cabins: Array,
            from: Array,
            to: Array
        },
        emits: [ 'bookingCreated' ],
        data() {
            return {
                cabinIndex: -1,
                fromId: -1,
                toId: -1,
            }
        },
        methods: {
            bookCabin() {
                if (this.cabinIndex < 0 && this.fromId < 0 && this.toId < 0) return;
                this.$emit('bookingCreated', this.cabinIndex,this.fromId, this.toId);
                this.cabinIndex = -1;
                this.fromId = -1;
                this.toId = -1;
            },
        }
    }
</script>

<style scoped>
h2 {
    font-size: 30px;
    position: relative;
    left: 50px;
}

.row {
    position: relative;
    left: 50px;
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
    border: white;
    background-color: rgb(216, 215, 215);
}
button:hover { background-color: rgb(126, 213, 188); }
button:active {
    background-color: darkgray;
    box-shadow: 0 5px #666;
    transform: translateY(4px);
}
</style>