<template>
    <footer>
        <p>Copyright &copy;
           {{ currentYear }} vue app
        </p>
        <router-link to="/about">About</router-link>
    </footer>
</template>

<script>
export default {
  data() {
    return {
      currentYear: new Date().getFullYear()
    };
  }
};
</script>

<style scoped>

a {
    color: #000;
    text-decoration: none;
}

footer {
    text-align: center;
    margin-top: 30px;
}

</style>
