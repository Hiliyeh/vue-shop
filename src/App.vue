<template>
  <div id="app">
    <the-header />
    <user />
  </div>
</template>

<script>
import TheHeader from './components/TheHeader'
import User from './components/features/User/User';
import Admin from './components/features/Admin/Admin';

export default {
  name: 'App',
  components: {
    TheHeader,
    User,
    Admin
  }
}
</script>