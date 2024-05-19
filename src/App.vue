<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';

const componenteRenderizado = ref("Empty")
const disabled = ref(true)
const citas = ref([])
const onChange = e => {
  const { name, value } = e.target

  emptyLabels.value = {
    ...emptyLabels.value,
    [name]: value ? false : true
  }

  if (!Object.values(form.value).includes("")) {
    disabled.value = false
    return;
  }
  disabled.value = true
}

const form = ref({
  paciente: "",
  fecha: "",
  hora: "",
  gravedad: "",
  motivo: "",
})

const emptyLabels = ref({
  paciente: true,
  fecha: true,
  hora: true,
  gravedad: true,
  motivo: true,
})

const onSubmit = () => {


  if (!Object.values(form.value).includes("")) {
    citas.value.push(form.value);
    form.value = {
      paciente: "",
      fecha: "",
      hora: "",
      gravedad: "",
      motivo: "",
    }

    emptyLabels.value = {
      paciente: true,
      fecha: true,
      hora: true,
      gravedad: true,
      motivo: true,
    }

    disabled.value = true
    return;
  }
  alert("Todos los campos son obligatorios")
}



</script>

<template>

  <form @submit.prevent="onSubmit" class="form">
    <div class="form__campos">
      <div class="campo">
        <label :class="{ empty: emptyLabels.paciente }" for="paciente">Paciente</label>
        <input @input="onChange" v-model="form.paciente" type="text" name="paciente" id="paciente">
      </div>

      <div class="campo">
        <label :class="{ empty: emptyLabels.fecha }" for="fecha">Fecha</label>
        <input @input="onChange" v-model="form.fecha" type="date" name="fecha" id="fecha">
      </div>

      <div class="campo">
        <label :class="{ empty: emptyLabels.hora }" for="hora">Hora</label>
        <input @input="onChange" v-model="form.hora" type="time" name="hora" id="hora">
      </div>

      <div class="campo">
        <label :class="{ empty: emptyLabels.gravedad }" for="gravedad">Gravedad</label>
        <select @change="onChange" v-model="form.gravedad" name="gravedad" id="gravedad">
          <option disabled></option>
          <option>Baja</option>
          <option>Media</option>
          <option>Alta</option>
        </select>
      </div>

      <div class="campo">
        <label :class="{ empty: emptyLabels.motivo }" for="motivo">Motivo</label>
        <input @input="onChange" v-model="form.motivo" type="text" name="motivo" id="motivo">
      </div>
    </div>

    <div class="form__boton">
      <button type="submit" :disabled="disabled">Agregar</button>
    </div>
  </form>

  <div v-if="citas.length > 0" class="citas">
    <Card v-for="(cita, i) in citas" :cita="cita" :key="i" @eliminarCita="citas.splice(i, 1)" />
  </div>
  <div v-else>
    <p class="mensaje"> Aún no hay consultas registradas </p>
  </div>

</template>

<style scoped>
.form {
  border: 1px solid #000;
  border-radius: 10px;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.form__campos {
  display: flex;
  justify-content: space-between;
}

.campo {
  display: flex;
  flex-direction: column;
}

.campo label {
  font-weight: 500;
}

.mensaje,
.empty {
  color: #F00;
}

.citas {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 2rem;
}
</style>
