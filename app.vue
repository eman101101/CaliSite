<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

export default {
  data() {
    return {
      email: '',
      submitted: false,
      isOpen: false
    };
  },
  methods: {
    submitForm() {
      this.submitted = true;
      this.requestLocation();
    },
    requestLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          console.log('Latitude: ' + position.coords.latitude);
          console.log('Longitude: ' + position.coords.longitude);
        });
      } else {
        console.log('Geolocation is not supported by this browser.');
      }
    },
    playing() {
      console.log('Video is playing');
    },
    ended() {
      console.log('Video has ended');
    }
  },
  mounted() {
    gsap.utils.toArray('.animate-section').forEach((section, index) => {
      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: section,
          start: 'top bottom',
          end: 'bottom top',
          onEnter: () => tl.play()
        },
        paused: true
      });

      tl.from(section, {
        y: 200,
        autoAlpha: 0,
        delay: 0.5,
      });
    });
  },
};
</script>

<template>
  <div class="apple-site">
    <main>
      <section class="product-showcase" v-for="i in 6" :key="i">
        <video autoplay loop muted class="background-video">
          <source :src="'/different' + i + '.mp4'" type="video/mp4">
        </video>
        <div class="content animate-section">
          <section v-if="i === 1">
            <h2>See Different With Calliagnosia </h2>
            <p style="min-width: 200px;">Experience the revolution in the Vision Pro. Calliagnosia is a groundbreaking app that removes appearance biases, promoting equality and unity.</p>            <UButton label="‎" style="background: transparent; color: lightblue; font-size: 50px; border: none;" />
            <UButton label="Watch the reveal" @click="isOpen = true" style="background: none; color: dodgerblue; font-size: 2.5em; border: none; padding-top: 30px; text-shadow: 2px 2px 4px rgba(0, 0, 0, 1);" />
<UModal v-model="isOpen" fullscreen>
  <div style="display: flex; justify-content: center; align-items: center; height: 100%; width: 100%;">
    <iframe style="width: 90%; height: 90%;" src="https://www.youtube.com/embed/vL_gRyQnKN8" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  </div>
  <UButton label="Close" @click="isOpen = false" style="position: absolute; top: 10px; right: 10px; font-size: 1.5em;" /></UModal>
          </section>
          <section v-else-if="i === 2">
            <h3>A world without barriers </h3>
            <p>Imagine a world without barriers, where everyone is seen for who they truly are. That's the world Calliagnosia is striving to create. Our groundbreaking technology allows you to experience people in their purest form. It's more than just a VR experience, it's a step towards a more equal and united world.</p>
          </section>
          <section v-else-if="i === 3">
            <h3>How it works</h3>
            <p>Calliagnosia leverages the power of cutting-edge Artificial Intelligence (AI) to revolutionize the way we perceive the world. Our proprietary AI algorithms are trained on vast datasets, enabling them to analyze and interpret visual information in real-time with unprecedented accuracy. This AI-driven approach allows us to remove appearance biases, providing a truly immersive and unbiased VR experience.</p>
            <p>Our state-of-the-art Virtual Reality (VR) tracking system offers an unparalleled level of immersion. By combining advanced motion tracking with high-definition 3D rendering, we create a hyper-realistic virtual environment that responds to your movements in real-time. This seamless integration of the physical and virtual worlds blurs the line between reality and simulation, creating a truly immersive VR experience.</p>
            <p>But that's not all. Calliagnosia also incorporates Machine Learning (ML), Deep Learning, and Neural Networks into its technology stack. These advanced technologies enable our system to learn and adapt over time, continually improving its performance. The result is a VR experience that's not just immersive and unbiased, but also personalized and adaptive.</p>
          </section>
          <section v-else-if="i === 4">
            <h3>Sort People Different </h3>
            <p>Calliagnosia allows you to change how others are seen as a way to show your superiority. Our advanced algorithms analyze a wide range of data points and can improve or reduce someones attractiveness on values that can include:</p>
            <p>- Personal Wealth</p>
            <p>- Individual Height</p>
            <p>- Valorant Ranking</p>
            <p>- Android User</p>
          </section>
          <section v-else-if="i === 5">
            <h3>What People Are Saying</h3>
            <p>"Calliagnosia is a game-changer. It's like nothing I've ever experienced before."</p>
            <p>- Scott Altwoman: CEO TechNova Inc.</p>
            <p>"I never realized how much appearance biases were affecting my perception of the world until I tried Calliagnosia. It's truly eye-opening."</p>
            <p>- Martin Fresh: Vice COO FutureDynamics LLC</p>
            <p>"The level of immersion and realism that Calliagnosia offers is unparalleled. It's a whole new way of experiencing the world."</p>
            <p>- Albert Reinstien: ML Engineer at QuantumLeap Solutions</p>
          </section>
          <section v-else-if="i === 6">
            <h3>Pricing</h3>
            <p>As a startup, none of this actually works but we're working towards a product that might have one of the features we've described. In the meantime contact our team so you can invest and we can get a lot of money! Yipeeeeeee!</p>
            <form @submit.prevent="submitForm" class="email-form">
              <input type="email" v-model="email" placeholder="Enter your email" class="email-input">
              <button type="submit" class="submit-button">Submit</button>
            </form>
            <p v-if="submitted" class="submit-message">REPLICANT DETECTED - LOCATION TRACKED FOR ELIMINATION</p>
            <footer>
      <p>© 2024 <a href="https://e2d.me" target="_blank" style="color: dodgerblue;">National Calliagnosia Inc.</a> Don't find out who we are.</p>
    </footer>
          </section>
        </div>
      </section>
    </main>

  </div>
</template>

<style>
body {
  background-color: black;
}
</style>

<style scoped>
.apple-site {
  font-family: 'Roboto', sans-serif;
  color: white;
  background-color: #1d1d1f;
}

.product-showcase {
  position: relative;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.background-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1;
}
.email-form {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 20px;
}
.email-input {
  padding: 10px;
  border: none;
  border-radius: 5px;
  outline: none;
}

.submit-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #4CAF50;
  color: white;
  cursor: pointer;
}

.submit-button:hover {
  background-color: #45a049;
}

.submit-message {
  color: red;
  margin-top: 20px;
  background-color: rgba(0, 0, 0, 0.7);
  padding: 10px;
  border-radius: 5px;
}
.content {
  z-index: 2;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 1);
  padding: 50px;
  max-width: 1800px;
  margin: 0 auto;
}

h1 {
  color: white;
  font-size: 9em;
}

h2, h3 {
  color: white;
  font-size: 7em;
}

p, li {
  color: white;
  line-height: 1.6;
  font-size: 2em;
}



footer {
  text-align: center;
  padding: 30px;
}

@media (max-width: 600px) {
  .content {
    padding: 20px;
    max-width: 100%;
  }

  h1 {
    font-size: 4.5em;
  }

  h2, h3 {
    font-size: 3.5em;
  }

  p, li {
    font-size: 1em;
  }

  footer {
    padding: 15px;
  }
}

</style>