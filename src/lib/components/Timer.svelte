<script lang="ts">
  import { onMount } from 'svelte'
  import { tweened } from 'svelte/motion'
  import { cubicOut } from 'svelte/easing'
  import moment from 'moment'

  const eventTime = new Date('2027-03-19T16:00:00.000Z').getTime()
  // const eventTime = new Date('2023-03-27T15:00:00.000Z').getTime()
  const currentTime = Date.now()
  const allDuration = 157766400000
  let diffTime = eventTime - currentTime
  const progress = tweened(0, {
    duration: 400,
    easing: cubicOut
  })

  let remaining = {
    years: 0,
    months: 0,
    days: 0,
    hours: 0,
    minutes: 0,
    seconds: 0,
    done: true,
    loaded: false
  }
  let timer = null

  onMount(() => {
    let duration = moment.duration(diffTime, 'milliseconds')
    const interval = 1000

    timer = setInterval(() => {
      if (diffTime > 0) {
        diffTime -= interval
        progress.set((allDuration - diffTime) / allDuration)
        duration = moment.duration(diffTime, 'milliseconds')
        remaining = {
          years: duration.years(),
          months: duration.months(),
          days: duration.days(),
          hours: duration.hours(),
          minutes: duration.minutes(),
          seconds: duration.seconds(),
          done: false,
          loaded: true
        }
      } else {
        clearInterval(timer)
        progress.set(1)
        remaining = {
          years: 0,
          months: 0,
          days: 0,
          hours: 0,
          minutes: 0,
          seconds: 0,
          done: true,
          loaded: true
        }
      }
    }, interval)
  })
</script>

{#if remaining.loaded}
  <div class="flex flex-col gap-2 justify-center items-center mt-2 p-4">
    {#if remaining.done === false}
      {#if remaining.years > 0}
        <div class="flex flex-row gap-2 justify-center items-center">
          <span class="text-9xl dark:text-white text-black font-medium">{remaining.years} ปี</span>
        </div>
      {/if}
      {#if remaining.months > 0 || remaining.days > 0}
        <div
          class="flex flex-row {remaining.years > 0
            ? 'gap-2'
            : 'gap-2 sm:gap-6'} justify-center items-center"
        >
          {#if remaining.months > 0}
            <span
              class="{remaining.years > 0
                ? 'text-2xl'
                : 'text-4xl sm:text-9xl'} dark:text-white text-black font-medium"
              >{remaining.months} เดือน</span
            >
          {/if}
          <span
            class="{remaining.years > 0
              ? 'text-2xl'
              : 'text-4xl sm:text-9xl'} dark:text-white text-black font-medium"
            >{remaining.days} วัน</span
          >
        </div>
      {/if}
      <div
        class="flex flex-row {remaining.years > 0 || remaining.months > 0 || remaining.days > 0
          ? 'gap-2'
          : 'gap-2 sm:gap-6'} justify-center items-center"
      >
        <span
          class="{remaining.years > 0 || remaining.months > 0 || remaining.days > 0
            ? 'text-2xl'
            : 'text-3xl sm:text-6xl'} dark:text-white text-black font-medium"
          >{remaining.hours} ชั่วโมง</span
        >
        <span
          class="{remaining.years > 0 || remaining.months > 0 || remaining.days > 0
            ? 'text-2xl'
            : 'text-3xl sm:text-6xl'} dark:text-white text-black font-medium"
          >{remaining.minutes} นาที</span
        >
        <span
          class="{remaining.years > 0 || remaining.months > 0 || remaining.days > 0
            ? 'text-2xl'
            : 'text-3xl sm:text-6xl'} dark:text-white text-black font-medium"
          >{remaining.seconds} วินาที</span
        >
      </div>
    {:else}
      <div
        class="flex flex-col gap-6 justify-center items-center text-3xl sm:text-4xl dark:text-white text-black font-medium text-center"
      >
        <span>ถึงเวลาแล้วชาวแชท</span>
        <span>ที่เราจะมาร่วมกันทวงนายอาร์มเล่าเรื่องปัญหาในบริษัทที่ต้องใช้เวลาแก้กว่า 1 ปี</span>
      </div>
    {/if}
  </div>
{/if}
<div class="w-9/12 bg-gray-200 rounded-full h-5 dark:bg-gray-700 mt-2">
  <div class="dark:bg-teal-200 bg-teal-800 h-5 rounded-full" style="width: {$progress * 100}%" />
</div>
