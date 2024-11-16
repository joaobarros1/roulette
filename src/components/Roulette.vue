<template>
    <section class="roulette-container">
        <h1>European Roulette</h1>
        <div class="result" :style="{ backgroundColor: resultColor }" ref="resultDiv">
            <h2>{{ rouletteResult }}</h2>
        </div>
        <img
            :src="rouletteImage"
            class="roulette-wheel"
            :class="{ spinning: spinning }"
            :style="{ transform: `rotate(${rotation}deg)` }"
            alt="Roulette Wheel"
        />
        <button @click="spinRoulette" :disabled="spinning" class="spin-button">Spin</button>
    </section>
    <section></section>
</template>

<style>
.roulette-container {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    height: 100vh;
    gap: 1rem;

    h1 {
        margin: 0;
        font-size: 24px;
    }
}
.roulette-wheel {
    width: 300px;
    height: 300px;
}
.roulette-wheel {
    transition: transform 3s ease-out;
}
.roulette-wheel.spinning {
    transition: transform 3s ease-out;
}
.spin-button {
    margin-top: 5rem;
}
.result {
    border: 1px solid #ccc;
    border-radius: 5px;
    min-width: 50px;
    min-height: 36px;

    h2 {
        margin: 0;
        font-size: 24px;
    }
}
</style>

<script>
import rouletteImage from "../assets/roulette.svg";

export default {
    data() {
        return {
            rotation: 0, // Current rotation of the wheel
            spinning: false, // Controls if the wheel is spinning
            rouletteImage, // Image path
            rouletteResult: "", // Result of the spin
            resultColor: "", // Color of the result
        };
    },
    methods: {
        spinRoulette() {
            if (this.spinning) return;

            this.spinning = true;

            // Calculate random spin (e.g., 5-10 full spins + random angle)
            const randomSpin = Math.floor(Math.random() * 360) + 1800; // At least 5 full spins
            const finalRotation = this.rotation + randomSpin;

            // Simulate spinning
            this.rotation = finalRotation;

            // Delay to simulate the spin duration
            setTimeout(() => {
                this.spinning = false;
                this.determineResult(finalRotation % 360); // Normalize rotation angle
                this.printBackgroundColor(); // Print background color after spin
            }, 3000); // Spin duration (3 seconds)
        },
        determineResult(angle) {
            // Map angle to a roulette number or color
            const result = Math.floor(angle / 10); // Assuming 36 segments
            this.resultColor = this.getColor(result);
            this.rouletteResult = result;
        },
        getColor(number) {
            if (number === 0) return "green"; // Special case for 0
            const redNumbers = [1, 3, 5, 7, 9, 12, 14, 16, 18, 19, 21, 23, 25, 27, 30, 32, 34, 36];
            return redNumbers.includes(number) ? "red" : "black";
        },
        printBackgroundColor() {
            const resultDiv = this.$refs.resultDiv;
            resultDiv.style.backgroundColor = this.resultColor;
        },
    },
};
</script>
