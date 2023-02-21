<template>
    <section>
        <div class="nav-bar">
            <h1>{{ cruise.name }}</h1>
            <h3>{{ cruise.description }}</h3>
        </div>
        

        <div>
            <img alt="Web pic" src="../assets/fly.png">
            <div class="row">
                <div>
                    <!-- Add booking-form -->
                    <booking-form @booking-created="addBooking" :cabins="cruise.cabins" :from="cruise.from" :to="cruise.to"></booking-form>
                </div>
                <div>
                    <!-- Add booking-list -->
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
                    description: 'Book a flight and enjoy your life.',
                    cabins: [
                        { name:'Economy Class', price:2500 },
                        { name: 'Bussiness Class', price:5000 },
                        { name: 'First Class', price:12500 },
                    ],
                    from: [
                        { name: '(TPE)Taipei'},
                        { name: '(KHH)Kaohsiung'},
                        { name: '(HKG)Hongkong'},
                        { name: '(ICN)Incheon'},
                    ],
                    to: [
                        { name: '(TPE)Taipei'},
                        { name: '(KHH)Kaohsiung'},
                        { name: '(HKG)Hongkong'},
                        { name: '(ICN)Incheon'},
                    ],
                }, 
                bookings: [
                    { name: 'Sample', price: 0 }
                ],
                
            }
        },
        // ADD Components
        components: {
            BookingList,
            BookingForm
        },
        methods: {
            addBooking(cabinIndex, fromId, toId) {
                const cabin = this.cruise.cabins[cabinIndex];
                const from = this.cruise.from[fromId];
                const to = this.cruise.to[toId];
                const booking = {
                    from: from.name,
                    to: to.name,
                    cabin: cabin.name,
                    price: cabin.price,
                }
                this.bookings.push(booking);
            }
        }
    }
</script>

<style scoped>
img {
    width: 1450px;
}
body {
    background-color: white;
    margin: 0, 5%;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.row {
    border-style: dotted;
    border-radius: 20px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    vertical-align: middle;
    margin: 2em;
}
.nav-bar {
    background: linear-gradient(-50deg, #33FFCA,#33DDFF);
    height: 180px;
    /* margin-bottom: 10px; */
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