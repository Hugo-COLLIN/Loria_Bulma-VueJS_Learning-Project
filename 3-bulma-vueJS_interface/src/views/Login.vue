<template>
  <div class="login">
    <section class="hero is-primary is-fullheight">
      <div class="hero-body">
        <div class="container">
          <div class="columns is-centered">
            <div class="column is-5-tablet is-4-desktop is-3-widescreen">
              <form class="box">

                <div class="field has-text-centered">
                  <img :src="require('@/assets/images/logo-bis.png')" width="167">
                </div>

                <div class="field">
                  <label class="label">Email</label>
                  <div class="control has-icons-left">
                    <input v-model="email" :class="{'is-danger': error.email}" class="input" type="email" placeholder="e.g. alexjohnson@gmail.com">
                    <span class="icon is-small is-left">
                                        <i class="fa fa-envelope"></i>
                                    </span>
                  </div>
                  <p class="help is-danger is-left" v-if="error.email">Oops... wrong email!</p>
                </div>

                <div class="field">
                  <label class="label">Password</label>
                  <div class="control has-icons-left">
                    <input v-model="password" :class="{'is-danger': error.password}" class="input" type="password" placeholder="**********">
                    <span class="icon is-small is-left">
                                        <i class="fa fa-lock"></i>
                                    </span>
                  </div>
                  <p class="help is-danger" v-if="error.password">Oops... wrong password!</p>
                </div>

                <div class="field">
                  <label class="checkbox">
                    <input type="checkbox">
                    Remember me
                  </label>
                </div>

                <div class="field">
                  <button class="button is-success" @click.prevent="tryLogin">
                    Login
                  </button>
                </div>

              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      form: {
        email: "",
        password: ""
      },
      error: {
        email: false,
        password: false
      }
    }
  },
  methods: {
    tryLogin() {
      this.resetErrors();

      if (this.form.email !== "user@bulma.com")
        return this.error.email = true;
      if(this.form.password !== "password")
        return this.error.password = true;

      this.resetErrors();
      this.$router.push({name: 'dashboard'});
    },
    resetErrors() {
      this.error.email = false;
      this.error.password = false;
    }
  },
  computed: {
    email: {
      get() {
        return this.form.email;
      },
      set(value) {
        this.form.email = value;
      }
    },
    password: {
      get() {
        return this.form.password;
      },
      set(value) {
        this.form.password = value;
      }
    }
  }
}
</script>

<style lang="sass" scoped>

</style>