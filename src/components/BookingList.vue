<template>
<section>
    <h2>
        Here's your bookings:
    </h2>

    <div class="row" v-for="(booking, index) in bookings" :key="index">
        <div class="country">
            {{ booking.from }} ⇢
            {{ booking.to }}
        </div>
        <div class="date">{{ booking.datepick }}</div>
        <div>{{ booking.cabin }}</div><hr />
    </div>

    <h3 class="row">
        Total : {{ totalDisplay }}
    </h3>
</section>
</template>

<script>
    export default {
        props: {
            bookings: Array,
        },
        computed: {
            totalDisplay() {
                let totalCost = 0;
                if (this.bookings && this.bookings.length > 0) {
                    totalCost = 
                        this.bookings.map( b => b.price).reduce((a,b) => a + b);
                }
                return '$' + totalCost.toLocaleString('en-US');
            }
        }
    }
</script>

<style scoped>
h2 {
    font-size: 30px;
}

.row {
    font-size: 18px;
}

.country {
    color: brown;
    font-weight: bolder;
}

.date {
    color: rgb(56, 75, 111);
    font-weight: bolder;
}
</style>