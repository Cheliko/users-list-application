<script lang="ts">
  import { onDestroy, createEventDispatcher } from "svelte";

  export let threshold: number = 0;
  export let horizontal: boolean = false;
  export let elementScroll: HTMLElement | null;
  export let hasMore: boolean = true;

  const dispatch = createEventDispatcher();
  let isLoadMore: boolean = false;
  let component: HTMLDivElement | null;

  $: {
    if (component || elementScroll) {
      const element = elementScroll ? elementScroll : component.parentNode;

      element.addEventListener("scroll", onScroll);
      element.addEventListener("resize", onScroll);
    }
  }

  const onScroll = e => {
    const element = e.target;

    const offset = horizontal
      ? e.target.scrollWidth - e.target.clientWidth - e.target.scrollLeft
      : e.target.scrollHeight - e.target.clientHeight - e.target.scrollTop;

    if (offset <= threshold) {
      if (!isLoadMore && hasMore) {
        dispatch("loadMore");
      }
      isLoadMore = true;
    } else {
      isLoadMore = false;
    }
  };

  onDestroy(() => {
    if (component || elementScroll) {
      const element = elementScroll ? elementScroll : component.parentNode;

      element.removeEventListener("scroll", null);
      element.removeEventListener("resize", null);
    }
  });
</script>

<div bind:this={component} style="width:0px" />