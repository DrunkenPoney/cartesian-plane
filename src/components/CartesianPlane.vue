<template>
  <div></div>
</template>

<script>

export default {
  name: "CartesianPlane",
  props: {
    steps: { type: Number, default: 20 },
    size: { type: Number, default: 800 },
    lblStep: { type: Number, default: 2 },
    xValStep: { type: Number, default: 1 },
    yValStep: { type: Number, default: 10 }
  },
  data() {
    return {
      sketch: null,
      instance: null
    }
  },
  mounted() {
    this.instance = new window.p5((sketch) => {
      sketch.preload = () => this.preload(sketch);
      sketch.setup = () => this.setup(sketch);
      sketch.draw = () => this.draw(sketch);
      this.sketch = sketch;
    }, this.$el);
  },
  methods: {
    preload(p) {

    },

    setup(p) {
      p.createCanvas(this.size, this.size);
    },

    draw(p) {
      const half = this.size / 2;
      const step = half / this.steps;
      
      p.background(255);
      p.strokeWeight(1);
      
      p.textStyle(p.NORMAL);
      p.textSize(0.6 * step);
      for (let pos, tick, i = 1; i < this.steps; i++) {
        pos = i * step;
        tick = step / (i % this.lblStep ? 7 : 5);
        
        p.stroke(210);
        // Vertical line
        p.line(pos, 0, pos, this.size);
        p.line(half + pos, 0, half + pos, this.size);
        // Horizontal line
        p.line(0, pos, this.size, pos);
        p.line(0, half + pos, this.size, half + pos);
        
        // Vertical tick
        p.stroke(0);
        p.line(pos, half - tick, pos, half + tick);
        p.line(half + pos, half - tick, half + pos, half + tick);
        // Horizontal tick
        p.line(half - tick, pos, half + tick, pos);
        p.line(half - tick, half + pos, half + tick, half + pos);
      }
      
      p.noStroke();
      for (let pos, value, tick, i = 1; i < this.steps; i++) {
        if (i % this.lblStep === 0) {
          pos = i * step;
          tick = step / (i % this.lblStep ? 7 : 5);
          
          // X labels
          p.textAlign(p.CENTER, p.TOP);
          value = -(this.steps - i) * this.xValStep;
          p.text(value, pos, half + tick + 2);
          value = i * this.xValStep;
          p.text(value, half + pos, half + tick + 2);
          
          // Y labels
          p.textAlign(p.RIGHT, p.CENTER);
          value = (this.steps - i) * this.yValStep;
          p.text(value, half - tick - 0.2 * step, pos);
          value = -i * this.yValStep;
          p.text(value, half - tick - 0.2 * step, half + pos)
        }
      }
      
      p.textAlign(p.RIGHT, p.TOP);
      p.text('0', half - 3, half + 1);
      
      
      // Axes (X and Y)
      p.stroke(0);
      p.line(half, 0, half, this.size);
      p.line(0, half, this.size, half);
      
      let triBase = step / 4, triHeight = step / 2;
      p.fill(0);
      p.triangle(half, 0, half - triBase, triHeight, half + triBase, triHeight); // Top arrow
      p.triangle(this.size, half, this.size - triHeight,
          half - triBase, this.size - triHeight, half + triBase); // Right arrow
      p.triangle(half, this.size, half - triBase,
          this.size - triHeight, half + triBase, this.size - triHeight); // Bottom arrow
      p.triangle(0, half, triHeight, half - triBase, triHeight, half + triBase); // Left arrow
      
      p.noStroke();
      p.textStyle(p.BOLD);
      p.textSize(3 * step / 4);
      p.textAlign(p.RIGHT, p.TOP)
      p.text('x', this.size - p.textDescent(), half + triBase);
      p.textAlign(p.LEFT, p.TOP);
      p.text('y', half + triBase + p.textDescent(), 0);
    },

  }, // END methods

  watch: {
    size(val, oldVal) {
      this.sketch.resizeCanvas(this.size, this.size);
    }
  }
};
</script>

<style scoped>
div {
  border: 1px solid black;
}

@media print {
  div {
    border: none;
  }
}
</style>
