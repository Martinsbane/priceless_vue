<template>
  <div id="wrapper">
    <nav class="navbar">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item"><strong>Priceless Empire</strong></router-link>

        <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu"
          @click="showMobileMenu = !showMobileMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active': showMobileMenu }">
        <div class="navbar-start">
          <div class="navbar-item">
            <form method="get" action="/search">
              <div class="field has-addons">
                <div class="control">
                  <input type="text" class="input" placeholder="What are you looking for?" name="query">
                </div>

                <div class="control">
                  <button class="button is-danger">
                    <span class="icon">
                      <i class="fas fa-search"></i>
                    </span>
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>

        <div class="navbar-end">
          <router-link to="/women" class="navbar-item">Women</router-link>
          <router-link to="/men" class="navbar-item">Men</router-link>

          <div class="navbar-item">
            <div class="buttons">
              <template v-if="$store.state.isAuthenticated">
                <router-link to="/my-account" class="button is-danger is-outlined">My account</router-link>
              </template>

              <template v-else>
                <router-link to="/log-in" class="button is-danger is-outlined">Log in</router-link>
              </template>

              <router-link to="/cart" class="button is-success is-inverted">
                <span class="icon"><i class="fas fa-shopping-cart"></i></span>
                <span>Cart ({{ cartTotalLength }})</span>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <div class="is-loading-bar has-text-centered" v-bind:class="{'is-loading': $store.state.isLoading }">
      <div class="lds-dual-ring"></div>
    </div>

    <section class="section">
      <router-view />
    </section>

    <footer class="footer">
      <div class="columns">
        <div class="column is-narrow">
          <!-- this logo will be changed to my logo after it is ready -->
          <figure class="image is-24x24">
            <img class="is-rounded"
              src="https://scontent-los2-1.xx.fbcdn.net/v/t1.6435-1/cp0/p40x40/82142583_767716080396805_3657080166242320384_n.jpg?_nc_cat=102&ccb=1-5&_nc_sid=7206a8&_nc_eui2=AeEMm_9o5I7I0go4bDgEhBHS3fh-YYSJ_Vrd-H5hhIn9WvSs867p0LsQo3ByFi7LYaX0jK_KGhMwmgBQsVcwY0Kl&_nc_ohc=Q_quc9xK8t4AX-wzE-F&tn=g6uzGt3latwaBKmL&_nc_pt=5&_nc_ht=scontent-los2-1.xx&oh=94155e772bf22e07f7f4be774210ddeb&oe=618C60E3">
          </figure>
        </div>
        <div>
          <p class="column">Designed by <a href="http://facebook.com/martinsbane" target="_blank"
              rel="noopener noreferrer">ShaQ</a></p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        showMobileMenu: false,
        cart: {
          items: []
        }
      }
    },
    beforeCreate() {
      this.$store.commit('initializeStore')

      const token = this.$store.state.token

      if (token) {
        axios.defaults.headers.common['Authorization'] = "Token " + token
      } else {
        axios.defaults.headers.common['Authorization'] = ""
      }
    },
    mounted() {
      this.cart = this.$store.state.cart
    },
    computed: {
      cartTotalLength() {
        let totalLength = 0

        for (let i = 0; i < this.cart.items.length; i++) {
          totalLength += parseInt(this.cart.items[i].quantity)
          
        }

        return totalLength
      }
    }
  }
</script>

<style lang="scss">
  @import '../node_modules/bulma';

  .lds-dual-ring {
    display: inline-block;
    width: 80px;
    height: 80px;
  }

  .lds-dual-ring:after {
    content: " ";
    display: block;
    width: 64px;
    height: 64px;
    margin: 8px;
    border-radius: 50%;
    border: 6px solid #ccc;
    border-color: #ccc transparent #ccc transparent;
    animation: lds-dual-ring 1.2s linear infinite;
  }

  @keyframes lds-dual-ring {
    0% {
      transform: rotate(0deg);
    }

    100% {
      transform: rotate(360deg);
    }
  }

  .is-loading-bar {
    height: 0;
    overflow: hidden;

    -webkit-transition: all 0.3s;
    transition: all 0.3s;

    &.is-loading {
      height: 80px;
    }
  }
</style>