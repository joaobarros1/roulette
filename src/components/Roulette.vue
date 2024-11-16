<template>
    <div class="roulette-container">
        <img
            :src="rouletteImage"
            class="roulette-wheel"
            :class="{ spinning: spinning }"
            :style="{ transform: `rotate(${rotation}deg)` }"
            alt="Roulette Wheel"
        />
        <button @click="spinRoulette" :disabled="spinning">Spin</button>
    </div>
</template>

<style>
.roulette-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    gap: 1rem;
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
</style>

<script>
import rouletteImage from "../assets/roulette.svg";

export default {
    data() {
        return {
            rotation: 0, // Current rotation of the wheel
            spinning: false, // Controls if the wheel is spinning
            rouletteImage, // Image path
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
            }, 3000); // Spin duration (3 seconds)
        },
        determineResult(angle) {
            // Map angle to a roulette number or color
            const result = Math.floor(angle / 10); // Assuming 36 segments
            alert(`The ball landed on: ${result}`);
        },
    },
};
</script>
