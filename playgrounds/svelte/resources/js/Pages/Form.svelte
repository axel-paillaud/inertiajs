<script context="module">
  export { default as layout } from '../Components/Layout.svelte'
</script>

<script>
  import { useForm } from '@inertiajs/svelte'

  export let appName

  let form = useForm('NewUser', {
    name: '',
    company: '',
    role: '',
  })

  function submit() {
    $form.post('/form', {preserveScroll: true, preserveState: false })
  }
</script>

<svelte:head>
  <title>Form - {appName}</title>
</svelte:head>

<h1 class="text-3xl">Form</h1>

<form on:submit|preventDefault={submit} class="mt-6 max-w-md space-y-4 overflow-scroll max-h-80">
  {#if $form.isDirty}
    <div class="my-5 rounded border border-amber-100 bg-amber-50 p-3 text-amber-800">There are unsaved changes!</div>
  {/if}
  <div>
    <label class="block" for="name">Name:</label>
    <input
      type="text"
      bind:value={$form.name}
      id="name"
      class="mt-1 w-full appearance-none rounded border px-2 py-1 shadow-sm"
    />
    {#if $form.errors.name}
      <div class="mt-2 text-sm text-red-600">{$form.errors.name}</div>
    {/if}
  </div>
  <div>
    <label class="block" for="company">Company:</label>
    <input
      type="text"
      bind:value={$form.company}
      id="company"
      class="mt-1 w-full appearance-none rounded border px-2 py-1 shadow-sm"
    />
    {#if $form.errors.company}
      <div class="mt-2 text-sm text-red-600">{$form.errors.company}</div>
    {/if}
  </div>
  <div>
    <label class="block" for="role">Role:</label>
    <select bind:value={$form.role} id="role" class="mt-1 w-full appearance-none rounded border px-2 py-1 shadow-sm">
      <option />
      <option>User</option>
      <option>Admin</option>
      <option>Super</option>
    </select>
    {#if $form.errors.role}
      <div class="mt-2 text-sm text-red-600">{$form.errors.role}</div>
    {/if}
  </div>
  <div class="flex gap-4">
    <button type="submit" disabled={$form.processing} class="rounded bg-slate-800 px-6 py-2 text-white">
      Submit
    </button>
    <button type="button" on:click={() => $form.reset()}>Reset</button>
  </div>
  <div>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas eu justo ac purus molestie dignissim. Nam quis enim finibus, interdum nulla sed, mollis magna. Mauris pretium aliquet venenatis. Nullam porta sodales pellentesque. Donec sagittis, neque quis placerat vestibulum, nulla felis ultricies lorem, ac malesuada risus mi a libero. Nulla vehicula eleifend lectus, tristique egestas sem fringilla non. Mauris sodales gravida nisi eget finibus. Mauris condimentum leo vel magna tristique suscipit. Pellentesque vulputate porta dolor, ac vestibulum ipsum sagittis a. Maecenas eleifend quam tortor, vel convallis est rhoncus sed. Suspendisse ipsum purus, varius quis sem luctus, molestie laoreet purus. Pellentesque egestas, diam eu molestie mollis, nulla lorem vestibulum dolor, id posuere est eros id orci.
  </div>
</form>
