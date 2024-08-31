// Componente que contendrá el formulario de registro de citas médicas
<script>
export default {
  name: 'FormComponent',
  data() {
    return {
      paciente: '',
      fecha: '',
      hora: '',
      gravedad: '',
      motivo: ''
    }
  },
  methods: {
    submitForm() {
      if (!this.paciente.trim() || !this.motivo.trim()) return
      this.$emit('enviar-paciente', {
        paciente: this.paciente.trim(),
        fecha: this.fecha,
        hora: this.hora,
        gravedad: this.gravedad,
        motivo: this.motivo.trim()
      })
      this.paciente = ''
      this.fecha = ''
      this.hora = ''
      this.gravedad = ''
      this.motivo = ''
    },
    isFormComplete() {
      return this.paciente.trim() && this.fecha && this.hora && this.gravedad && this.motivo.trim()
    }
  }
}
</script>

<template>
  <form @submit.prevent="submitForm">
    <div class="form-container">
      <div class="form-group">
        <label for="paciente" :class="{ vacio: !paciente }">Paciente</label>
        <input
          type="text"
          id="paciente"
          v-model="paciente"
          placeholder="Nombre completo"
          required
        />
      </div>
      <div class="form-group">
        <label for="fecha" :class="{ vacio: !fecha }">Fecha</label>
        <input
          type="date"
          id="fecha"
          value="2024-08-30"
          min="2024-01-01"
          max="2024-12-31"
          v-model="fecha"
          required
        />
      </div>
      <div class="form-group">
        <label for="hora" :class="{ vacio: !hora }">Hora</label>
        <input
          type="time"
          id="hora"
          min="08:00"
          max="19:00"
          value="08:00"
          v-model="hora"
          required
        />
      </div>
      <div class="form-group">
        <label for="gravedad" :class="{ vacio: !gravedad }">Gravedad</label>
        <select id="gravedad" v-model="gravedad" required>
          <option value="" disabled>Seleccione una opción</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </div>
      <div class="form-group">
        <label for="motivo" :class="{ vacio: !motivo }">Motivo</label>
        <input type="text" id="motivo" v-model="motivo" placeholder="Motivo consulta" required />
      </div>
    </div>
    <button type="submit" class="btn btn--agregar" :disabled="!isFormComplete()">Agregar</button>
  </form>
</template>

<style>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 1px solid #ccc;
  padding: 20px;
  border-radius: 10px;
  background-color: #fafafa;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.144);
}
.form-container {
  display: flex;
  align-items: center;
  margin-bottom: 2rem;
}
.form-group {
  margin: 10px;
  display: flex;
  flex-direction: column;
  text-align: center;
  gap: 5px;
}
.btn {
  padding: 10px 20px;
}
.btn--agregar {
  background-color: #312d2e;
  color: #fff;
  border: none;
  border-radius: 5px;
}
.btn--agregar:disabled {
  opacity: 0.5;
}

.btn--agregar:hover {
  background-color: #58c15e;
}
form label {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-width: 150px; /* Ajusta esto según sea necesario */
}

input[type='text'],
input[type='date'],
input[type='time'],
select {
  width: 100%;
  box-sizing: border-box;
  padding: 8px 6px;
  border: 1px solid #b5b4b4;
  border-radius: 5px;
}

.vacio {
  color: #dc143c;
}
</style>
