<template>
  <div>
    <q-btn
      color="yellow"
      glossy
      icon="celebration"
      direction="up"
      round
      size="l"
      @click="dialog = true"
    />

    <q-dialog v-model="dialog" full-width persistent>
      <q-card class="bg-white" style="height: 90vh; display: flex; flex-direction: column;">
        
        <!-- Bottone X -->
        <q-btn
          icon="close"
          color="red"
          round
          flat
          size="lg"
          dense
          @click="dialog = false"
          class="absolute-top-right z-top q-ma-sm"
        />

        <!-- Toolbar -->
        <q-toolbar class="bg-yellow-4 text-black border-bottom q-pa-sm" style="border-bottom: 2px solid black;">
          <div class="text-h6">
            Menu Eventi e compleanni bambini
          </div>
        </q-toolbar>

        <!-- CONTENUTO SCORREVOLE -->
        <div class="q-pa-md" style="flex: 1; overflow-y: auto;">
          <div v-for="category in categories" :key="category._id" class="container">
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
                  <q-card v-for="dish in category.dishes" :key="dish._id" class="no-shadow">
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
              <q-separator class="bg-gesuini" />
            </div>
          </div>
        </div>

        <!-- FOOTER FISSO -->
        <div class="gesuini-cover bg-yellow-4 text-black">
          coperto: 1 euro
        </div>
      </q-card>
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
.gesuini-cover {
  text-align: center;
  font-size: 1.2rem;
  padding: 0.5rem;
  border-top: 2px solid black;
  flex-shrink: 0;
}
</style>
