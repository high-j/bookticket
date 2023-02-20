<template>
    <section>
        <div class="nav-bar">
            <h1>Welcome to Galaxy Airline</h1>
            <h2>{{ cruise.name }}</h2>
            <h4>{{ cruise.description }}</h4>
        </div>
        

        <div>
            <!-- <h2>{{ cruise.name }}</h2>
            <div>{{ cruise.description }}</div>
            <hr /> -->

            <div class="row">
                <div>
                    <!-- TODO: Add booking-form -->
                    <booking-form @booking-created="addBooking" :cabins="cruise.cabins" :countrys="cruise.countrys"></booking-form>
                </div>
                <div>
                    <!-- TODO: Add booking-list -->
                    <booking-list :bookings="bookings"></booking-list>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import BookingList from './BookingList.vue';
import BookingForm from './BookingForm.vue';

    export default {
        name: 'Host',
        data() {
            return {
                cruise:{
                    name: 'Cruise to anywhere',
                    description: 'Book a ticket and enjoy your life.',
                    cabins: [
                        { name:'Economy Class', price:2500 },
                        { name: 'Bussiness Class', price:5000 },
                        { name: 'First Class', price:12500 },
                    ],
                    countrys: [
                        { name: 'America'},
                        { name: 'UK'},
                        { name: 'Japan'},
                        { name: 'Korea'},
                    ]
                }, 
                bookings: [
                    { name: 'Sample', price: 0 }
                ]
            }
        },
        // TODO: ADD Components
        components: {
            BookingList,
            BookingForm
        },
        methods: {
            addBooking(cabinIndex, countryId) {
                const cabin = this.cruise.cabins[cabinIndex];
                const country = this.cruise.countrys[countryId];
                const booking = {
                    country: country.name,
                    cabin: cabin.name,
                    price: cabin.price,
                }
                this.bookings.push(booking);
            }
        }
    }
</script>

<style scoped>
body {
    background-color: white;
    margin: 0, 5%;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    vertical-align: middle;
    margin: 2em;
}
.nav-bar {
    background: linear-gradient(-50deg, #33FFCA,#33DDFF);
    height: 180px;
    margin-bottom: 10px;
    text-align: center;
}
.head {
    background-color: aquamarine;
}

h1 {
    text-align: center;
    font-size: 35px;
}
</style>