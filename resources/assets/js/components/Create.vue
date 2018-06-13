<template>
	<div>
		<h2>Add New User</h2>
		<form action="/users" method="POST" class="form-horizontal">
			<div class="form-group">
				<label for="name" class="control-label col-sm-2">Name</label>
				<div class="col-sm-10">
					<input type="text" class="form-control" id="name" placeholder="Enter Name" name="name" v-model="name">
					<span v-if="errors.name" class="error">{{errors.name[0]}}</span>
				</div>
			</div>

			<div class="form-group">
				<label for="name" class="control-label col-sm-2">Email</label>
				<div class="col-sm-10">
					<input type="email" class="form-control" id="email" placeholder="Enter Email" name="email" v-model="email">
					<span v-if="errors.email" class="error">{{errors.email[0]}}</span>
				</div>
			</div>

			<div class="form-group">
				<label for="name" class="control-label col-sm-2">Password</label>
				<div class="col-sm-10">
					<input type="password" class="form-control" id="pwd" placeholder="Enter Password" name="password" v-model="password">
					<span v-if="errors.password" class="error">{{errors.password[0]}}</span>
				</div>
			</div>

			<div class="form-group">
				<div class="col-sm-offset-2 col-sm-10">
					<button type="button" class="btn btn-default" v-on:click="addNewUser()">Save</button>
				</div>
			</div>
		</form>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				name: '',
				email: '',
				password: '',
				errors:[]
			}
		},
		methods: {
			addNewUser(){
				this.errors = []

				//passing the data to API
				
				axios.post('/api/users', {
					name: this.name,
					email: this.email,
					password: this.password,
				}).then(response => {
					console.log(response)

					this.name = ''
					this.email = ''
					this.password = ''
				}).catch(error => {
					if(error.response.status == 422) {
						this.errors = error.response.data.errors
					}
				})
			}
		}
	}

</script>