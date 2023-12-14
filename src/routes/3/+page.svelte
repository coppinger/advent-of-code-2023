<script lang="ts">
  import { onMount } from "svelte";
  import Item from "./Item.svelte";

  interface Record {
    name: string;
    weight: number;
  }

  let data: Array<Record> = [];

  let list: Array<Record> = [];
  let sled: Array<Record> = [];

  onMount(() => {
    async function getData() {
      const res = await fetch(
        "https://advent.sveltesociety.dev/data/2023/day-three.json",
      );

      data = await res.json();
      list = await [...data];
    }
    getData();

    console.log(list);
  });

  function listToSled(i: number) {
    const item = list.splice(i, 1);
    sled = [...sled, ...item];
    list = list;
  }

  function sledToList(i: number) {
    const item = sled.splice(i, 1);
    list = [...list, ...item];
    sled = sled;
  }
</script>

<div class="grid grid-cols-5 gap-8">
  <!-- Main -->
  <div
    class="grid col-span-4 grid-cols-4 p-8 gap-8 border-2 border-slate-500 rounded-md"
  >
    {#if data.length > 0}
      {#each list as { name, weight }, i}
        <Item {name} {weight} {i} on:click={() => listToSled(i)} />
      {/each}
    {:else}
      <p>Loading...</p>
    {/if}
  </div>
  <!-- Sidebar -->
  <div
    class="flex flex-col col-span-1 gap-8 border-2 border-slate-500 rounded-md p-8"
  >
    {#if data.length > 0}
      {#each sled as { name, weight }, i}
        <Item {name} {weight} {i} on:click={() => sledToList(i)} />
      {/each}
    {:else}
      <p>Loading...</p>
    {/if}
  </div>
</div>
