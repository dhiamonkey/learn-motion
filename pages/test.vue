<script setup>
  import { ref, onMounted } from 'vue'
  import { animate, scroll } from "motion"
  
  const sectionRef = ref(null)
  const containerRef = ref(null)
  
  const refreshPage = () => {
    window.location.reload()
  }
  
  onMounted(() => {
    // Set a random accent color
    document.body.style.setProperty(
      "--accent",
      `var(--hue-${Math.ceil(Math.random() * 7) - 1})`
    )
  
    const items = containerRef.value.querySelectorAll(".item")
  
    // Animate gallery horizontally during vertical scroll
    scroll(
      animate(
        containerRef.value,
        {
          transform: ["none", `translateX(-${items.length - 1}00vw)`],
        },
        { ease: "linear" }
      ),
      { target: sectionRef.value }
    )
  
    // Progress bar representing gallery scroll
    scroll(animate(".progress", { scaleX: [0, 1] }, { ease: "linear" }), {
      target: sectionRef.value,
    })
  
    // Image title parallax
    const segmentLength = 1 / items.length
    items.forEach((item, i) => {
      const header = item.querySelector("h3")
  
      scroll(animate(header, { x: [200, -200] }, { ease: "linear" }), {
        target: sectionRef.value,
        offset: [
          [i * segmentLength, 1],
          [(i + 1) * segmentLength, 0],
        ],
      })
    })
  })
  </script>

<template>
    <div>
      <main>
        <article>
          <header><h2>Lines of London</h2></header>
          <section ref="sectionRef">
            <div ref="containerRef" class="container">
              <div v-for="n in 12" :key="n" class="item">
                <h3>#{{ n.toString().padStart(3, '0') }}</h3>
              </div>
            </div>
          </section>
          <footer>
            <p>
              Photos by
              <a target="_blank" href="https://twitter.com/mattgperry">Matt Perry</a>
            </p>
          </footer>
        </article>
        <div class="progress"></div>
        <div>test</div>
      </main>
    </div>
  </template>
  
  
  
  <style scoped>

  
  article header,
  article footer {
    height: 80vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  
  section {
    height: 500vh;
    position: relative;
  }
  
  .container {
    display: flex;
    position: sticky;
    top: 25%;
    gap: 20px
  }
  
  .item {
    display: flex;
    width: 100vw;
    height: 100vh;
    flex: 0 0 auto;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    overflow: hidden;
  }
  
  .item {
    width: 300px;
    height: 400px;
    background-color: red;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  
  h2 {
    font-size: 56px;
    font-weight: 700;
    letter-spacing: -3px;
    line-height: 1.2;
    text-align: center;
    margin: 0;
  }
  
  h3 {
    margin: 0;
    color: var(--red);
    font-size: 50px;
    font-weight: 700;
    letter-spacing: -3px;
    line-height: 1.2;
    position: relative;
    bottom: 30px;
    display: inline-block;
  }
  
  .item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  .progress {
    position: fixed;
    left: 0;
    right: 0;
    height: 5px;
    background: var(--accent);
    bottom: 50px;
    transform: scaleX(0);
  }
  </style>