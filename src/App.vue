<script setup>
import { computed, ref, watch } from "vue";

const title = "Títol de la pàgina";

const sumatori = 1000;
const quantitat = ref(10);
const total = computed(() => quantitat.value + sumatori);
const errorMessage = computed(() => {
  if (quantitat.value > 10) {
    return "T'has passat! Deixa'n pels altres";
  }

  if (quantitat.value < 4) {
    return "Quantitat insuficient, compra més!";
  }

  return "";
});

const codiDeAPI = "<div style='background:red'>hola</div>";

watch(quantitat, (newValue, oldValue) => {
  if (newValue > 10) {
    alert("T'has passat! Deixa'n pels altres.");
    name.value = "Pasota";
    quantitat.value = oldValue;
    return;
  }

  if (newValue < 4) {
    alert("Quantitat insuficient, compra més!");
    return;
  }
});

const name = ref("Joan");
const cognom = ref("Cifo");
const age = ref(25);

// const total = ref(quantitat.value + sumatori);

const restarUn = () => {
  quantitat.value -= 1;
};

const augmentarUn = () => {
  quantitat.value += 1;
};

const onSubmit = () => {
  if (name.value.length < 10) {
    alert("el teu nom mínim ha de tenir 10 caràcters");
  }

  // Enviar API
  fetch("/perfil", {
    method: "POST",
    body: JSON.stringify({
      user: {
        nom: name.value,
        cognom: cognom.value,
        age: age.value,
      },
      cart: [
        {
          quantitat: quantitat.value,
        },
      ],
    }),
  });
};

const something = function () {};

const checkCognom = ($event) => {
  console.log($event.target.value);
};
</script>

<template>
  <h1>
    {{ title }}
  </h1>
  <div id="main">
    <div>
      <button @click="restarUn" :disabled="quantitat === 0">-1</button>
      <span>quantitat: {{ quantitat }}</span>
      <button @click="augmentarUn" :disabled="quantitat > 7">+1</button>
    </div>
    <span>sumatori: {{ sumatori }}</span>
  </div>
  <div>
    <div>{{ errorMessage }}</div>
    total: {{ total }}
  </div>

  <!-- <div>
    {{ codiDeAPI }}
  </div>
  <div v-text="codiDeAPI" /> -->
  <div v-html="codiDeAPI" />

  <div>
    <h2>Perfil personal</h2>
    <form @submit.prevent="onSubmit">
      <input
        type="text"
        name="nom"
        placeholder="El teu nom"
        @input="name = $event.target.value"
        :value="name"
      />

      <input
        v-model="cognom"
        @input="checkCognom"
        type="text"
        name="cognom"
        placeholder="El teu cognom"
      />

      <input v-model="age" type="number" name="age" placeholder="El teu age" />

      <div>
        <button type="submit">Guardar</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
h1 {
  font-size: 30px;
}
</style>
