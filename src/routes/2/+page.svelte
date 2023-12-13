<script lang="ts">
  import { Button } from "$lib/components/ui/button";

  let cookieCount = 0;

  function eatCookie() {
    cookieCount++;
  }

  function unEatCookie() {
    cookieCount--;
  }

  function purgeStomach() {
    cookieCount = 0;
  }
</script>

{cookieCount}

<Button
  on:click={() => {
    unEatCookie();
  }}>Uneat</Button
>
<Button
  on:click={() => {
    eatCookie();
  }}>Eat</Button
>
<Button
  on:click={() => {
    purgeStomach();
  }}>Purge</Button
>
