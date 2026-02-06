<template>
  <div
    class="container"
    :style="{
      backgroundImage: `url(${heartBg}), linear-gradient(180deg, #ffe4ec, #ffd6e0)`
    }"
  >
    <div v-if="state === 'question'" class="card big">
      <h1>To the one who makes my heart smile 💖</h1>

      <p class="question">
        This heart has already chosen you… <br />
        <strong>will you be my Valentine?</strong>
      </p>

      <div
        class="buttons"
        @mousemove="(e) => {
          fleeFromMouse(e, yesBtn)
          fleeFromMouse(e, noBtn)
        }"
      >
        <button
          class="btn yes"
          ref="yesBtn"
          @mouseleave="resetButton(yesBtn)"
          @click="sayYes"
        >
          Of course ❤️
        </button>

        <button
          class="btn no"
          ref="noBtn"
          @mouseleave="resetButton(noBtn)"
          @click="sayNo"
        >
          Let me think 😏
        </button>
      </div>
    </div>

    <div v-if="state === 'yes'" class="final big">
      <h1>💘 It’s a date 💘</h1>
      <p>
        Then it’s official…<br />
        Invite me on <strong>February 14th at 6:00 PM</strong>.<br />
        I’ll be ready, smiling… just for you 😌✨
      </p>
    </div>

    <div v-if="state === 'no'" class="final big">
      <h1>😌 Oops…</h1>
      <p>
        That’s unfortunate…<br />
        Looks like you just missed the sweetest Valentine date ever 💅💔
      </p>
    </div>
    
  </div>
   <footer class="dev-footer">
    © Designed & developed by Malika
  </footer>
</template>

<script setup>
import { ref } from 'vue'
import heartBg from './assets/hearts.png'

const state = ref('question')

const yesBtn = ref(null)
const noBtn = ref(null)

function fleeFromMouse(event, btn) {
  if (!btn) return

  const rect = btn.getBoundingClientRect()
  const btnX = rect.left + rect.width / 2
  const btnY = rect.top + rect.height / 2

  const dx = btnX - event.clientX
  const dy = btnY - event.clientY

  const distance = Math.sqrt(dx * dx + dy * dy)
  const maxDistance = 180

  if (distance < maxDistance) {
    const force = (maxDistance - distance) / maxDistance
    btn.style.transform = `translate(${dx * force}px, ${dy * force}px)`
  }
}

function resetButton(btn) {
  if (!btn) return
  btn.style.transform = 'translate(0, 0)'
}

function sayYes() {
  state.value = 'yes'
}

function sayNo() {
  state.value = 'no'
}
</script>

<style scoped>
.container {
  min-height: 100vh;
  width: 100%;
  background-repeat: repeat;
  background-size: 140px, cover;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Playfair Display', serif;
}

.card.big,
.final.big {
  background: white;
  padding: 4rem 4.5rem;
  border-radius: 60px;
  text-align: center;
  box-shadow:
    0 50px 120px rgba(0, 0, 0, 0.25),
    0 0 70px rgba(255, 77, 109, 0.3);
  max-width: 1000px;
  width: 100%;
}

h1 {
  color: #c9184a;
  font-size: 3.6rem;
  margin-bottom: 2.5rem;
}

.question {
  font-size: 2rem;
  margin: 3rem 0 4rem;
  line-height: 1.6;
  color: #333;
}

.final p {
  font-size: 1.8rem;
  line-height: 1.7;
}

.buttons {
  display: flex;
  gap: 3rem;
  justify-content: center;
}

.btn {
  padding: 1.2rem 3rem;
  border-radius: 999px;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  transition: transform 0.15s ease-out;
  will-change: transform;
}

.yes {
  background: #ff4d6d;
  color: white;
}

.no {
  background: #ffd6e0;
  color: #a4133c;
}

.final {
  animation: fadeIn 1s ease forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
.dev-footer {
  position: fixed;
  bottom: 1.2rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 0.75rem;
  color: #8b2d3b;
  opacity: 0.55;
  letter-spacing: 0.03em;
  pointer-events: none; /* ne gêne jamais les clics */
  user-select: none;
}

@media (max-width: 900px) {
  .card.big,
  .final.big {
    padding: 2rem 2rem;
    border-radius: 32px;
    max-width: 70%;
  }

  h1 {
    font-size: 2.2rem;
  }

  .question,
  .final p {
    font-size: 1.3rem;
  }

  .buttons {
    flex-direction: column;
    gap: 1.5rem;
  }
}
</style>
