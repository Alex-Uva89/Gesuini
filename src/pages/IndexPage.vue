<template>
  <div class="q-mb-lg">
    <q-page class="q-pa-md bg-sand q-mb-lg text-burgundy">
      <div  v-for="category in categories" :key="category._id" class="container">
        {{ console.log(category) }}
        <div v-if="!category.specialMenu">
          <q-expansion-item>
            <template v-slot:header>
              <q-item-section class="text-gesuini libertinus-mono-bold text-uppercase">
                {{ category.title }}
                <q-item-label caption lines="2" class="text-xs">
                  {{ category.description }}
                </q-item-label>
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
                        <template v-if="dish.price != 0">
                          <q-item-label>{{ dish.price }} €</q-item-label>
                        </template>
                        <template v-else>
                          prezzo in esposizione all'etto
                        </template>
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
      </div>
  
    </q-page>
    <q-banner class="text-white bg-black ">
      Si avvisa la gentile clientela che negli alimenti preparati possono essere contenuti ingredienti o coadiuvanti considerati allergeni.
    </q-banner>

    <q-page-sticky position="bottom-right" :offset="[18, 40]">
      <special-menu :categories="categories" />
    </q-page-sticky>
  </div>
</template>


<script setup>
import { onMounted, ref } from 'vue'
import { sanity } from 'src/sanity/client'

import SpecialMenu from 'src/components/SpecialMenu.vue'

const categories = ref([])

onMounted(async () => {
  const result = await sanity.fetch(`*[_type == "category"] | order(orderView asc){
    _id,
    title,
    description,
    orderView,
    specialMenu,
    "dishes": *[_type == "dish" && references(^._id)] | order(orderView asc){
      _id,
      title,
      price,
      description,
      orderView,
      specialMenu
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
  font-size: .9rem;
}

.bg-gesuini{
  background-color: #b93131;
}

.container{
  overflow-y: auto;
}
</style>
