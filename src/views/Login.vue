<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-6 col-lg-6 col-xl-6">
                <div class="card shadow-lg o-hidden border-0 my-5">
                    <div class="card-body p-0">
                        <div class="row">
                            <div class="col-lg-12">
                                <div class="p-5">
                                    <div class="text-center">
                                        <h4 class="text-dark mb-4">Welcome Back!</h4>
                                    </div>
                                    <form class="user">
                                        <div class="form-group">
                                            <input v-model="form.email" class="form-control form-control-user" type="email" id="exampleInputEmail" aria-describedby="emailHelp" placeholder="Enter Email Address..." name="email">
                                        </div>
                                        <div class="form-group">
                                            <input v-model="form.password" class="form-control form-control-user" type="password" id="exampleInputPassword" placeholder="Password" name="password">
                                        </div>
                                        <button @click.prevent="login" class="btn btn-primary btn-block text-white btn-user" type="submit">
                                            Login
                                        </button>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
	name: "Login",
	props: {},
	data() {
		return {
            form: {}
        };
	},
	beforeMount() {
	},
	methods: {
        login(){
            if(!this.form || !this.form.email || !this.form.password){
                alert("All fields must be filled!")
                return;
            }
            this.axios.post("http://localhost/login", this.form)
			.then((response) =>{
				console.log(response.data.token);
			})
			.catch((error) =>{
				// handle error
				console.log(error);
			})
        }
	}
};
</script>

<style >
    body{
        background-color: #f3f3f3 !important;
    }
</style>
