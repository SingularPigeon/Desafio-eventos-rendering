<script>
import FormComponent from './FormComponent.vue'
import CardPatients from './CardPatients.vue'
export default {
  name: 'AdminCitas',
  components: { FormComponent, CardPatients },
  data() {
    return {
      pacientes: [],
      isFormComplete: false
    }
  },
  methods: {
    agregarPaciente(nuevoPaciente) {
      this.pacientes.push(nuevoPaciente)
    },
    EliminarPaciente(idx) {
      this.pacientes.splice(idx, 1)
    }
  }
}
</script>
<template>
  <h1>Citas Medicas</h1>
  <FormComponent @enviar-paciente="agregarPaciente" />
  <!-- directiva v-show para mostrar el mensaje si el array pacientes está vacío -->
  <p class="info" v-show="pacientes.length === 0">Aún no hay consultas registradas</p>

  <div class="container">
    <!-- aqui se mostratán las card de cada paciente -->
    <CardPatients :listaPacientes="pacientes" @eliminar-paciente="EliminarPaciente" />
  </div>
</template>
<style>
h1 {
  text-align: center;
}
.container {
  margin-top: 2rem;
  display: flex;
  gap: 2rem;
}
.info {
  text-align: center;
  color: #dc143c;
  font-size: 14px;
}
</style>
