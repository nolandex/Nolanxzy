<template>
  <main
    class="mt-10 md:mt-1 flex flex-col-reverse gap-8 items-center md:flex-row md:gap-16 md:justify-center min-h-[65vh] md:min-h-[80vh]">
    <div class="space-y-2 text-center md:text-left px-10">
      <p class="text-amber-200">Hello World, I'm</p>
      <h1 class="text-4xl font-bold md:text-5xl text-white fadein-up">Bagas Rakha</h1>
      <div class="py-2">
        <h1
          class="typewrite text-xl font-semibold text-transparent bg-clip-text bg-gradient-to-r from-slate-100 to-yellow-500 md:text-2xl fadein-up"
          ref="typewriter">
          <span class="wrap">{{ txt }}</span>
        </h1>
      </div>
      <p class="text-white pr-4 fade-in-from-left">Welcome to My personal website. <span class="wave">👋🏼</span></p>
      <br>
    </div>

    <div class="flex justify-center md:justify-start fadein-right">
      <img
        alt="avatar"
        fetchpriority="high"
        width="300"
        height="300"
        decoding="async"
        data-nimg="1"
        class="w-10/12 md:h-auto rounded-full border-4 border-amber-200 pict"
        :src="avatar"
      />
    </div>
  </main>
</template>

<script>
import avatar from '@/assets/images/avatar.jpg'; // Ini penting!!

export default {
  name: 'HomeView',
  data() {
    return {
      toRotate: ["Web Developer", "Full-stack Engineer", "Informatics Student", "Tech Enthusiast"],
      period: 2000,
      txt: '',
      loopNum: 0,
      isDeleting: false,
      avatar, // masukkan ke data
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.tick();
    });
  },
  methods: {
    tick() {
      let typewriter = this.$refs.typewriter;

      if (!typewriter) {
        return;
      }

      let i = this.loopNum % this.toRotate.length;
      let fullTxt = this.toRotate[i];

      this.txt = this.isDeleting ? fullTxt.substring(0, this.txt.length - 1) : fullTxt.substring(0, this.txt.length + 1);
      typewriter.innerHTML = `<span class="wrap">${this.txt}</span>`;

      let that = this;
      let delta = 200 - Math.random() * 100;

      if (this.isDeleting) {
        delta /= 2;
      }

      if (!this.isDeleting && this.txt === fullTxt) {
        delta = this.period;
        this.isDeleting = true;
      } else if (this.isDeleting && this.txt === '') {
        this.isDeleting = false;
        this.loopNum++;
        delta = 500;
      }

      setTimeout(() => {
        that.tick();
      }, delta);
    },
  }
}
</script>
