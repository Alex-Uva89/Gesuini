<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="header text-h4 libertinus-mono-regular ">
      Gesuini
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <div class="gesuini-cover">
      coperto: 2 euro
    </div>
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

.gesuini-cover{
  position: fixed;
  bottom: 0%;
  width: 100%;
  background-color: #b93131;
  text-align: center;
  color: white;
  font-size: 1.2rem;
}

</style>
