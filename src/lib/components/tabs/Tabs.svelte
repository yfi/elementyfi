<script lang="ts">
  import { nanoid } from "./nanoid"
  import { writable } from "svelte/store"
  import { onMount, setContext } from "svelte"

  const root = writable()
  const index = writable(0)
  export let label = "Tabs"
  export let id: string = nanoid()
  export let orientation: "horizontal" | "vertical" = "horizontal"

  setContext("tabs", {
    selectedTab: index,
    root,
  })
</script>

<div {id} bind:this={$root} class={orientation}>
  <div
    role="tablist"
    aria-label={label}
    id="tablist_{id}"
    aria-orientation={orientation}
  >
    <slot />
  </div>

  <slot name="tabcontent" />
</div>

<style>
  div:not(.horizontal) {
    @apply flex;
  }

  [aria-orientation="horizontal"] {
    @apply flex;
  }
</style>
