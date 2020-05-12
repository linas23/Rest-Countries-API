<template>
  <GmapMap
    :center="{lat:27.6710, lng:85.4298}"
    :zoom="7"
    map-type-id="satellite"
    style="width: 95vw; height: 444px"
  >
    <!-- <GmapMarker
      :key="index"
      v-for="(m, index) in markers"
      :position="m.position"
      :clickable="true"
      :draggable="true"
      @click="center=m.position"
    />-->
  </GmapMap>
</template>

<script>
</script>

