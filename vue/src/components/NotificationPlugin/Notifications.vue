<template>
  <div class="lesson-schedule">
    <h2>Horário das Aulas</h2>
    <div class="carousel-container">
      <button class="prev-button" @click="prevSlide">&#8249;</button>
      <div class="carousel">
        <table>
          <thead>
            <tr>
              <th>Hora</th>
              <th v-for="field in fields" :key="field">{{ field }}</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="time in times" :key="time">
              <td>{{ time }}</td>
              <td v-for="field in fields" :key="field">
                <div v-if="hasLesson(field, time)">
                  <div v-for="lesson in getLessons(field, time)" :key="lesson.id">
                    <p><strong>Professor:</strong> {{ lesson.professor }}</p>
                    <p><strong>Aluno:</strong> {{ lesson.student }}</p>
                    <p><strong>Hora:</strong> {{ lesson.time }}</p>
                  </div>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <button class="next-button" @click="nextSlide">&#8250;</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fields: ['Campo 1', 'Campo 2', 'Campo 3', 'Campo 4'],
      times: ['09:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00'],
      lessons: [
        { id: 1, professor: 'João Silva', field: 'Campo 1', time: '09:00', student: 'Maria Santos' },
        { id: 2, professor: 'Pedro Oliveira', field: 'Campo 2', time: '11:00', student: 'Carlos Mendes' },
        { id: 3, professor: 'Ana Rodrigues', field: 'Campo 3', time: '14:00', student: 'Marta Almeida' },
        // ... outras aulas marcadas para os campos
      ],
      currentSlide: 0
    };
  },
  methods: {
    hasLesson(field, time) {
      return this.lessons.some(lesson => lesson.field === field && lesson.time === time);
    },
    getLessons(field, time) {
      return this.lessons.filter(lesson => lesson.field === field && lesson.time === time);
    },
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.fields.length;
    },
    prevSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.fields.length) % this.fields.length;
    }
  }
};
</script>

<style scoped>
.lesson-schedule {
  max-width: 600px;
  margin: 0 auto;
}

.carousel-container {
  position: relative;
  display: flex;
  align-items: center;
}

.carousel {
  flex: 1;
  overflow-x: hidden;
  position: relative;
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: center;
}

th, td {
  padding: 8px;
  border: 1px solid #ccc;
}

th {
  background-color: #f0f0f0;
}

td div {
  margin-bottom: 10px;
}

td div:last-child {
  margin-bottom: 0;
}

.prev-button,
.next-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 24px;
  background-color: #f0f0f0;
  border: none;
  padding: 4px 8px;
  cursor: pointer;
}

.prev-button {
  left: 0;
}

.next-button {
  right: 0;
}
</style>
