<template>
  <json-chart :type="type" :previousPeriodDatasets="previousPeriodDatasets" :currentPeriodDatasets="currentPeriodDatasets" :labels="labels" />
</template>

<script>
import JsonChart from "@/components/jsonChart"
export default {
  components: {
    JsonChart
  },
};
</script>

<script setup>
import {
  type,
  previousPeriodDatasets,
  currentPeriodDatasets,
  labels
} from '@/data/custom.json'

</script>
