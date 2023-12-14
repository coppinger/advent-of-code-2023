<script lang="ts">
  export let name: string;
  export let weight: number;
  export let i: number;
</script>

<button
  class="flex p-8 border-2 border-slate-500 rounded-md gap-8 justify-between cursor-pointer hover:bg-slate-800 transition-all ease-linear hover:border-slate-300"
  id={`item-${i}`}
  on:click
>
  <p>{name}</p>
  <p>{weight}</p>
</button>
