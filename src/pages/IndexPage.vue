<template>
  <q-page class="q-pa-md bg-sand text-burgundy">
    <div  v-for="category in categories" :key="category._id">
      <q-expansion-item>
        <template v-slot:header>
          <q-item-section class="text-gesuini text-h6 libertinus-mono-bold text-uppercase">
            {{ category.title }}
          </q-item-section>
        </template>
        
        <div v-if="category.dishes.length > 0">
          <q-card v-for="dish in category.dishes" :key="dish._id"  class="no-shadow">
            <q-card-section>
              <q-list>
                <q-item>
                  <q-item-section>
                    <q-item-label>{{ dish.title }}</q-item-label>
                    <q-item-label caption lines="2">{{ dish.description }}</q-item-label>
                  </q-item-section>
  
                  <q-item-section side top>
                    <q-item-label>{{ dish.price }} €</q-item-label>
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card-section>
          </q-card>
        </div>

        <div v-else class="flex justify-center align-center q-pa-md">
          <q-chip>
             Non sono presenti piatti in questa categoria
          </q-chip>
        </div>
        
      </q-expansion-item>
      <q-separator class="bg-gesuini"/>
    </div>


    <q-chip class="gesuini-cover">
      coperto: 2 euro
    </q-chip>
  </q-page>
</template>


<script setup>
import { onMounted, ref } from 'vue'
import { sanity } from 'src/sanity/client'

const categories = ref([])

onMounted(async () => {
  const result = await sanity.fetch(`*[_type == "category"] | order(orderView asc){
    _id,
    title,
    orderView,
    "dishes": *[_type == "dish" && references(^._id)] | order(orderView asc){
      _id,
      title,
      price,
      description,
      orderView
    }
  }`)
  console.log('Categorie ordinate:', result)
  categories.value = result
})
</script>

<style lang="css">

.h{
  height: 50px;
}

.text-gesuini{
  color: #b93131;
}

.bg-gesuini{
  background-color: #b93131;
}

.gesuini-cover{
  position: fixed;
  bottom: 10%;
  left: 50%;
  transform: translate(-50%);
}

</style>
