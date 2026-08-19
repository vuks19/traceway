<script lang="ts">
	import * as Select from '$lib/components/ui/select';
	import Button from '../button/button.svelte';

	type Props = {
		value?: string;
		onSearch: () => void;
		disabled?: boolean;
	};

	let { 
		value = $bindable('all'), 
		onSearch,
		disabled = false 
	}: Props = $props();

	const METHOD_COLORS: Record<string, string> = {
		GET: 'text-sky-600 dark:text-sky-400',
		POST: 'text-emerald-600 dark:text-emerald-400',
		PUT: 'text-amber-600 dark:text-amber-400',
		PATCH: 'text-orange-600 dark:text-orange-400',
		DELETE: 'text-rose-600 dark:text-rose-400',
		HEAD: 'text-violet-600 dark:text-violet-400',
		OPTIONS: 'text-violet-600 dark:text-violet-400'
	};

	const options = [
		{ value: 'all', label: 'All' },
		{ value: 'get', label: 'GET' },
		{ value: 'post', label: 'POST' },
		{ value: 'put', label: 'PUT' },
		{ value: 'patch', label: 'PATCH' },
		{ value: 'delete', label: 'DELETE' },
		{ value: 'head', label: 'HEAD' },
		{ value: 'options', label: 'OPTIONS' },
	];

	const label = $derived(options.find((o) => o.value === value)?.label ?? 'All');
</script>

<div class="flex">
	<Select.Root type="single" bind:value>
		<Select.Trigger class="h-9 w-[120px] rounded border-r-0 shadow-none font-mono text-sm">
			<span class={METHOD_COLORS[label] ?? ''}>{label}</span>
		</Select.Trigger>
		<Select.Content>
			{#each options as option}
				<Select.Item value={option.value} label={option.label} class="font-mono text-sm">
					<span class={METHOD_COLORS[option.label] ?? ''}>{option.label}</span>
				</Select.Item>
			{/each}
		</Select.Content>
	</Select.Root>
	<Button variant="outline" class="h-9 rounded-l-none shadow-none" onclick={onSearch} {disabled}>
		Go
	</Button>
</div>
