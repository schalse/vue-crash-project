<script setup>
import Hero from '@/Components/Hero.vue'
import HomeCards from '@/Components/HomeCards.vue'
import JobListings from '@/Components/JobLisitings.vue'
</script>
<template>
  <Hero title="Become a Vue Dev"  />
  <HomeCards />
  <JobListings :limit="3" :showButton="true"/>
</template>