<script>
	import { onMount } from "svelte";
	export let post;
	export let index;
	const formatPostTags = (tags) => {
		if (tags.length === 1) {
			return tags[0];
		} else {
			return tags.join(", ");
		}
	};
	let postNode;

	const callback = function (entries) {
		entries.forEach((entry) => {
			if (entry.isIntersecting) {
				entry.target.classList.remove("opacity-0", "translate-y-16");
			}
		});
	};

	onMount(() => {
		const observer = new IntersectionObserver(callback);
		observer.observe(postNode);
	});
</script>

<style>
	.teaser-img {
		transition: all 0.5s ease;
	}

	.teaser:hover .teaser-img {
		transform: scale(1.015);
	}
</style>

<li
	class="card transform opacity-0 translate-y-16 flex flex-col rounded-lg
		shadow-lg overflow-hidden teaser"
	bind:this={postNode}
	style="--transition-order: {index + 2}">
	<div class="flex-shrink-0">
		<img
			class="h-48 w-full object-cover teaser-img"
			src="post_images/{post.image}"
			alt="" />
	</div>
	<div class="flex-1 bg-white p-6 flex flex-col justify-between">
		<div class="flex-1">
			<!-- <p class="text-sm leading-5 font-medium text-indigo-600">
        <a href="blog/" class="hover:underline"> Blog </a>
			</p> -->
			<div class="text-red-400 uppercase font-bold text-xs mb-1 space-x-4">
				{#each post.tags as tag}<span>{tag}</span>{/each}
			</div>
			<a href="blog/{post.slug}" class="flex flex-col">
				<h3 class="mt-2 text-2xl leading-7 font-semibold text-gray-900 flex-1">
					{post.title}
				</h3>
				<p class="mt-3 text-base leading-6 text-gray-600">{post.description}</p>
			</a>
		</div>
		<div class="mt-3 flex text-sm leading-5 text-gray-600">
			<time datetime="2020-03-16"> {post.date} </time>
			<span class="mx-1"> &middot; </span>
			<span> {post.readingTime} </span>
		</div>
	</div>
</li>
<!-- <li
  class="card transform opacity-0 translate-y-16"
  bind:this={postNode}
  style="--transition-order: {index + 2}">

  <a
    class="flex bg-white shadow-lg transition-all duration-200 hover:shadow-xl
      transform hover:-translate-y-1 focus:translate-y-0 focus:shadow rounded-lg
      cursor-pointer group"
    rel="prefetch"
    href="blog/{post.slug}">
    <div class="flex flex-col flex-1 px-4 sm:px-6 md:px-8 py-4 sm:py-5 md:py-6">
      <div class="text-red-400 uppercase font-bold text-xs mb-1">
        {formatPostTags(post.tags)}
      </div>
      <div
        class="text-gray-800 font-bold text-lg lg:text-xl xl:text-2xl mb-1
          flex-1">
        {post.title}
      </div>
      <div class="text-gray-500 text-xs">{post.date}</div>
    </div>
    <div class="flex items-center pr-4">
      <svg
        class="w-6 h-6 transform transition-transform duration-200 ease-out
          group-hover:translate-x-2 group-hover:scale-125"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        viewBox="0 0 24 24"
        stroke="currentColor">
        <path d="M9 5l7 7-7 7" />
      </svg>
    </div>
  </a>
</li> -->
