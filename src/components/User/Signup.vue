<template>
  <v-container>
    <v-layout>
      <v-flex xs12 sm6 offset-sm3>
        <v-card>
          <v-card-text>
            <v-container>
              <form @submit.prevent="onSignup">
                <v-layout row>
                  <v-flex xs12>
                    <v-text-field
                      name="email"
                      label="Mail"
                      id="email"
                      v-model="email"
                      type="email"
                      :rules="emailRules"
                      required>
                    </v-text-field>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs12>
                    <v-text-field
                      name="password"
                      label="Password"
                      id="password"
                      v-model="password"
                      :rules="passwordRules"
                      :counter="passwordMinLength"
                      type="password"
                      required>
                    </v-text-field>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs12>
                    <v-text-field
                      name="confirmPassword"
                      label="Confirm Password"
                      id="confirmPassword"
                      v-model="confirmPassword"
                      :rules="confirmPasswordRules"
                      :counter="passwordMinLength"
                      type="password"
                    >
                    </v-text-field>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs12>
                    <v-btn type="submit">Sign up</v-btn>
                  </v-flex>
                </v-layout>
              </form>
            </v-container>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: "signup",
    data() {
      return {
        passwordMinLength: 6,
        email: '',
        emailRules: [
          v => !!v || 'E-mail is required',
          v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
        ],
        password: '',
        passwordRules: [
          v => !!v || 'Password is required',
          v => (v && v.length >= this.passwordMinLength) || `Password must be at least ${this.passwordMinLength} characters`
        ],
        confirmPassword: '',
        confirmPasswordRules: [
          v => !!v || 'Confirm Password is required',
          v => (v && v.length >= this.passwordMinLength) || `Password must be at least ${this.passwordMinLength} characters`,
          () => (this.password === this.confirmPassword) || 'Passwords do not match'
        ]
      }
    },
    computed: {
      user () {
        return this.$store.getters.user
      }
    },
    watch: {
      user (value) {
        if (value !== null && value !== undefined)
          this.$router.push('/')
      }
    },
    methods: {
      onSignup() {
        //Vuex
        this.$store.dispatch('signUserUp', {email: this.email, password: this.password});
        //TODO
        // .then()
        // .catch()
      }
    }
  }
</script>

<style scoped>

</style>