<script>
  import Navigation from "../components/Navigation.svelte";
  export let segment;
</script>

{#if segment === 'mastering-coding-mindset' || segment === 'sales-page'}
  <div class="font-inter bg-gray-200">
    <slot />
  </div>
{:else}
  <!-- border-t-4 border-red-400 -->
  <div class="font-inter bg-gray-100">
    {#if segment !== 'confirm-book'}
      <div
        class="bg-red-400 text-base py-4 sm:text-lg md:text-xl font-semibold
          text-white sm:hidden">
        <div class="max-w-7xl w-full mx-auto px-4 sm:px-12 text-center">
          <span class="mb-2">
            I wrote a book on improving your dev skills and landing a job!
          </span>
          <a
            href="/mastering-coding-mindset"
            class="font-bold text-white underline">
            Learn more →
          </a>
        </div>
      </div>
      <Navigation {segment} />
    {/if}
    <main
      class="max-w-7xl w-full mx-auto px-4 sm:px-12 pb-16 pt-12 md:pt-24
        lg:py-32 xl:pt-48 text-gray-800 min-h-screen">
      <slot />
    </main>
  </div>
{/if}
