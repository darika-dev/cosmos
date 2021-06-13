<template>
  <div class="space" :class="{ 'space-loading': loading }"></div>
</template>

<style lang="stylus" scoped>
.space
  position absolute
  z-index -1
  top 0
  right 0
  left 0
  bottom 0
  background-image radial-gradient(circle, #141b3f, #111735, #0e132a, #0b0d21, #040617)
</style>

<script>
export default {
  data: () => ({
    loading: true,
    parentInfo: {
      width: 0,
      height: 0,
      item: '',
    },
    starAmount: 2000,
    cameraZ: 0,
    fov: 20,
    baseSpeed: 0.032,
    speed: 0,
    starStretch: 5,
    starBaseSize: 0.05,
    starTexture: null,
    colors: ['0xFFFFFF', '0xDED473', '0x9C3328', '0x51726D'],
    stars: [],
    pixiApp: null,
  }),
  async mounted() {
    const PIXI = await import('pixi.js');

    window.addEventListener('resize', () => this.resizeHandler());
    this.createAnimation(PIXI);
  },
  methods: {
    resizeHandler() {
      this.parentInfo.width = this.parentInfo.item.clientWidth;
      this.parentInfo.height = this.parentInfo.item.clientHeight;
      this.pixiApp.renderer.resize(
        this.parentInfo.width,
        this.parentInfo.height
      );
    },

    createAnimation(PIXI) {
      this.pixiApp = new PIXI.Application({ transparent: true });
      this.$el.appendChild(this.pixiApp.view);
      this.parentInfo.item = this.pixiApp.view.parentNode;
      this.resizeHandler();
      this.starAmount = (200 * this.parentInfo.item.clientWidth) / 150;
      this.loadTextures(PIXI);

      this.createStars(PIXI);
      this.loading = false;

      // Listen for animate update
      this.pixiApp.ticker.add((delta) => {
        // Simple easing. This should be changed to proper easing function when used for real.
        this.cameraZ += delta * 10 * (this.speed + this.baseSpeed);
        for (let i = 0; i < this.starAmount; i++) {
          const star = this.stars[i];
          star.z < this.cameraZ && this.randomizeStar(star);

          // Map star 3d position to 2d with really simple projection
          const z = star.z - this.cameraZ;
          star.sprite.x =
            star.x * (this.fov / z) * this.pixiApp.renderer.screen.width +
            this.pixiApp.renderer.screen.width / 2;
          star.sprite.y =
            star.y * (this.fov / z) * this.pixiApp.renderer.screen.width +
            this.pixiApp.renderer.screen.height / 2;

          // Calculate star scale & rotation.
          const dxCenter =
            star.sprite.x - this.pixiApp.renderer.screen.width / 2;
          const dyCenter =
            star.sprite.y - this.pixiApp.renderer.screen.height / 2;
          const distanceCenter = Math.sqrt(
            dxCenter * dxCenter + dyCenter * dyCenter
          );
          const distanceScale = Math.max(0, (2000 - z) / 2000);
          star.sprite.scale.x = distanceScale * this.starBaseSize;
          // Star is looking towards center so that y axis is towards center.
          // Scale the star depending on how fast we are moving, what the stretchfactor is and depending on how far away it is from the center.
          star.sprite.scale.y =
            distanceScale * this.starBaseSize +
            (distanceScale * this.speed * this.starStretch * distanceCenter) /
              this.pixiApp.renderer.screen.width;
          star.sprite.rotation = Math.atan2(dyCenter, dxCenter) + Math.PI / 2;
        }
      });
    },

    loadTextures(PIXI) {
      // eslint-disable-next-line
      this.starTexture = PIXI.Texture.from('data:image/png;base64,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');
    },

    createStars(PIXI) {
      for (let i = 0; i < this.starAmount; i++) {
        const color = Math.floor(Math.random() * this.colors.length);
        const star = {
          sprite: new PIXI.Sprite(this.starTexture),
          z: 0,
          x: 0,
          y: 0,
        };
        this.colors.length > 0 && (star.sprite.tint = this.colors[color]);
        star.sprite.anchor.x = 0.5;
        star.sprite.anchor.y = 0.7;
        this.randomizeStar(star, true);
        this.pixiApp.stage.addChild(star.sprite);
        this.stars.push(star);
      }
    },

    randomizeStar(star, initial) {
      star.z = initial
        ? Math.random() * 2000
        : this.cameraZ + Math.random() * 1000 + 2000;

      // Calculate star positions with radial random coordinate so no star hits the camera.
      const deg = Math.random() * Math.PI * 2;
      const distance = Math.random() * 50 + 1;
      star.x = Math.cos(deg) * distance;
      star.y = Math.sin(deg) * distance;
    },
  },
};
</script>
