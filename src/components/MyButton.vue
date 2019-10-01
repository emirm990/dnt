<template>
  <div>
    <h1>{{ msg }}</h1>
    <button
      id="button"
      v-on:mouseover="hover=true"
      v-on:mouseleave="hover = false"
      v-on:click="handleClick()"
    >Do not touch</button>
  </div>
</template>

<script>
export default {
  name: "MyButton",
  data() {
    return {
      msg: "Do not touch",
      hover: false,
      counter: 0,
      mousePos: {
        x: 0,
        y: 0
      },
      elementPos: {
        x: 0,
        y: 0
      },
      distance: {
        x: 0,
        y: 0
      }
    };
  },
  mounted: function() {
    let button = document.getElementById("button");
    let buttonPos = button.getBoundingClientRect();
    this.elementPos.x = buttonPos.x;
    this.elementPos.y = buttonPos.y;
  },
  props: ["coords"],
  watch: {
    hover: function(hover) {
      if (this.hover) {
        this.msg = "You touched again :(";
        this.counter++;
      } else {
        this.msg = "Do not touch again!";
      }
    },
    $props: {
      handler(props) {
        (this.mousePos.x = props.coords.x), (this.mousePos.y = props.coords.y);
        this.distance.x = props.coords.x - this.elementPos.x;
        this.distance.y = props.coords.y - this.elementPos.y;
        if (
          this.distance.x > 0 &&
          this.distance.x < 100 &&
          this.distance.y > 0 &&
          this.distance.y < 50
        ) {
          this.msg = "Wow, rude!";
        } else {
          if (
            this.distance.x < 250 &&
            this.distance.x > -250 &&
            this.distance.y < 200 &&
            this.distance.y > -200
          ) {
            this.msg = "Don't come closer!";
          } else {
            this.msg = "Thank you!";
          }
        }
      },
      deep: true,
      immediate: true
    }
  },
  methods: {
    handleClick: function() {
      this.msg = "You touched!";
      this.counter++;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
button {
  border: 1px solid lightblue;
  background: lightblue;
  cursor: pointer;
  width: 100px;
  height: 50px;
  &:hover,
  &:active {
    border: 1px solid red;
  }
}
</style>
