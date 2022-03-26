<script lang="ts">
  import Timer from '$lib/components/Timer.svelte'
</script>

<div class="w-full h-screen flex bg-rome">
  <div
    class="w-full h-screen flex flex-col gap-6 justify-center items-center bg-white dark:bg-black bg-opacity-40 dark:bg-opacity-90"
  >
    <div class="flex flex-col gap-6 justify-center items-center">
      <p class="text-3xl sm:text-4xl dark:text-teal-200 text-teal-800 text-center">
        "ผมจะเล่าเรื่อง Operation Rome ในอีก 5 ปีข้างหน้า"
      </p>
      <a
        href="https://www.twitch.tv/armzi/clip/CharmingSolidMeerkatBibleThump-4r9QYutPWmFQQR97"
        target="_blank"
        class="text-2xl sm:text-3xl dark:text-gray-500 text-gray-800 text-center"
        >นายอาร์ม - 19 มิ.ย. 2565 23:00 น.</a
      >
    </div>
    <Timer />
  </div>
</div>
