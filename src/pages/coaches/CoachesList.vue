<template>
   <section>
      <coach-filter @change-filter='setFilters'>

      </coach-filter>
   </section>
  <base-card>
    <section>
      <div class='controls'>
        <base-button mode='outline'> Refresh </base-button>
        <base-button v-if='!isCoach' link to='register'> Register as a coach</base-button>
      </div>
    </section>
    <section>
      <ul v-if="hasCoaches">
        <coach-item
          v-for="coach in filteredCoaches"
          :key="coach.id"
          :id="coach.id"
          :first-name="coach.firstName"
          :last-name="coach.lastName"
          :rate="coach.hourlyRate"
          :areas="coach.areas"
        ></coach-item>
      </ul>
      <h3 v-else> No coaches </h3>
    </section>
  </base-card>
</template>


<script>
  import CoachItem from '../../components/coaches/CoachItem.vue';
  import CoachFilter from '../../components/coaches/CoachFilter.vue';

  import BaseButton from '../../components/UI/BaseButton';
  export default {
    components: { BaseButton, CoachItem, CoachFilter},
     data() {
        return {
           activateFilters: {
              frontend: true,
              backend: true,
              career: true
           }
        }
     },
    computed: {
      filteredCoaches() {
        const coaches =  this.$store.getters['coaches/coaches'];
        return coaches.filter((coach) => {
           if(this.activateFilters.frontend && coach.areas.includes('frontend')){
              return true;
           }
           if(this.activateFilters.backend && coach.areas.includes('backend')){
              return true;
           }
           if(this.activateFilters.career && coach.areas.includes('career')){
              return true;
           }
           return false;
        })
      },
      hasCoaches() {
        return this.$store.getters['coaches/hasCoaches'];
      },
       isCoach(){
          return this.$store.getters['coaches/isCoach']
       }
    },
     methods: {
       setFilters(updateFilters){
         this.activateFilters = updateFilters;
       }
     }
  }
</script>


<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.controls {
  display: flex;
  justify-content: space-between;
}
</style>
