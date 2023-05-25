<script lang="ts">
  import { getContext, onMount } from "svelte"
  const { root, selectedTab } = getContext("tabs")

  let el
  let index
  let id

  onMount(() => {
    id = $root.id
    index = [...$root.querySelectorAll('[role="tabpanel"]')].indexOf(el)
  })

  $: selected = $selectedTab == index
</script>

<div
  class:selected
  role="tabpanel"
  aria-labelledby="{id}_tab_{index}"
  tabindex="-1"
  bind:this={el}
>
  <slot />
</div>

<style>
  div {
    @apply hidden;
  }

  .selected {
    @apply block;
  }
</style>
