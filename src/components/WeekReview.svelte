<svelte:options immutable />

<script lang="ts">
  import type { Moment } from "moment";
  import { IGranularity } from "obsidian-daily-notes-interface";
  import { getStartOfWeek } from "../utils";

  // Properties
  export let days: Moment[];

  // Event handlers
  export let onClick: (
    granularity: IGranularity,
    date: Moment,
    existingFile: null,
    inNewSplit: boolean
  ) => boolean;

  let startOfWeek: Moment;
  $: startOfWeek = getStartOfWeek(days);

  function handleClick(event: MouseEvent) {
    // Simple click only, no meta key support for now
    onClick?.("week", startOfWeek, null, false);
  }
</script>

<td>
  <div class="week-review" on:click={handleClick}>
    R
  </div>
</td>

<style>
  td {
    border-left: 1px solid var(--background-modifier-border);
  }

  .week-review {
    background-color: var(--color-background-weeknum);
    border-radius: 4px;
    color: var(--color-text-weeknum);
    cursor: pointer;
    font-size: 0.65em;
    font-weight: 600;
    height: 100%;
    padding: 4px;
    text-align: center;
    transition: background-color 0.1s ease-in, color 0.1s ease-in;
    vertical-align: baseline;
  }

  .week-review:hover {
    background-color: var(--interactive-hover);
    color: var(--interactive-accent);
  }
</style>
