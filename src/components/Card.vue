<script setup>

defineProps({
    cita: Object,
})

const color = {
    Baja: "green",
    Media: "yellow",
    Alta: "red"
}
</script>

<template>
    <div :style="{ backgroundColor: color[cita.gravedad] }" class="card">
        <h4>Paciente</h4>
        <p>{{ cita.paciente }}</p>

        <h4>Fecha</h4>
        <p>{{ cita.fecha }}</p>

        <h4>Hora</h4>
        <p>{{ cita.hora }}</p>

        <h4>Motivo</h4>
        <p>{{ cita.motivo }}</p>

        <button @click="$emit('eliminarCita')" type="button"> Eliminar </button>
    </div>
</template>

<style scoped>
.card {
    flex-basis: calc(25% - 4rem);
    border-radius: 1rem;
    padding: 1rem;
}
</style>