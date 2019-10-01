<template>
  <div class="container">
    <div class="button-container">
      <h1>
        <p>{{ msg }}</p>
      </h1>
      <button class="left" id="button"></button>
    </div>
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
    msg: function() {
      if (this.msg == "Don't come closer!") {
        button.classList.add("angry");
        button.classList.remove("sad");
      } else if (this.msg == "Wow, rude!") {
        button.classList.add("sad");
        button.classList.remove("angry");
      } else {
        button.classList.remove("angry");
        button.classList.remove("sad");
      }
    },
    $props: {
      handler(props) {
        (this.mousePos.x = props.coords.x), (this.mousePos.y = props.coords.y);
        this.distance.x = props.coords.x - this.elementPos.x;
        this.distance.y = props.coords.y - this.elementPos.y;
        if (this.distance.x < 0) {
          button.classList.add("left");
          button.classList.remove("right");
        } else {
          button.classList.add("right");
          button.classList.remove("left");
        }
        if (this.distance.y < 0) {
          button.classList.add("top");
          button.classList.remove("bot");
        } else {
          button.classList.add("bot");
          button.classList.remove("top");
        }
        if (
          this.distance.x > 0 &&
          this.distance.x < 100 &&
          this.distance.y > 0 &&
          this.distance.y < 50
        ) {
          this.msg = "Wow, rude!";
          this.counter++;
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
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped lang="scss">
button {
  border: 1px solid lightblue;
  background: lightblue;
  cursor: pointer;
  width: 100px;
  height: 50px;
  position: relative;
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    width: 15px;
    height: 15px;
  }
}
.left {
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    content: "";
    display: inline-block;
    position: absolute;
    background: white;
    border-radius: 50%;
  }
  &::before {
    left: 0;
    top: 0;
  }
  &::after {
    right: 20px;
    top: 0;
  }
}
.right {
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    content: "";
    display: inline-block;
    position: absolute;
    background: white;
    border-radius: 50%;
  }
  &::before {
    left: 20px;
    top: 0;
  }
  &::after {
    right: 0;
    top: 0;
  }
}
.top {
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    content: "";
    display: inline-block;
    position: absolute;
    background: white;
    border-radius: 50%;
  }
  &::before {
    top: 0px !important;
  }
  &::after {
    top: 0px !important;
  }
}
.bot {
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    content: "";
    display: inline-block;
    position: absolute;
    background: white;
    border-radius: 50%;
  }
  &::before {
    top: 30px !important;
  }
  &::after {
    top: 30px !important;
  }
}
.angry {
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    width: 15px;
    height: 10px;
    background-color: maroon;
  }
  &::before {
    transform: rotate(30deg);
  }
  &::after {
    transform: rotate(-30deg);
  }
}
.sad {
  &::before,
  &::after {
    transition: all 0.2s ease-in-out;
    width: 18px;
    height: 20px;
    background-color: blue;
  }
  &::before {
    transform: rotate(-10deg);
    left: 0;
    bottom: 0;
  }
  &::after {
    transform: rotate(15deg);
    right: 0;
    bottom: 0;
  }
}
.button-container {
  position: relative;
  h1 {
    position: absolute;
    top: -140px;
    left: 50px;
    padding: 10px;
    margin: 0;
    border: 1px solid lightblue;
    font-size: 22px;
    width: 200px;
    &::after {
      position: absolute;
      content: "";
      border-bottom: 1px solid lightblue;
      border-right: 1px solid lightblue;
      width: 40px;
      height: 40px;
      left: 20px;
      bottom: -21px;
      background: white;
      transform: rotate(45deg);
    }
    span {
      display: inline-block;
      z-index: 10;
    }
  }
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
}
</style>
