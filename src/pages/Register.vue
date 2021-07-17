<template>
  <div class="login-page">
    <div class="sec-1">
      <div class="sub-sec">
        <!-- <a href="index.html"><img src="./assets/images/logo/white.svg" alt="" class="logo"></a> -->
        <h1>Welcome</h1>
        <a href="index.html" class="btn btn-white">
          <i class="fas fa-home"></i> Go Back to Home
        </a>
      </div>
    </div>
    <div class="sec-2">
      <form class="register-form" name="form" @submit.prevent="handleRegister">
        <!-- <a href="index.html"><img src="./assets/images/logo/Red.svg" alt="" class="logo"></a> -->
        <h1>Become part of our community</h1>
        <div class="form-section">
          <div class="form-field">
            <label for="username">Username</label>
            <input
              type="text"
              name="username"
              placeholder="Enter your username"
              v-validate="'required|min:3|max:20'"
            />
            <div
              v-if="submitted && errors.has('username')"
              class="alert-danger"
            >
              {{ errors.first('username') }}
            </div>
          </div>

          <div class="form-field">
            <label for="email">Email</label>
            <input
              type="email"
              name="email"
              id=""
              placeholder="John.snow@gmail.com"
              v-validate="'required|email|max:50'"
            />

            <div v-if="submitted && errors.has('email')" class="alert-danger">
              {{ errors.first('email') }}
            </div>
          </div>

          <div class="form-field">
            <label for="password">Password</label>
            <input
              type="password"
              name="password"
              placeholder="Password"
              v-validate="'required|min:6|max:40'"
            />

            <div
              v-if="submitted && errors.has('password')"
              class="alert-danger"
            >
              {{ errors.first('password') }}
            </div>
          </div>

          <button type="submit" class="btn btn-green">Register Now</button>
          <div class="alt">
            <p>
              Already have an account?
              <!-- <a href="login.html">Sign in</a> -->
              <router-link to="/login">Sign In</router-link>
            </p>
          </div>
        </div>
        <a href="index.html" class="btn btn-white home-btn">
          <i class="fas fa-home    "></i> Go Back to Home
        </a>
      </form>
      <div v-if="message" class="alert">
        {{ message }}
      </div>
    </div>
  </div>
</template>

<script>
// import User from '../models/user';

export default {
  name: 'Register',
  data() {
    return {
      // user: new User('', '', ''),
      submitted: false,
      successful: false,
      message: '',
    };
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  mounted() {
    if (this.loggedIn) {
      this.$router.push('/profile');
    }
  },
  methods: {
    handleRegister() {
      //       this.message = '';
      //       this.submitted = true;
      //       this.$validator.validate().then((isValid) => {
      //         if (isValid) {
      //           this.$store.dispatch('auth/register', this.user).then(
      //             (data) => {
      //               this.message = data.message;
      //               this.successful = true;
      //             },
      //             (error) => {
      //               this.message =
      //                 (error.response && error.response.data) ||
      //                 error.message ||
      //                 error.toString();
      //               this.successful = false;
      //             }
      //           );
      //         }
      //       });
      console.log('I am awesome');
    },
  },
};
</script>

<style>
/* start of the login page styles  */

.login-page {
  display: flex;
  width: 100vw;
}

.login-page .sec-1 {
  width: 25vw;
  height: inherit;
  min-height: 100vh;
  /* background: url('../assets/login-bg.jpg'); */
  background-size: cover;
  background-position: center;
}

.login-page .sec-1 .sub-sec {
  width: 100%;
  height: 100%;
  min-height: 100vh;
  background: linear-gradient(0deg, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2));
  padding: 6rem 0;
  text-align: center;
  display: grid;
  justify-content: center;
  align-content: space-between;
}

.login-page .sec-1 .sub-sec .btn,
.login-page .sec-1 .sub-sec .logo {
  width: 100%;
  margin: 0 auto;
}

.login-page .sec-1 .sub-sec h1 {
  color: #fff;
  font-size: 45px;
}

.login-page .sec-2 {
  width: 75vw;
  height: 100vh;
  overflow-y: scroll;
}

.login-page .login-form {
  width: 600px;
  height: fit-content;
  margin: 0 auto;
  margin-top: 15vh;
}

.login-page .register-form {
  width: 80%;
  height: fit-content;
  margin: 0 auto;
  margin-top: 10vh;
}

.login-page .register-form .logo,
.login-page .login-form .logo {
  display: none;
}

.login-page h1 {
  margin-bottom: 2rem;
}

.login-page .login-remember {
  width: 100%;
  height: fit-content;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 2rem;
}

.login-page .login-remember a {
  color: var(--primary-color);
}

.login-page .btn {
  margin-top: 1rem;
}

.login-page .form-flex {
  gap: 1rem;
}

.login-page .btn.google {
  border: 2px solid var(--gray);
  padding: 1rem 0.5rem !important;
  color: var(--text);
  background-color: #fff;
}

.login-page .btn.google:hover {
  background-color: #eee;
}

.login-page .btn.facebook {
  border: 2px solid var(--gray);
  padding: 1rem 0.5rem !important;
  color: #fff;
  background-color: #4267b2;
}

.login-page .btn.facebook:hover {
  background-color: #24417a;
}

.login-page .alt {
  width: 100%;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
}

.login-page .alt a {
  color: var(--primary-color);
}

.login-page .alt a:hover {
  text-decoration: underline;
}

.login-page .home-btn {
  display: none;
}

@media screen and (min-width: 768px) and (max-width: 1023px) {
  .login-page .sec-1 {
    display: none;
  }
  .login-page .sec-2 {
    width: 100%;
  }
  .login-page .register-form .logo,
  .login-page .login-form .logo {
    display: block;
    margin-bottom: 3rem;
  }
  .login-page .home-btn {
    display: block;
    width: 300px;
    display: flex;
    justify-content: center;
    margin: 2rem auto;
  }
}

@media screen and (max-width: 767px) {
  .login-page {
    display: flex;
    width: 100vw;
  }
  .login-page .sec-1 {
    display: none;
  }
  .login-page .sec-2 {
    width: 100vw;
    height: auto;
  }
  .login-page .login-form {
    width: 90vw;
    margin-top: 5vh;
  }
  .login-page .register-form {
    width: 90%;
  }
  .login-page .register-form .logo,
  .login-page .login-form .logo {
    display: block;
    width: 65vw;
    margin-bottom: 2rem;
  }
  .login-page h1 {
    margin-bottom: 2rem;
    font-size: 35px;
  }
  .login-page .login-remember a {
    color: var(--primary-color);
  }
  .login-page .home-btn {
    display: block;
    width: 300px;
    display: flex;
    justify-content: center;
    margin: 2rem auto;
  }
}

/* end of the login page styles  */
</style>
