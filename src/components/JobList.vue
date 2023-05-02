<script setup lang="ts">
import Job from '@/types/Job';
import OrderTerm from '@/types/OrderTerm';
import { computed, defineProps, PropType } from 'vue';

// props
const props = defineProps({
    jobs: {
        required: true,
        type: Array as PropType<Job[]>
    },
    order: {
        required: true,
        type: String as PropType<OrderTerm>
    }
})

// computed
const orderedJobs = computed(() => {
    return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
    })
})
</script>

<template>
    <div class="job-list">
        <p>Ordered by {{ order }}</p>
        <transition-group name="list" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <img src="../assets/rupee.svg" alt="rupee icon">
                    <p>{{ job.salary }}</p>
                </div>
                <div class="description">
                    <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Laboriosam, laborum vero necessitatibus accusamus odio adipisci? Vero, harum numquam doloribus adipisci architecto quia, ab in dolore natus sunt repudiandae sed commodi.</p>
                </div>
            </li>
        </transition-group >
    </div>
</template>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move{
    transition: all 1s;
  }
</style>