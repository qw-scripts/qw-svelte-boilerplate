<script lang="ts">
  import Test from "@components/Test.svelte";
  import { debugData } from "@utils/debugData";

  debugData([
    {
      action: "openUI",
      data: null,
    },
  ]);
</script>

<main>
  <Test />
</main>
