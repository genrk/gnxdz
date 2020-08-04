<template>
  <div>
    <div v-if="logged" :class="ismobile ? 'content mx-1 mt-2 px-0' : 'content ml-5 mt-2 mr-5 pl-5 pr-5'">
      <h1 class="title has-text-centered has-text-weight-bold has-text-white">Settings</h1>
      <div class="loading">
        <loading :active.sync="loading" :can-cancel="false" :is-full-page="fullpage"></loading>
      </div>
      <div class="columns has-text-white is-centered is-multiline">
        <div class="column is-two-thirds">
          <div class="box has-background-light">
            <h3 class="title has-text-centered has-text-weight-bold has-text-info-dark">Seus detalhes</h3>
            <div class="columns is-vcentered is-centered is-multiline is-mobile">
              <div class="column has-text-centered is-full">
                <figure class="image is-128x128 is-inline-block">
                  <img class="is-rounded" :src="avatar" @click="alerts('Avatar em desenvolvimento')">
                </figure>
              </div>
              <div class="column is-three-fifths">
                <p class="subtitle">Nome</p>
              </div>
              <div class="column is-two-fifths">
                <p class="subtitle has-text-weight-bold">{{ user.name }}</p>
              </div>
              <div class="column is-three-fifths">
                <p class="subtitle">Email</p>
              </div>
              <div class="column is-two-fifths">
                <p class="subtitle has-text-weight-bold">{{ user.email }}</p>
              </div>
              <div class="column is-three-fifths">
                <p class="subtitle">Classe</p>
              </div>
              <div class="column is-two-fifths">
                <p class="subtitle has-text-weight-bold">{{ user.role }}</p>
              </div>
              <div v-if="!admin && !superadmin || admin && !superadmin" class="column is-three-fifths">
                <p class="subtitle">Requisitar mais poderes</p>
              </div>
              <div v-if="!admin && !superadmin || admin && !superadmin" class="column has-text-centered is-two-fifths">
                <button class="button is-success" @click="gotoPage('/request/', 'settings')">
                  <span class="icon is-small">
                    <i class="fas fa-user-shield"></i>
                  </span>
                  <span>Requesitar</span>
                </button>
              </div>
              <div v-if="admin && superadmin" class="column has-text-centered is-full">
                <p class="subtitle has-text-warning-dark has-text-weight-bold">Você tem o máximo de acessos para este site./p>
              </div>
              <div class="column is-three-fifths">
                <p class="subtitle">Último Token Issue Date</p>
              </div>
              <div class="column is-two-fifths">
                <p class="subtitle has-text-weight-bold">{{ token.issuedate | moment("dddd, MMMM Do YYYY [at] hh:mm A") }}</p>
              </div>
              <div class="column is-three-fifths">
                <p class="subtitle">Último Token Expiry Date</p>
              </div>
              <div class="column is-two-fifths">
                <p class="subtitle has-text-weight-bold">{{ token.expirydate | moment("dddd, MMMM Do YYYY [at] hh:mm A") }}</p>
              </div>
            </div>
          </div>
        </div>
        <div class="column is-vcentered is-one-third">
          <div class="columns is-multiline is-desktop is-centered">
            <div class="column is-full">
              <div class="box has-background-warning">
                <h3 class="title has-text-centered has-text-weight-bold">Suas preferencias</h3>
                <div class="columns is-vcentered is-centered is-multiline is-mobile">
                  <div class="column is-three-fifths">
                    <p class="subtitle">Mudar avatar</p>
                  </div>
                  <div class="column has-text-centered is-two-fifths">
                    <button class="button is-rounded is-primary" @click="alerts('em desenvolvimento')">
                      <span class="icon is-small">
                        <i class="far fa-user-circle"></i>
                      </span>
                      <span>Change</span>
                    </button>
                  </div>
                  <div class="column is-three-fifths">
                    <p class="subtitle">Mudar senha</p>
                  </div>
                  <div class="column has-text-centered is-two-fifths">
                    <button class="button is-rounded is-primary" @click="gotoPage('/changepassword/', 'settings')">
                      <span class="icon is-small">
                        <i class="fas fa-lock"></i>
                      </span>
                      <span>Mudar</span>
                    </button>
                  </div>
                  <div class="column is-three-fifths">
                    <p class="subtitle">Mudar EMAIL</p>
                  </div>
                  <div class="column has-text-centered is-two-fifths">
                    <button class="button is-rounded is-primary" @click="alerts('em desenvolvimento')">
                      <span class="icon is-small">
                        <i class="fas fa-envelope"></i>
                      </span>
                      <span>Change</span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
            <div class="column is-full">
              <div class="box has-background-danger">
                <h3 class="title has-text-centered has-text-white has-text-weight-bold">Área ResTriTa</h3>
                <div class="columns is-vcentered is-centered is-multiline is-mobile">
                  <div class="column is-three-fifths">
                    <p class="subtitle has-text-white">Excluir conta</p>
                  </div>
                  <div class="column is-two-fifths">
                    <button class="button is-rounded is-warning" @click="gotoPage('/me/', 'delete')">
                      <span class="icon is-small">
                        <i class="fas fa-user-times"></i>
                      </span>
                      <span>Excluir</span>
                    </button>
                  </div>
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
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';
    export default {
        components: {
          Loading,
        },
        data() {
          return {
            user: {},
            token: {},
            logged: false,
            avatar: "",
            gds: [],
            currgd: {},
            admin: false,
            superadmin: false,
            loading: false,
            fullpage: true,
          }
        },
        methods: {
          alerts(text) {
            window.alert(text);
          },
          gotoPage(url, cmd) {
            if(cmd){
              this.$router.push({ path: '/'+ this.currgd.id + ':' + cmd + url })
            } else {
              this.$router.push({ path: '/'+ this.currgd.id + ':' + url })
            }
          }
        },
        computed: {
          ismobile() {
            var width = window.innerWidth > 0 ? window.innerWidth : screen.width;
            if(width > 966){
              return false
            } else {
              return true
            }
          }
        },
        beforeMount() {
          this.loading = true;
          var token = localStorage.getItem("tokendata")
          var user = localStorage.getItem("userdata");
          if (user != null && token != null){
            var tokenData = JSON.parse(this.$hash.AES.decrypt(token, this.$pass).toString(this.$hash.enc.Utf8));
            var userData = JSON.parse(this.$hash.AES.decrypt(user, this.$pass).toString(this.$hash.enc.Utf8));
            this.user = userData, this.token = tokenData, this.loading = false; this.logged = true;
          } else {
            this.user = null, this.token = null, this.loading = false, this.logged = true;
          }
        },
        mounted() {
          this.loading = true;
          if(this.user.admin && this.user.superadmin){
            this.admin = true,   this.superadmin = true, this.loading = false;
            if(this.user.avatar){
              this.avatar = this.user.avatar;
            } else {
              this.avatar = 'https://cdn.statically.io/img/www.joyonlineschool.com/static/emptyuserphoto.png?w=64&h=64&quality=100&f=auto';
            }
          } else if(this.user.admin && !this.user.superadmin){
            this.admin = true, this.loading = false;
            if(this.user.avatar){
              this.avatar = this.user.avatar;
            } else {
              this.avatar = 'https://cdn.statically.io/img/www.joyonlineschool.com/static/emptyuserphoto.png?w=64&h=64&quality=100&f=auto';
            }
          } else {
            this.loading = false;
            if(this.user.avatar){
              this.avatar = this.user.avatar;
            } else {
              this.avatar = 'https://cdn.statically.io/img/www.joyonlineschool.com/static/emptyuserphoto.png?w=64&h=64&quality=100&f=auto';
            }
          }
        },
        created() {
          if (window.gds && window.gds.length > 0) {
            this.gds = window.gds.map((item, index) => {
              return {
                name: item,
                id: index,
              };
            });
            let index = this.$route.params.id;
            if (this.gds && this.gds.length >= index) {
              this.currgd = this.gds[index];
            }
          }
        }
      }
</script>
