<template>
  <svg viewBox="0 0 24 24" :height="height" :width="width" :fill="color" style="display: inherit;">
    <g>
      <path d="M21.5,0h-19C1.1,0,0,1.1,0,2.5v19C0,22.9,1.1,24,2.5,24h19c1.4,0,2.5-1.1,2.5-2.5v-19C24,1.1,22.9,0,21.5,0z
         M23,21.5c0,0.8-0.7,1.5-1.5,1.5h-19C1.7,23,1,22.3,1,21.5v-19C1,1.7,1.7,1,2.5,1h19C22.3,1,23,1.7,23,2.5V21.5z"/>
      <path d="M7.9,10.9H10V9.7H7.9V3.6H6.7v6.2H4.2v1.1h2.4c-0.6,1.8-1.5,3.4-2.8,4.8L4.4,17c1-1.3,1.7-2.7,2.3-4.2v6.7h1.2
        v-7c0.5,0.8,1.2,1.8,1.9,3l0.7-1.1c-0.9-1.1-1.7-2.1-2.6-3V10.9z"/>
      <path d="M10.3,4.8L9.3,4.7C9.2,6.1,9,7.4,8.6,8.5l0.9,0.3C9.9,7.6,10.2,6.3,10.3,4.8z"/>
      <path d="M5.9,8.7C5.7,7.3,5.5,6.1,5.2,5L4.3,5.3c0.3,1.2,0.6,2.3,0.8,3.6L5.9,8.7z"/>
      <polygon class="st9" points="15.9,7.9 19.1,7.9 19.1,6.9 15.9,6.9 15.9,5.7 19.5,5.7 19.5,4.7 15.9,4.7 15.9,3.5 14.7,3.5 
        14.7,4.7 11,4.7 11,5.7 14.7,5.7 14.7,6.9 11.5,6.9 11.5,7.9 14.7,7.9 14.7,9.1 10.6,9.1 10.6,10.1 20,10.1 20,9.1 15.9,9.1   "/>
      <path d="M11.5,19.5h1.2v-2.8h5.1v1c0,0.4-0.2,0.6-0.6,0.6l-1.2-0.1l0.3,1.1h1.2c0.9,0,1.4-0.5,1.4-1.4v-6.8h-7.5V19.5z
         M12.7,12.3h5.1v1.3h-5.1V12.3z M12.7,14.5h5.1v1.2h-5.1V14.5z"/>
    </g>
  </svg>
</template>
<script>
const Excellent = {
  props: {
    height: {
      type: [String, Number],
      default: 24
    },
    width: {
      type: [String, Number],
      default: 24
    },
    color: {
      type: String,
      default: '#000'
    }
  }
}

export default Excellent;
</script>