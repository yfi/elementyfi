<script>
    
  import { onMount } from "svelte"
  import { getContext } from "svelte"

  const { root, selectedTab } = getContext("tabs")

  export let disabled = false

  export let focus_class = "focus:bg-yellow-400"
  export let selected_class = "underline"

  let el
  let index
  let id

  $: selected = index == $selectedTab

  onMount(() => {
    id = $root.id
    index = [...$root.querySelectorAll('[role="tab"]')].indexOf(el)
  })

</script>

<button
  bind:this={el}
  id="{id}_tab_{index}"
  aria-selected={selected}
  aria-controls="tabpanel_{index}"
  role="tab"
  class="{selected ? selected_class : ''} {focus_class}"
  on:click={() => ($selectedTab = index)}
  {disabled}><slot /></button
>

<style>
  [aria-selected="true"] {
  }

  [role="tab"] {
    @apply flex-1 flex items-center justify-center;
  }

  button {
    @apply w-full h-full;
  }
</style>
