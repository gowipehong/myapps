<script>
  import SvelteMarkdown from 'svelte-markdown'
  import humanize from 'humanize-plus'
  import { getUserId } from '../../../utils/auth'
  export let data
</script>

<div class="m-10 ">
  <div class="flex">
      <div class="flex-1">
          <h1 class="text-3xl font-extrabold">{data.job.title}</h1>
          <p class="text-xl">{data.job.employer}</p>
      </div>
      {#if data.job.user === getUserId()}
          <a class="btn btn-outline btn-info normal-case" href="/jobs/{data.job.id}/update">Edit</a>
      {/if}
  </div>

  <div class="flex flex-col md:flex-row w-full mt-8">
      <div class="basis-2/3 prose max-w-none w-full">
          <h2 class="text-xl font-thin">Description</h2>
          <SvelteMarkdown source={data.job.description} />
          <div class="mt-6" />
          <h2 class="text-xl font-thin">Requirements</h2>
          <SvelteMarkdown source={data.job.requirements} />
          <div class="mt-6" />
          <h2 class="text-xl font-thin">How to Apply?</h2>
          <p>{data.job.applicationInstructions}</p>
      </div>
      <div class="basis-1/3 md:ml-4 mt-6 md:mt-0">
          <h2 class="text-xl font-thin">Location</h2>
          <p>{data.job.location}</p>
          <div class="mt-6" />
          <h2 class="text-xl font-thin">Salary Range</h2>
          <p>
              USD {humanize.formatNumber(data.job.minAnnualCompensation)} - USD {humanize.formatNumber(
                  data.job.maxAnnualCompensation
              )}
          </p>
      </div>
  </div>
</div>