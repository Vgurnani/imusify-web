<template>
  <div class="wrapform">
    <h1 class="heading">Sign in to imusify</h1>
    <p class="subheading">In a consequat mi. Etiam sit amet diam in diam ullamcorper consequat.
      Maecenas pellentesque mauris augue, in scelerisque lectus imperdiet et. Nullam ultricies,
      eros quis maximus.
    </p>
    <div class="social-icons">
      <a  href="#">
        <icon name="facebook" />
      </a>
      <a  href="#">
        <icon name="linkedin" />
      </a>
      <a  href="#">
        <icon name="cloud" />
      </a>
    </div>
    <div class="or-ui"><span>OR</span></div>
    <div>
      <form @submit.prevent="signupPage()">
        <div class="form-group">
          <label class="control-label">Email address</label>
          <input type="text" id="username" class="form-control"
            placeholder="Enter your username" v-model="credentials.username">
        </div>
        <div class="form-group">
          <label class="control-label">Password</label>
          <input type="password" id="password" class="form-control"
            placeholder="Enter your password" v-model="credentials.password">
        </div>
        <div class="form-group">
          <div class="checkbox">
            <label><input type="checkbox"/> <span></span> keep me signed in</label>
          </div>
        </div>
        <div class="cta dubble">
          <button class="button">LOGIN</button>
          <button class="signupbutton" >SIGNUP</button>
        </div>
      </form>
    </div>
    <div class="status" v-if="status">
      {{status}}
    </div>
  </div>
</template>

<script>
import Icon from '@/components/Icon.vue';
import { mapActions } from 'vuex';
import * as types from '../store/types';

export default {
  name: 'login',
  components: {
    Icon,
  },
  data() {
    return {
      credentials: {
        username: '',
        password: '',
      },
      status: '',
    };
  },

  methods: {
    ...mapActions({
      login: types.ACCOUNTS_USER,
    }),
    onSubmit() {
      this.login(this.credentials)
        .then(() => {
          this.$router.replace(this.$route.query.redirect || '/');
        });
    },
    signupPage() {
      this.$router.push('/signupnext');
    },
  },
};
</script>

