<script>
export default {
  name: 'ListPatients',
  props: {
    listaPacientes: {
      type: Array,
      required: true
    }
  },
  methods: {
    getColorClass(gravedad) {
      const gravedadClase = {
        Baja: 'baja',
        Media: 'media',
        Alta: 'alta'
      }
      return gravedadClase[gravedad] || ''
    }
  }
}
</script>
<template>
  <div
    v-for="(paciente, idx) in listaPacientes"
    :key="idx"
    :class="['card', getColorClass(paciente.gravedad)]"
  >
    <p class="title">Paciente</p>
    <p>{{ paciente.paciente }}</p>
    <hr />
    <p class="title">fecha</p>
    <p>{{ paciente.fecha }}</p>
    <hr />
    <p class="title">Hora</p>
    <p class="title">{{ paciente.hora }}</p>
    <hr />
    <p class="title">Motivo</p>
    <p>{{ paciente.motivo }}</p>
    <hr />
    <button type="button" class="btn btn--eliminar" @click="$emit('eliminar-paciente', idx)">
      Eliminar
    </button>
  </div>
</template>
<style scoped>
.card {
  width: 18rem;
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.144);
  text-align: center;
}

.title {
  font-weight: 700;
}

.btn {
  margin-top: 1rem;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.144);
}
.btn--eliminar {
  background-color: #312d2e;
  color: #fff;
  transition: all 0.5s ease;
}

.btn--eliminar:hover {
  background-color: #d61b41f7;
}

hr {
  opacity: 0.5;
}

/* Colores según la gravedad */
.baja {
  background-color: #b0f2c0; /* Verde claro */
}

.media {
  background-color: #f8e4a5; /* Amarillo claro */
}

.alta {
  background-color: #f8abb2; /* Rojo claro */
}
</style>
