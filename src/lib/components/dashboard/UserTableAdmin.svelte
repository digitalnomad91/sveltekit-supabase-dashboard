<script lang="ts">
	import Time from 'svelte-time';
	import { TrashIcon } from 'svelte-feather-icons';
	import type { AnyObject } from 'chart.js/types/basic';

	export let users: Array<any>;
	// console.log(users)

	let current_user: AnyObject = {};

	function updateUser(usr: AnyObject) : any{
		// console.log(usr);
		current_user = usr;
		// console.log(current_user);
	}
</script>

<table class="table w-full">
	<thead>
		<tr>
			<th>email</th>
			<th>organization</th>
			<th>role</th>
			<th>created</th>
			<th>last sign in</th>
		</tr>
	</thead>
	<tbody>
		{#each users as user}
			<tr>
				<td>
					{user.email}
				</td>
				<td>
					{user.app_metadata.org}
				</td>
				<td>
					<div
						class="badge"
						class:badge-secondary={user.app_metadata.role === 'user'}
						class:badge-warning={user.app_metadata.role === 'admin'}
						class:badge-accent={user.app_metadata.role === 'super'}
					>
						{user.app_metadata.role}
					</div>
				</td>

				<td>
					<Time timestamp={user.created_at} />
				</td>
				<td>
					<Time timestamp={user.last_sign_in_at} />
				</td>
				<td>
					<label
						on:click={updateUser(user)}
						for="delete-modal"
						class="btn btn-ghost btn-circle modal-button"
					>
						<TrashIcon class="stroke-warning" />
					</label>
				</td>
			</tr>
		{/each}
	</tbody>
	<!-- foot -->
	<tfoot />
</table>

<!-- Put this part before </body> tag -->
<input type="checkbox" id="delete-modal" class="modal-toggle" />
<div class="modal">
	<div class="modal-box">
		<h3 class="font-bold text-lg">Are you sure?</h3>
		<p class="py-4">You are going to delete <span class="font-bold">{current_user?.email}</span></p>
		<form method="POST" action="?/delete">
			<input name="user" value={current_user?.id} hidden />
			<div class="modal-action">
				<label for="delete-modal" class="btn">CANCEL</label>
				<button class="btn btn-warning">DELETE</button>
			</div>
		</form>
	</div>
</div>
