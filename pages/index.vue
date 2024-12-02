<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import { animate, scroll } from "motion";
import AnimatedWord from '../components/animated-word.vue'

const stickyRef = useTemplateRef('stickyRef')
const sectionRef = useTemplateRef('sectionRef')
const typographyRef = useTemplateRef('typographyRef')

const BOX_NUM = 12

onMounted(() => {

  animate(".box2", { opacity: [0, 1], y: [50, 0]});

  if (stickyRef.value && sectionRef.value) {
    const sectionPos = sectionRef.value.getBoundingClientRect()
    console.log(sectionPos)
    scroll(
      animate(
        stickyRef.value,
        {
            x: [ 20, -(sectionPos.width - (4 * (sectionPos.width / BOX_NUM)))]
        } as any,
        { 
          ease: "easeIn",
        }
      ),
      {
        target: sectionRef.value,
      }
    );
  }

});

watchEffect(() => {
  if (sectionRef.value) {
//   console.log(sectionRef.value.getBoundingClientRect())
}
})



</script>

<template>
  <div ref="typographyRef" class="wrapper">
    <AnimatedWord
        text="FUTUREPROOF"
        remove-char="ueo"
        />
    </div>
  <div class="height">
    <section ref="sectionRef" class="pin">
      <div ref="stickyRef" class="container">
        <div class="box" v-for="n in BOX_NUM" :key="n"></div>
      </div>
    </section>
  </div>
  <div class="box2"></div>

  </template>

<style lang="postcss" scoped>
.wrapper{
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 50vh;
}


.pin {
  margin-top: 30vh;
  height: 400vh;
  position: relative;
  width: fit-content;
  will-change: transform;
}

.flex-sticky {
  display: flex;
  position: sticky;
  gap: 20px;
  top: 0;
}

.container {
    display: flex;
    position: sticky;
    top: 25%;
    gap: 20px
  }


.box2 {
  width: 300px;
  height: 800px;
  border-radius: 10px;
  background-color: blue;
  opacity: 0;
}

.box {
  width: 300px;
  height: 300px;
  border-radius: 10px;
  background-color: red;
  opacity: 1;
}

</style>