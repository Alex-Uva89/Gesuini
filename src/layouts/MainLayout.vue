<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="header text-h4 libertinus-mono-regular ">
      Gesuini
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<style scoped>

.header{
  background-color: #b93131;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
