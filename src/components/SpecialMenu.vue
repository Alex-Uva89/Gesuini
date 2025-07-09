<template>
  <div>
    <!-- FAB senza v-model -->
    <q-btn
      color="yellow"
      glossy
      icon="celebration"
      direction="up"
      round
      size="l"
      @click="dialog = true"
    />

    <!-- Dialog a schermo intero -->
    <q-dialog v-model="dialog" full-width persistent>
      <q-card class="bg-white" style="height: 90vh; position: relative;">
        <!-- Bottone X in alto a destra -->
        <q-btn
          icon="close"
          color="red"
          round
          flat
          dense
          @click="dialog = false"
          class="absolute-top-right q-ma-sm z-top"
        />

        <!-- Contenuto centrale -->
        <div class="q-pa-md">
        <div  v-for="category in categories" :key="category._id" class="container">
            <div v-if="category.specialMenu">

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


        </div>
    </q-card>
    <div class="gesuini-cover">
        coperto: 1 euro
    </div>

    </q-dialog>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
    categories: Array,
})

const dialog = ref(false)
</script>

<style scoped>

.gesuini-cover{
  background-color: #b93131;
  text-align: center;
  color: white;
  font-size: 1.2rem;
}

</style>
