<template>
  <div id="wrapper">
    <header>
      <span class="main-title">Portfolio</span>
      <span class="sub-title">cødex | Tobias Baake</span>
    </header>

    <div class="body glass-card">
      <div class="content">
        <span class="header">Tech Stack</span>
        <div class="card-wrapper">
          <div :class="['card', tech.additionalClass]"  v-for="tech in TECH_CARDS" :key="tech.title">
            <div class="card-content">
              <div class="card-header">
                <h3>{{ tech.title }}</h3>
                <NuxtImg :src="tech.icon" alt="icon" class="icon" />
              </div>
              <hr />
              <p>
                {{ tech.description }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="js">
const TECH_CARDS = [
  {
    title: "Nuxt.js",
    description:
      "Nuxt.js is a powerful framework built on top of Vue.js that simplifies the development of server-side rendered applications. It offers features like automatic routing, code splitting, and a modular architecture, making it easier to create performant and SEO-friendly web applications.",
    icon: "assets/nuxt.svg",
    additionalClass: "nuxt"
  },
  {
    title: "Python",
    description:
      "Python is a versatile and widely-used programming language known for its simplicity and readability. It supports multiple programming paradigms, including procedural, object-oriented, and functional programming. Python is commonly used for web development, data analysis, artificial intelligence, scientific computing, and automation.",
    icon: "assets/python.svg",
    additionalClass: "python"
  },
  {
    title: "Rust",
    description:
      "Rust is a systems programming language that prioritizes safety, performance, and concurrency. It is designed to prevent common programming errors such as null pointer dereferencing and data races.",
    icon: "assets/rust.svg",
    additionalClass: "rust"
  },
  {
    title: "Java",
    description:
      "Java is a high-level, class-based, object-oriented programming language that is designed to have as few implementation dependencies as possible. It is a general-purpose programming language intended to let application developers write once, run anywhere (WORA), meaning that compiled Java code can run on all platforms that support Java without the need for recompilation.",
    icon: "assets/java.svg",
    additionalClass: "java"
  }
];

function cardHoverEffect(){
  const cards = document.getElementsByClassName("card");
  const cardWrapper = document.getElementsByClassName("card-wrapper");
  console.log(cardWrapper);
  console.log(cards);

  //if (cardWrapper.length < 1 || cards.length < 1) return;

  for (let i = 0; i < cardWrapper.length; i++) {
    cardWrapper[i].addEventListener("mousemove", function ($event) {
      for (let j = 0; j < cards.length; j++) {
        const rect = cards[j].getBoundingClientRect();
        const x = $event.clientX - rect.left;
        const y = $event.clientY - rect.top;
        cards[j].style.setProperty("--xPos", `${x}px`);
        cards[j].style.setProperty("--yPos", `${y}px`);
      }
    });
  }
}

onMounted(() => {
  cardHoverEffect();
});
</script>

<style>
:root {
  --main-text-color: #FFFFFF;
  --sub-text-color: #BBBBCC;
  --body-box-shadow-color: rgba(77, 77, 97, 0.3);
  --body-background: rgba(77, 77, 97, 0.2);
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
}

#wrapper {
  min-height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: #10131b;
}

header {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 32px;
}

header .main-title {
  color: var(--main-text-color);
  font-size: 2.5rem;
  font-weight: bold;
}

header .sub-title {
  color: var(--sub-text-color);
  font-size: 1.2rem;
  margin-top: 4px;
}

.body {
  width: 80vw;
  min-width: 360px;
  max-width: 1800px;
  background: var(--body-background);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border: 1px solid var(--body-box-shadow-color);
}

.body .content {
  width: 100%;
  padding: 24px;
  color: var(--main-text-color);
  font-size: 1rem;
  line-height: 1.5;
}

.body .content .header {
  width: 100%;
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 16px;
}

.body .content .card-wrapper {
  width: 100%;
  border-radius: 24px;
  padding: 20px 0;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  gap: 0.75rem;
  margin: auto;
  text-align: justify;
  -webkit-hyphens: auto;
  hyphens: auto;
}

.body .content .card-wrapper .card {
  width: 340px;
	height: 350px;
	border-radius: 16px;
	display: flex;
	justify-content: center;
	align-items: center;
	position: relative;
	transition: all 0.15s;
}

.body .content .card-wrapper .card::before {
  content: "";
	height: 100%;
	width: 100%;
	position: absolute;
	top: 0;
	left: 0;
	border-radius: inherit;
	opacity: 0;
	transition: all 0.15s ease-in-out;
}

.body .content .card-wrapper .card:hover::before {
  opacity: 1;
}

.body .content .card-wrapper .card .card-content {
  background-color: rgba(20, 20, 35, 0.5);
	border-radius: inherit;
	transition: all 0.25s;
	height: calc(100% - 0.12rem);
	width: calc(100% - 0.12rem);
  padding: 15px;
}

.body .content .card-wrapper .card .card-content .card-header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 0 20px;
}

.body .content .card-wrapper .card .card-content .card-header h3 {
  padding-bottom: 0;
  font-size: 22px;
}

.body .content .card-wrapper .card .card-content .card-header .icon {
  height: 40px;
}

.body .content .card-wrapper .card .card-content hr {
  border: 0;
  height: 1px;
  background: var(--sub-text-color);
  margin: 10px 0;
}

.body .content .card-wrapper .card .card-content p {
  width:100%;
}

/* Default Case */
.body .content .card-wrapper:hover .card.default{
  background: radial-gradient(100rem circle at var(--xPos) var(--yPos), rgba(0, 255, 255, 0.4), transparent 15%);
}

/* Nuxt */
.body .content .card-wrapper:hover .card.nuxt{
  background: radial-gradient(100rem circle at var(--xPos) var(--yPos), rgba(0, 220, 130, 0.4), transparent 15%);
}

/* Python */
.body .content .card-wrapper:hover .card.python {
  background: radial-gradient(100rem circle at var(--xPos) var(--yPos), rgba(255, 208, 0, 0.4), transparent 15%);
}

/* Rust */
.body .content .card-wrapper:hover .card.rust {
  background: radial-gradient(100rem circle at var(--xPos) var(--yPos), rgba(255, 0, 76, 0.4), transparent 15%);
}

/* Java */
.body .content .card-wrapper:hover .card.java {
  background: radial-gradient(100rem circle at var(--xPos) var(--yPos), rgba(255, 145, 0, 0.4), transparent 15%);
}

</style>