<template>
  <div class="container">
    <div class="headers text-center">
      <h1>Online Courses</h1>
      <p>Choose an online course and start to learn something interesting!</p>
      <br>
    </div>
    <template v-if="ongoingCourses && ongoingCourses.length">
      <h3 class="d-flex justify-center">Ongoing Online Courses</h3>
        <v-container>
          <v-row class="d-flex justify-center">
            <div class="mx-2" v-for="course in ongoingCourses" :key="course.id">
              <course-card :course="course" :role="user.type" />
            </div>
          </v-row>
        </v-container>
    </template>
    <template v-if="finishedCourses && finishedCourses.length">
      <h3 class="d-flex justify-center">Completed Online Courses</h3>
        <v-container>
          <v-row class="d-flex justify-center">
            <div class="mx-2" v-for="course in finishedCourses" :key="course.id">
              <course-card :course="course" :role="user.type" />
            </div>
          </v-row>
        </v-container>
    </template>
    <h3 class="d-flex justify-center">Available Online Courses</h3>
    <v-container>
      <v-row class="d-flex justify-center">
        <div class="mx-2" v-for="course in courses" :key="course.id">
           <course-card :course="course" :role="user.type" />
        </div>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import CourseCard from '@/components/teachers/courses/CourseCard.vue'

export default {
  components: { CourseCard },
  computed: {
    user () {
      return this.$store.getters.user
    }
  },
  created () {
    this.$http.get('courses')
      .then(({ data: { courses, page, pages } }) => {
        this.ongoingCourses = this.user.courses.inProgress
        this.finishedCourses = this.user.courses.finished
        this.courses = courses.filter(course => !this.ongoingCourses.includes(course) && !this.finishedCourses.includes(course))
      })
  },
  data: () => ({
    courses: [],
    ongoingCourses: [],
    finishedCourses: []
  })
}
</script>

<style lang="sass" scoped>

</style>
