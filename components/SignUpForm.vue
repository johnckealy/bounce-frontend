<template>
	<form @submit.prevent="processForm">
		<p class="is-title has-text-centered">Be the first to know when the new release is out!</p>
		<div class="field">
			<label for="" class="label">Email</label>
			<div class="control has-icons-left">
				<input 
					type="email" 
					class="input" 
					name="email" 
					placeholder="e.g. bobsmith@gmail.com"
					v-model="email">
					<span class="icon is-small is-left">
						<fa :icon="['fas', 'envelope']"/>
					</span>
				</div>
		</div>
		<br>
		<button class="button is-primary is-centered is-fullwidth" type="submit"><strong>Join Early Access</strong></button>
	</form>
</template>


<script>

export default {

  name: 'SignUpForm', 
  data () {
    return {
      email: ''
    }
  },
  methods: {
    processForm: function() {
      console.log({ email: this.email });
      alert('Processing the form for '+this.email);
    }
  }
}

</script>


<style>
</style>
