<script lang="ts">
	import type { PageData } from '../../../../.svelte-kit/types/src/routes/auth/dashboard_/$types';

	export let data: PageData;
	$: ({ testTable, user } = data);
</script>

<div class="block">
	<p>Protected content for {user.email}</p>
	<p>server-side fetched data with RLS:</p>
	<pre>{JSON.stringify(testTable, null, 2)}</pre>
</div>
<div class="block">
	<p>user:</p>
	<pre>{JSON.stringify(user, null, 2)}</pre>
</div>
