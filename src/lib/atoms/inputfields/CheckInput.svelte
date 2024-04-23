<script>
    export let inputType = "checkbox"
	export let checkName;
	export let checkId;
	export let options;
    export let isRequired;
    export let data;

</script>

{#each data.tag as tag}
<span class="tag-title">{tag.title}</span>
{#each data.sub_tag as sub}
{#if tag.sub_tag && tag.sub_tag.includes(sub.id)}
<label>
    <input type="{inputType}" name="{checkName}" id="{checkId}" required={isRequired} value={sub.id}>
    <span>{sub.title}</span>
</label>
{/if}

{/each}
{/each}
<style>
    	input {
		border: solid 2px var(--border-color, #fff);
		padding: var(--unit-small) 0.8rem;
		background-color: var(--input-bg, var(--color-hva-navy));
		color: var(--input-color, #fff);
	}

	input::placeholder {
		color: rgba(255, 255, 255, 0.4);
		font-style: italic;
	}

	input:focus {
		outline: var(--btn-focus, var(--color-hva-pink)) dashed 2px;
	}

    input:user-invalid {
        border: 2px solid red;
        animation: shake 0.2s ease-in-out 0s 2;   
    }

    input::before{
        content: " ";
    }
    
    input:user-invalid + span::before {
        content: "✖";
        color: red;
    }

    .tag-title{
        font-weight: bold;
    }

    @media (min-width: 170rem) {
        input, input::placeholder{
            font-size: var(--input-font-large);
            height: var(--input-height-large);
        }
    }

    @keyframes shake {
        0% { margin-left: 0rem; }
        25% { margin-left: 0.5rem; }
        75% { margin-right: -0.5rem; }
        100% { margin-left: 0rem; }
    }

	@media (prefers-reduced-motion) {
		input:user-invalid {
        animation: none;
    }
    }
</style>