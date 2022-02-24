<template>
  <base-nav
    container-classes="container-fluid"
    class="navbar-top navbar-expand"
    :class="{'navbar-dark': type === 'default'}"
  >
    <a href="#" aria-current="page" class="h4 mb-0 text-white text-uppercase d-none d-lg-inline-block active router-link-active">  </a>
    <!-- Navbar links -->
    <b-navbar-nav class="align-items-center ml-md-auto">
      <!-- This item dont have <b-nav-item> because item have data-action/data-target on tag <a>, wich we cant add -->
      <li class="nav-item d-sm-none">
        <a class="nav-link" href="#" data-action="search-show" data-target="#navbar-search-main">
          <i class="ni ni-zoom-split-in"></i>
        </a>
      </li>
    </b-navbar-nav>
    
    <b-navbar-nav class="align-items-center ml-auto ml-md-0">
       
      <base-dropdown menu-on-right
                     class="nav-item"
                     tag="li"
                     title-tag="a"
                     title-classes="nav-link pr-0">
        <a href="#" class="nav-link pr-0" @click.prevent slot="title-container">
          <b-media no-body class="align-items-center" >
                  <span class="avatar avatar-sm rounded-circle">
                    <img alt="Image placeholder" src="@/assets/jt2.png">
                  </span>
            <b-media-body class="ml-2 d-none d-lg-block">
              <span class="mb-0 text-sm  font-weight-bold"> <div v-for="data in items" :key="data._id">
            <!-- {{data.emp_id}}  -->
              </div>  </span>
            </b-media-body>
          </b-media>
        </a>

        <template > 

          <b-dropdown-header class="noti-title ">
            <h6 class="text-overflow m-0">Welcome!  Jintai App</h6>
          </b-dropdown-header>
          <b-dropdown-item href="#/adminseting">
            <i class="ni ni-single-02"></i>
            <span>My Admin Settings</span>
          </b-dropdown-item>
         
      
          <b-dropdown-item href="#!">
            <i class="ni ni-support-16"></i>
            <span>Support</span>
          </b-dropdown-item>
          <div class="dropdown-divider"></div>
          <b-dropdown-item href="#!">
            <i class="ni ni-user-run"></i>
            <span>Logout</span>
          </b-dropdown-item>
  <b-dropdown-item href="#/test">
            <i class="ni ni-support-16"></i>
            <span>test</span>
          </b-dropdown-item>


        </template>
      </base-dropdown>
    </b-navbar-nav>
  </base-nav>
</template>
<script>
import { CollapseTransition } from 'vue2-transitions';
import { BaseNav, Modal } from '@/components';
import axios from "axios";
export default {
    created() {
    axios.get("http://localhost:3000/admin/emp_allusers").then((res) => {
      this.items = res.data;
  
    });
  },
  components: {
    CollapseTransition,
    BaseNav,
    Modal
  },
  props: {
    type: {
      type: String,
      default: 'default', // default|light
      description: 'Look of the dashboard navbar. Default (Green) or light (gray)'
    }
  },
  computed: {
    routeName() {
      const { name } = this.$route;
      return this.capitalizeFirstLetter(name);
    }
  },
  data() {
    return {
      activeNotifications: false,
      showMenu: false,
      searchModalVisible: false,
      searchQuery: ''
    };
  },
  methods: {
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    toggleNotificationDropDown() {
      this.activeNotifications = !this.activeNotifications;
    },
    closeDropDown() {
      this.activeNotifications = false;
    }
  }
};
</script>
<style scoped>
.b-setting{
  margin-left: 100px;
}
</style>