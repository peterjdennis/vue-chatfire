<template>
  <div>

    <div class="ui middle aligned center aligned grid login_container">
      <div class="column">
        <h2 class="ui pink image header">
          <div class="content">
            #Practice::vChatFire
          </div>
        </h2>

        <form class="ui large form" :class="{'error' : hasErrors}">
          <div class="ui stacked segment">

            <div class="field">
              <div class="ui left icon input">
                <i class="mail icon"></i>
                <input type="email" name="email" placeholder="email" v-model.trim="email" required>
              </div>
            </div>


            <div class="field">
              <div class="ui left icon input">
                <i class="lock icon"></i>
                <input type="password" name="password" placeholder="Password"
                       v-model.trim="password" required>
              </div>
            </div>

            <div class="ui fluid large teal button" @click.prevent="login" :class="{'loading':isLoading}">เข้าสู่ระบบ
            </div>
          </div>

          <div class="ui error message" v-if="hasErrors">
            <p v-for="error in errors">{{error}}</p>
          </div>

        </form>

        <div class="ui message">
          ลงทะเบียน
          <router-link to="/register">Registration</router-link>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

    import firebase from 'firebase'

    export default{
        name: 'login',
            computed: {
            hasErrors(){
              return this.errors.length > 0;
            }
        },
        data(){
            return{

              email: '', password: '', errors: [], isLoading: false, hasError: []

            }
        },
        methods: {
          login(){
            console.log('log in');
            this.errors = [];
            if(this.isFormValid()){
                this.isLoading = true;
                firebase.auth().signInWithEmailAndPassword(this.email, this.password)
                .then(user => {

                      this.$store.dispatch('setUser', user)
                      this.$router.push('/')

                }).catch(error => {

                  this.errors.push(error.message);
                  this.isLoading = false;
                })
            }
          },
          isFormValid(){
            if(this.email.length > 0 && this.password.length > 0){
              return true;
            }
            return false;
          }
        }
    }

</script>

<style scope>
  .login_container{
    margin-top: 40px;
  }
  .column{
    max-width: 450px;
  }

</style>
