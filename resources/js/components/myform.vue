<template>
    <form @submit.prevent="register">
        <div class="row mb-3">
            <label for="name" class="col-md-4 col-form-label text-md-end">{{ __('Name') }}</label>
            <div class="col-md-6">
                <input id="name" v-model="formData.name" type="text" class="form-control" :class="{ 'is-invalid': errors.name }" required autofocus>
                <span class="invalid-feedback" role="alert" v-if="errors.name">
          <strong>{{ errors.name }}</strong>
        </span>
            </div>
        </div>

        <div class="row mb-3">
            <label for="email" class="col-md-4 col-form-label text-md-end">{{ __('Email Address') }}</label>
            <div class="col-md-6">
                <input id="email" v-model="formData.email" type="email" class="form-control" :class="{ 'is-invalid': errors.email }" required>
                <span class="invalid-feedback" role="alert" v-if="errors.email">
          <strong>{{ errors.email }}</strong>
        </span>
            </div>
        </div>

        <div class="row mb-3">
            <label for="password" class="col-md-4 col-form-label text-md-end">{{ __('Password') }}</label>
            <div class="col-md-6">
                <input id="password" v-model="formData.password" type="password" class="form-control" :class="{ 'is-invalid': errors.password }" required>
                <span class="invalid-feedback" role="alert" v-if="errors.password">
          <strong>{{ errors.password }}</strong>
        </span>
            </div>
        </div>

        <div class="row mb-3">
            <label for="password-confirm" class="col-md-4 col-form-label text-md-end">{{ __('Confirm Password') }}</label>
            <div class="col-md-6">
                <input id="password-confirm" v-model="formData.password_confirmation" type="password" class="form-control" required>
            </div>
        </div>

        <div class="row mb-0">
            <div class="col-md-6 offset-md-4">
                <button type="submit" class="btn btn-primary">{{ __('Register') }}</button>
            </div>
        </div>
    </form>
</template>

<script>
export default {
    name: "myform",
    props: {
        csrfToken: String, // CSRF token received as a prop
    },
    data() {
        return {
            formData: {
                name: '',
                email: '',
                password: '',
                password_confirmation: '',
            },
            errors: {},
        };
    },
    methods: {
        async register() {
            this.errors = {};
            try {
                const response = await fetch('/api/register', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'X-CSRF-TOKEN': this.csrfToken, // Attach CSRF token to headers
                    },
                    body: JSON.stringify(this.formData),
                });

                if (response.ok) {
                    // Registration successful, handle accordingly
                } else {
                    const responseData = await response.json();
                    this.errors = responseData.errors || {};
                }
            } catch (error) {
                console.error('An error occurred:', error);
            }
        },
    },
}
</script>

<style scoped>

</style>
