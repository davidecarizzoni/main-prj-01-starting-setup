<template>
  <li>
    <h3> {{ fullName }} </h3>
    <h4> {{ rate }} /hour</h4>
    <div>
      <base-badge v-for="area in areas" :key="area" :type="area" :title="area"> </base-badge>
    </div>
    <div class='actions'>
       <router-view></router-view>
      <base-button mode='outline' link :to='coachContactLink'> Contact </base-button>
      <base-button link :to='coachDetail'> Detail  </base-button>
    </div>
  </li>
</template>

<script>
  import BaseButton from '../UI/BaseButton';
  import BaseBadge from '../UI/BaseBadge';
  export default {
    components: { BaseBadge, BaseButton },
    computed: {
      fullName(){
        return this.firstName + this.lastName;
      },
      coachContactLink() {
        return this.$route.path + '/' + this.id + '/contact'
      },
      coachDetail() {
        return this.$route.path + '/' + this.id
      }
    },
    props: ['id', 'firstName', 'lastName', 'rate', 'areas']
  }
</script>

<style scoped>

li {
  margin: 1rem 0;
  border: 1px solid #424242;
  border-radius: 12px;
  padding: 1rem;
}

h3 {
  font-size: 1.5rem;
}

h3,
h4 {
  margin: 0.5rem 0;
}

div {
  margin: 0.5rem 0;
}

.actions {
  display: flex;
  justify-content: flex-end;
}
</style>
