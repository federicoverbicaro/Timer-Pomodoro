<script>
export default {
  data() {
    return {
      countDown: 1,
      timerId: null,
      isPaused: false,
      pauseCountDown: 3,
      timerId2: null,
    }
  },

  methods: {
    countDownTimer() {
      if (this.timerId) return;
      this.isPaused = false;
      this.timerId = setInterval(() => {
        if (this.countDown > 0) {
          this.countDown -= 1;
        } else {
          this.stopTimer();
          this.isPaused = true;
          this.fiveCountDown();
        }
      }, 1000);
    },

    stopTimer() {
      clearInterval(this.timerId);
      this.timerId = null;
    },

    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const secs = seconds % 60;
      return `${minutes}:${secs < 10 ? '0' : ''}${secs}`;
    },

    fiveCountDown() {
      this.timerId2 = setInterval(() => {
        if (this.pauseCountDown > 0) {
          this.pauseCountDown -= 1
        } else {
          this.stopFiveTimer()
        }
      }, 1000)
    },

    stopFiveTimer() {
      clearInterval(this.timerId2);
      this.timerId2 = null;
      this.pauseCountDown = 5 * 60;
      this.isPaused = false;
      this.countDown = 25 * 60;
      this.countDownTimer();
    }
  },
}
</script>

<template>
  <div class="h-screen bg-purple-300">
    <div class="text-center w-full p-5">
      <h1 class="text-red-500 text-4xl font-mono">Time Pomodoro</h1>
    </div>
    <div>
      <div class="flex h-full ">
        <div class=" w-1/2 h-96 flex">
          <div class=" w-1/2">
            <h1 class="text-4xl capitalize text-red-500 p-6 font-mono">click me</h1>
            <div class="mt-3 flex justify-end">
              <img class="h-56 w-56" src="/img/freccia.png" alt="freccia">
            </div>
          </div>
          <div class=" w-1/2 flex justify-center items-center">
            <img @click="countDownTimer" class="h-80 w-80" src="/img/pomodoro.png" alt="pomodoro">
          </div>
        </div>
        <div class="w-1/2 h-96 flex justify-center items-center">
          <div class="border border-black rounded-full h-96 w-96 flex justify-center items-center">
            <span class="text-6xl text-white font-mono">{{ formatTime(countDown) }}</span>
          </div>
        </div>
      </div>


    </div>

    <div class=" justify-center flex mt-5 ">
      <div class="w-1/2  justify-center items-center flex h-36">
        <span @click="countDownTimer"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
            stroke-width="1.5" stroke="currentColor" class="size-14">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
            <path stroke-linecap="round" stroke-linejoin="round"
              d="M15.91 11.672a.375.375 0 0 1 0 .656l-5.603 3.113a.375.375 0 0 1-.557-.328V8.887c0-.286.307-.466.557-.327l5.603 3.112Z" />
          </svg>
        </span>
        <span @click="stopTimer"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
            stroke-width="1.5" stroke="currentColor" class="size-14">
            <path stroke-linecap="round" stroke-linejoin="round"
              d="M14.25 9v6m-4.5 0V9M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
          </svg>
        </span>
      </div>
    </div>

    <!-- Messaggio di pausa -->
    <div v-if="isPaused" class="text-center text-4xl text-green-500 mt-10 h-10">
      <h1>Prenditi 5 minuti di pausa!</h1>
      <div>
        <span class="text-6xl text-white h-5 font-mono">{{ formatTime(pauseCountDown) }}</span>
      </div>
    </div>

  </div>

</template>
