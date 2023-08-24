<template>
    <div class="slide">
        <div v-if="currentSlide === 0">
            <h2>Slide 1: Name and Phone</h2>
            <input v-model="name" placeholder="Name" />
            <input v-model="phone" placeholder="Phone" />
            <button @click="nextSlide">Next</button>
        </div>
        <div v-else-if="currentSlide === 1">
            <h2>Slide 2: Interests</h2>
            <label>
                <input type="checkbox" v-model="interests.football" />
                Football
            </label>
            <label>
                <input type="checkbox" v-model="interests.basketball" />
                Basketball
            </label>
            <label>
                <input type="checkbox" v-model="interests.iceHockey" />
                Ice Hockey
            </label>
            <button @click="prevSlide">Previous</button>
            <button @click="submitForm">Submit</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "Registeration",
    data() {
        return {
            currentSlide: 0,
            name: '',
            phone: '',
            interests: {
                football: false,
                basketball: false,
                iceHockey: false,
            },
        };
    },
    methods: {
        nextSlide() {
            this.currentSlide++;
        },
        prevSlide() {
            this.currentSlide--;
        },
        submitForm() {
            const formData = {
                name: this.name,
                phone: this.phone,
                interests: Object.keys(this.interests).filter(key => this.interests[key]),
            };
            console.log(formData); // You can replace this with your desired action
        },
    },

}
</script>

<style scoped>
.slide {
    max-width: 400px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
}
</style>
