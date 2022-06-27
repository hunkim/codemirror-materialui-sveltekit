<script lang="ts">
	import Button, { Label, Icon } from '@smui/button';
  import CodeMirror from '../lib/CodeMirror.svelte';
  import { syntaxHighlighting, defaultHighlightStyle } from '@codemirror/language';
  import {python} from '@codemirror/lang-python';

  let currentValue = "Hello";
	let clicked = 0;

	function handleClick(event: CustomEvent | MouseEvent) {
		event = event as MouseEvent;
		if (event.button === 0) {
			clicked++;
		}
	}

	function reset() {
		clicked = 0;
	}
</script>

<Button on:mousedown={handleClick}>
	<Icon class="material-icons">thumb_up</Icon>
	<Label>Click Me</Label>
</Button>
<p class="mdc-typography--body1">
	{#if clicked}
		You've clicked the button {clicked} time{clicked === 1 ? '' : 's'}. You can
		<a on:click={reset} href="{null}">reset it</a>.
	{:else}
		<span class="grayed">You haven't clicked the button.</span>
	{/if}
</p>

<CodeMirror extensions={[python(), syntaxHighlighting(defaultHighlightStyle)]} basicSetup bind:currentValue initialValue="def func():
print('Hello CodeMirror')"/>
{#if currentValue}
  <p class="mdc-typography--body1">
    The current value is: <code>{currentValue}</code>
  </p>
{/if}

<style>
	.grayed {
		opacity: 0.6;
	}

  #CodeMirror {
    border: 1px solid #eee;
    height: auto;
  }
</style>
