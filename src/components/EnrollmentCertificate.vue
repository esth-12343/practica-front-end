<script>
import axios from 'axios'

export default {
  data() {
    return {
      cui: '',
      enrollments: []
    }
  },

  methods: {
    async buscar() {
      const response = await axios.get(
        `https://sisacad-enrollments-backend.vercel.app/restful/enrollment-certificate/?cui=${this.cui}`
      )

      this.enrollments = response.data.results
    }
  }
}
</script>

<template>
  <div>
    <h1>Constancia de Matrícula</h1>

    <input v-model="cui" placeholder="Ingrese CUI">
    <button @click="buscar">Buscar</button>

    <div v-if="enrollments.length">
      <h2>{{ enrollments[0].student.full_name }}</h2>

      <p>CUI: {{ enrollments[0].student.cui }}</p>

      <table border="1">
        <thead>
          <tr>
            <th>Código</th>
            <th>Curso</th>
            <th>Docente</th>
            <th>Créditos</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="e in enrollments" :key="e.id">
            <td>{{ e.workload.course.code }}</td>
            <td>{{ e.workload.course.name }}</td>
            <td>{{ e.workload.teacher.full_name }}</td>
            <td>{{ e.workload.course.credits }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>