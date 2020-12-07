<template>
	<v-container>
		<v-card
			class="my-10"
			elevation="10"
			rounded="xl"
			width="100%"
		>
			<v-container
				class="mx-10 text-center"
			>
				<input-form />
			</v-container>
		</v-card>
	</v-container>
</template>

<script>
  import InputForm from './InputForm.vue'
	export default {
    components: {
      InputForm,
    },
	}
</script>
