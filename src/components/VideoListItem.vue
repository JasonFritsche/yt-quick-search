<template>
  <li class="list-group-item">{{ video.snippet.title }}</li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: ['video'],
  methods: {
    logProps: function() {
      console.log(this.video.snippet);
    },
  },
  mounted: function() {
    this.logProps();
  },
};
</script>
