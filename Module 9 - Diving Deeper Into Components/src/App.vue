<template>
  <div>
    <the-header></the-header>
    <button @click="setSelectedComponent('active-goals')">Active goals</button>
    <button @click="setSelectedComponent('manage-goals')">Manage goals</button>
    <!-- <active-goals v-if="selectedComponent === 'active-goals'"></active-goals>
    <manage-goals v-if="selectedComponent === 'manage-goals'"></manage-goals> -->
    <keep-alive>
      <component :is="selectedComponent"></component>
    </keep-alive>
  </div>
</template>

<script>
// import CourseGoals from "./components/CourseGoals.vue";
// import UserInfo from "./components/UserInfo.vue";
import TheHeader from "./components/TheHeader.vue";
// import BadgeList from "./components/BadgeList.vue";
import ActiveGoals from './components/ActiveGoals.vue';
import ManageGoals from './components/ManageGoals.vue';
export default {
  components: {
    "the-header": TheHeader,
    ActiveGoals,
    ManageGoals
    // "badge-list": BadgeList,
    // UserInfo,
    // CourseGoals,
  },
  data() {
    return {
      selectedComponent: 'active-goals',
      activeUser: {
        name: "Maximilian Schwarzmüller",
        description: "Site owner and admin",
        role: "admin",
      },
    };
  },
  methods: {
    setSelectedComponent(cmp) {
      this.selectedComponent = cmp
    }
  }
};
</script>

<style>
html {
  font-family: sans-serif;
}

body {
  margin: 0;
}
</style>