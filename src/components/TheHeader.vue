<template>
  <transition appear>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand">
        <img
          src="../assets/logo.png"
          width="30"
          height="30"
        >
       
      </a>
      <button
        v-trigger-collapse="'collapse'"
        class="navbar-toggler"
      >
        <span class="navbar-toggler-icon" />
      </button>
      <div
        id="collapse"
        class="collapse navbar-collapse"
      >
        <ul class="navbar-nav">
          <li class="nav-item">
            <a
              class="nav-link"
              :class="{ active: page === 'User'}"
              @click="changePage('User')"
            >Boutique</a>
          </li>
          <li class="nav-item">
            <a
              class="nav-link"
              :class="{ active: page === 'Admin'}"
              @click="changePage('Admin')"
            >Admin</a>
          </li>
        </ul>
      </div>
    </nav>
  </transition>
</template>

<script>
import { eventBus } from '../main';

export default {
  directives: {
    triggerCollapse: {
      inserted(el, binding) {
        window.addEventListener('click', () => {
          nav.classList.remove('show');
        })
        const nav = document.querySelector(`#${ binding.value }`);
        el.addEventListener('click', (e) => {
          if (nav.classList.contains('show')) {
            nav.classList.remove('show');
          } else {
            nav.classList.add('show');
          }
          e.stopPropagation();
        })
      }
    }
  },
  data() {
    return {
      page: eventBus.page
    }
  },
  created() {
    eventBus.$on('update:page', (page) => {
      this.page = page;
    })
  },
  methods: {
    changePage(page) {
      eventBus.changePage(page);
    }
  }
}
</script>

<style scoped>
 a {
   cursor: pointer;
 }

   @keyframes fromtop {
    from { 
      transform: translateY(-20px);
    }
    to {}
  }


  .v-enter-active {
    animation: fromtop 1s;
  }
</style>
