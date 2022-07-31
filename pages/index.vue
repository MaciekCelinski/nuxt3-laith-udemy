<template>
  <div>
    
    <Html lang="pl-PL">
      <Head>
        <Title>Restaurantly</Title>
        <Meta name="description" content="My page is cool" />
        <Link rel="preload" href="https://www.iconpacks.net/icons/2/free-sad-face-icon-2691-thumb.png" as="script" />
      </Head>
    </Html>

    <div class="container">
      <h1>Welcome to Restaurantly</h1>
      <NuxtLink to="/restaurants">Go to restaurants</NuxtLink>
    </div>
  </div>
</template>

<script setup>

</script>

<style scoped>
.container {
  text-align: center;
  margin-top: 3rem;
}
</style>
