<template>
    <q-form @submit.prevent="submitForm" ref="passwordForm">
        <div class="row q-mb-md">
            <q-banner class="bg-grey-3 col">
                <template v-slot:avatar>
                    <q-icon name="account_circle" color="primary"/>
                </template>
                {{ tab | titleCase }} to access your Tasks anywhere
            </q-banner>
        </div>
        <div class="row q-mb-md">
            <q-input
                class="col"
                outlined
                v-model="formData.email"
                label="Email"
                stack-label
                lazy-rules
                :rules="[val => isValidEmailAddress(val) || 'Please enter a valid email address']"
                ref="email"
            />
        </div>
        <div class="row q-mb-md">
            <q-input
                class="col"
                type="password"
                outlined
                v-model="formData.password"
                label="Password"
                stack-label
                :rules="[val => val.length >= 6 || 'Password must be at least 6 characters']"
                lazy-rules
                ref="password"
            />
        </div>
        <div class="row q-mb-md">
            <q-space></q-space>
            <q-btn
                color="primary"
                :label="tab"
                type="submit"
            ></q-btn>
        </div>

    </q-form>
</template>

<script>
    import { mapActions } from 'vuex';

    export default {
        name: "Register",

        props: {
            tab: {
                required: true,
                type: String,
            },
        },

        data() {
            return {
                formData: {
                    email: '',
                    password: '',
                }
            }
        },

        methods: {
            ...mapActions('auth', ['registerUser']),

            submitForm() {
                this.$refs.passwordForm.validate().then(success => {
                    if (success) {
                        if (this.tab === 'login') {
                            console.log('login user');
                        } else {
                            this.registerUser(this.formData);
                        }
                    } else {
                        console.error('could not submit form');
                    }
                });
            },

            isValidEmailAddress(email) {
                return email.match(/^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/);
            }
        },

        filters: {
            titleCase(value) {
                return value.charAt(0).toUpperCase() + value.substr(1);
            }
        }
    }
</script>

<style scoped>

</style>
