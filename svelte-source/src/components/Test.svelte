<script lang="ts">
  import { useNuiEvent } from "@hooks/useNuiEvent";
  import { cubicOut, cubicIn } from "svelte/easing";
  import { fade } from "svelte/transition";
  import { Router, Link, Route } from "svelte-routing";
  import Home from "../layouts/home/Home.svelte";
  import About from "../layouts/about/About.svelte";
  import { onMount } from "svelte";
  import { useFetchNui } from "@hooks/useFetchNui";

  let show = false;

  useNuiEvent("openUI", () => {
    show = true;
  });

  const handleClose = () => {
    show = false;
    useFetchNui("boilerplate:closeUI");
  };

  onMount(() => {
    const keyHandler = (e: KeyboardEvent) => {
      if (["Escape"].includes(e.code)) handleClose();
    };

    window.addEventListener("keydown", keyHandler);

    return () => window.removeEventListener("keydown", keyHandler);
  });
</script>

<main>
  {#if show}
    <div
      class="container bg-neutral-900 text-neutral-50"
      in:fade={{ duration: 400, easing: cubicOut }}
      out:fade={{ duration: 400, easing: cubicIn }}
    >
      <Router>
        <nav class="p-2">
          <Link to="/">Home</Link>
          <Link to="about">About</Link>
        </nav>
        <div class="p-2">
          <Route path="/" component={Home} />
          <Route path="/about" component={About} />
        </div>
      </Router>
    </div>
  {/if}
</main>

<style>
  .container {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    border-radius: 5px;
    min-height: 85%;
    min-width: 85%;
    user-select: none;
  }
</style>
