<script lang="ts">
  import { Button } from "$lib/components/ui/button";
  import { onMount } from "svelte";

  interface Record {
    name: string;
    tally: number;
  }

  let data: Array<Record> = [];

  let naughty: Array<Record> = [];
  let nice: Array<Record> = [];

  onMount(() => {
    async function getData() {
      const res = await fetch(
        "https://advent.sveltesociety.dev/data/2023/day-one.json",
      );
      console.log(data);

      data = await res.json();
      data.map((record: Record) => {
        record.tally > 0 ? nice.push(record) : naughty.push(record);
      });
      console.log(data);
    }

    getData();
  });
</script>

<div class="">
  {#if data.length > 0}
    <div class="flex gap-8">
      <div class="flex flex-col gap-2">
        <p>Naughty List</p>
        {#each naughty as item}
          <p>{item.name}</p>
        {/each}
      </div>
      <div class="flex flex-col gap-2">
        <p>Nice List</p>
        {#each nice as item}
          <p>{item.name}</p>
        {/each}
      </div>
    </div>
  {:else}
    <p>Loading..</p>
  {/if}
</div>
