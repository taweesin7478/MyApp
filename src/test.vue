<template>
  <app-navigation></app-navigation>
</template>

<script>
import React from "react";
import { StackNavigator } from "vue-native-router";
import HomeScreen from "./screen/url.vue";

const AppNavigation = StackNavigator(
  {
    Home: { HomeScreen },
  },
  {
    initialRouteName: "Home",
  }
);

export default {
  components: { AppNavigation },
};
</script>