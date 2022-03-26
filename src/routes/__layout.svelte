<script lang="ts">
  import '../app.css'
  import Head from '$lib/components/Head.svelte'
  import Kofi from '$lib/components/Kofi.svelte'
  import Menu from '$lib/components/Menu.svelte'
  import Social from '$lib/components/Social.svelte'
  import ThemeSelector from '$lib/components/ThemeSelector.svelte'
  import Modal from '$lib/components/Modal.svelte'
  import { darkTheme, modalViewed } from '$lib/store'

  const url = 'https://operationrome.vercel.app'
  const title = 'Operation Rome Count Down'
  const description = 'Operation Rome Count Down for 9arm'

  const menuItems = [{ name: 'Made by bossoq', url: 'https://github.com/bossoq/operation_rome' }]
  const imageUrl = `${url}/screenshot.jpg`
  const gtagId = null
  const themeIcons = ['🌞 Toggle Light mode', '🌙 Toggle Dark mode']
</script>

<Head {title} {description} {url} {imageUrl} {gtagId} />
<Kofi name="bossoq" label="Buy me Coffee" />
<Social {url} {title} />
<main class={$darkTheme && 'dark'}>
  <ThemeSelector {themeIcons} />
  <Menu items={menuItems} />
  {#if $modalViewed}
    <Modal />
  {/if}
  <slot />
</main>
