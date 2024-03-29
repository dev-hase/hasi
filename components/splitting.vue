<template>

  <span data-splitting :class="actionclass"><slot></slot></span>

</template>

<script>

import "splitting/dist/splitting.css";
import "splitting/dist/splitting-cells.css";
import Splitting from "splitting";

export default {

    props: ["action"],
    data () {
        return {
            actionclass: 'headline--' + this.action
        }
    },
    mounted() {
        Splitting();
    }
}
</script>

<style lang="scss">

.word,
.char {
  animation-delay: var(--del);
  animation-direction: var(--dir, normal);
  animation-duration: var(--dur);
  animation-iteration-count: var(--it, infinite);
  animation-name: var(--name);
  animation-timing-function: var(--tf);
  animation-fill-mode: var(--fill, forwards);
  display: inline-block;
  position: relative;
  transform-origin: 50% 100%;
  z-index: 1;
}


// =========================
// Headline animations
// =========================

.headline--fall {
  .char {
    --name: fall;
    --dur: 600ms;
    --del: calc(var(--char-index) * -0.05s);
    --tf: cubic-bezier(0.165, 0.44, 0.64, 1);
  }

  @keyframes fall {
    0% {
      transform: rotateY(-25deg);
    }
    25% {
      transform: translateY(2%) rotateY(25deg);
    }
    50% {
      transform: rotateY(-25deg);
    }
    75% {
      transform: translateY(4%) rotateY(25deg);
    }
    100% {
      transform: rotateY(-25deg);
    }
  }
}

.headline--flip {
  .char {
    --name: flip;
    --dur: 4000ms;
    --del: calc(var(--char-index) * 0.075s);
    --tf: linear;
  }

  @keyframes flip {
    5% {
      transform: rotateX(1turn);
    }
    10% {
      transform: rotateX(2turn);
    }
    20% {
      transform: rotateX(3turn);
    }
    40% {
      transform: rotateX(4turn);
    }
    70%, 100% {
      transform: rotateX(5turn);
    }
  }
}

.headline--float {
  .char {
    --name: float;
    --dur: 2200ms;
    --del: calc(var(--char-index) * -0.5s);
    --tf: ease-in-out; 
    --dir: alternate;
    
    &:nth-child(2n) {
      --name: float-alt;
    }
  }
  
  @keyframes float {
    from {
      transform: translate(2%, -10%) rotate(-1deg);
    }
    to {
      transform: translate(-2%, 5%) rotate(3deg);
    }
  }

  @keyframes float-alt {
    from {
      transform: translate(0%, -5%) rotate(-1deg);
    }
    to {
      transform: translate(2%, 10%) rotate(3deg);
    }
  }
}

.headline--jog {
  .char {
    --name: jog;
    --dur: 500ms;
    --del: calc(var(--char-index) * -0.025s);
    --tf: linear;
  }

  @keyframes jog {
    0% {
      transform: translate(0, 0) rotate(5deg);
    }
    25% {
      transform: translate(5%, -5%) rotate(10deg);
    }
    50% {
      transform: translate(5%, 0) rotate(15deg);
    }
    75% {
      transform: translate(10%, -5%) rotate(10deg);
    }
    100% {
      transform: translate(0, 0) rotate(5deg);
    }
  }
}

.headline--jump {
  .char {
    --name: jump;
    --dur: 800ms;
    --del: calc(var(--char-index) * 0.075s);
    --tf: cubic-bezier(0.165, 0.44, 0.64, 1);
  }

  @keyframes jump {
    20% {
      transform: translateY(2%) scaleY(0.9);
    }
    40% {
      transform: translateY(-100%) scaleY(1.2);
    }
    50% {
      transform: translateY(10%) scaleY(0.8);
    }
    70% {
      transform: translateY(-5%) scaleY(1);
    }
    80%, 100% {
      transform: translateY(0) scaleY(1);
    }
  }
}

.headline--twirl {
  .char {
    --name: twirl;
    --dur: 6000ms;
    --del: calc(var(--char-index) * 0.025s);
    --tf: linear;
  }

  @keyframes twirl {
    2.5% {
      transform: rotateY(1turn);
    }
    5% {
      transform: rotateY(2turn);
    }
    10% {
      transform: rotateY(3turn);
    }
    20% {
      transform: rotateY(4turn);
    }
    40% {
      transform: rotateY(5turn);
    }
    70%, 100% {
      transform: rotateY(6turn);
    }
  }
}

.headline--fade {
  .char {
    --name: fade;
    --dur: 2s;
    --del: calc(var(--distance-percent) * 0.15s);
    --td: ease-in-out;
    
    transform-origin: 0 100%;
  }
  
  @keyframes fade {
    50% { opacity: 0; }
  }
}

.headline--ghost {
  .char {
    --name: rise;
    --dur: 3s;
    --del: calc(var(--distance-percent) * 0.125s);
    --tf: cubic-bezier(0.25, 0.46, 0.45, 0.94);
    
    transform-origin: 50% 100%;
    
    &:after {
      animation: ghost var(--dur) ease-in var(--del) infinite;
      content: attr(data-char);
      opacity: 0;
      transform-origin: 100% 50%;
      visibility: visible;
    }
  }
  
  @keyframes rise {
    40% {
      transform: 
        translateY(-40%)
        rotate(calc(var(--distance-sine) * 10deg)
      );
    }
    50% { transform: translateY( 6%); }
    55% { transform: translateY(-4%); }
    60% { transform: translateY( 2%); }
    65% { transform: translateY(-1%); }
    70% { transform: translateY( 0%); }
  }
  
  @keyframes ghost {
    8% {
      opacity: 0;
      transform: translateY(0); 
    }
    40% {
      opacity: 0.25;
      transform: 
        translateY(-30%)
        rotate(calc(var(--distance-sine) * -10deg)
      ); 
    }
    60%, 100% {
      opacity: 0;
      transform: translateY(-200%);
    }
  }
}

.headline--rock {
  .char {
    --name: rock;
    --dur: 2s;
    --td: ease-in-out;
    
    transform-origin: 0 100%;
  }
  
  @keyframes rock {
    0%, 100% { transform: rotate(-10deg); }
    50% { transform: rotate(-18deg); }
  }
}

.headline--sail {
  .word {
    --dur: 5s;
    
    &:before,
    &:after {
      animation: wave var(--dur) linear infinite;
      background-image: 
        radial-gradient(
          circle at 20px -30px,
          transparent 40px,
          var(--color) 41px
        );
      background-repeat: repeat-x;
      background-size: 40px 100%;
      content: '';
      height: 150%;
      left: 0;
      position: absolute;
      top: 90%;
      width: 200%;
      z-index: 2;
    }  
    
    &:after {
      animation-duration: calc(var(--dur) * 1.4);
      opacity: 0.8;
      top: 70%;
    }
  }
  
  .char {
    --name: sail;
    --del: calc(var(--char-index) * -0.15s);
    --tf: linear;
  }
  
  @keyframes sail {
    25% { transform: rotate(-1deg) translateY(2%); }
    50% { transform: rotate(0) translateY(0); }
    75% { transform: rotate(1deg) translateY(1%); }
  }
  
  @keyframes wave {
    to { transform: translateX(-200px); }
  }
}

.headline--shiver {
  .word {
    --name: shiver;
    --dur: 3s;
    --td: linear;
  }
  
  .char {
    --name: shiver-letter;
    --del: calc(var(--char-index) * -0.0125s);
    --dur: 140ms;
    --td: linear;
  }
  
  @keyframes shiver {
     1% { transform: translateX( 2%); }
     2% { transform: translateX(-2%); }
     3% { transform: translateX( 3%); }
     4% { transform: translateX(-3%); }
     5% { transform: translateX( 4%); }
     6% { transform: translateX(-4%); }
     7% { transform: translateX( 3%); }
     8% { transform: translateX(-3%); }
     9% { transform: translateX( 2%); }
    10% { transform: translateX(-2%); }
    11% { transform: translateX( 1%); }
    12% { transform: translateX( 0%); }
  }

  @keyframes shiver-letter {
    25% { transform: translateY( 1%); }
    50% {
      transform: translate(
        calc(var(--distance-percent) * 1%),
        calc(var(--distance-percent) * 1%)
      );
    }
    75% { transform: translateY( 1%); }
  }
}

.headline--yell {
  .char {
    --name: yell;
    --dur: 3s;
    --tf: ease;
    
    transform-origin: 50% 100%;
  }
  
  @keyframes yell {
    3% {
      transform:
        scale(calc(1 * var(--distance-percent) + 1.5)) 
        rotate(calc(15deg * var(--distance-sine)))
        translateY(-10%);
    }
    6% {
      transform:
        scale(calc(1 * var(--distance-percent) + 1.2)) 
        rotate(calc(15deg * var(--distance-sine)))
        translateY(-10%);
    }
    12% {
      transform:
        scale(calc(1 * var(--distance-percent) + 1.5)) 
        rotate(calc(15deg * var(--distance-sine)))
        translateY(-10%);
    }
    18% { transform: scaleY(1) translateY(-2%); }
    25% { transform: scaleY(0.98); }
    50% { transform: scaleY(1); }
    75% { transform: scale(0.98); }
  }
}

.headline--blink {  
  .char {
    --dur: 0.8s;
    --del: calc(var(--char-index) * 0.0125s);
    --name: blink;
    --tf: steps(1, start);
    
    opacity: 0;
  }
  
  @keyframes blink {
    50% { opacity: 1 }
  }
}

.headline--break {
  .char {
    --dur: 2s;
    --name: break-drop;
    --td: ease;
    
    color: transparent;
    overflow: visible;
    
    &:before,
    &:after {
      color: black;
      visibility: visible;
    } 
    
    &:before {
      animation: break-left var(--dur) linear infinite;
      clip-path: polygon(55% 0, 50% 25%, 55% 60%, 50% 120%, 0 100%, 0 0);
      transform-origin: 0 100%;
    } 
    
    &:after {
      animation: break-right var(--dur) linear infinite;
      clip-path: polygon(50% 0%, 100% 0, 100% 100%, 44% 120%, 53% 68%, 46% 22%);
      transform-origin: 100% 100%;
    } 
  }
  
  @keyframes break-drop {
    20% { transform: translateY(-100%); }
    22% { transform: translateY(10%); }
    25% { transform: translateY(-5%); }
    30% { transform: translateY(0); }
  }
  
  @keyframes break-left {
    22% { transform: rotate(0) }
    25% { transform: rotate(-8deg) }
    28% { transform: rotate(-10deg) }
    30%, 100% { transform: rotate(-5deg) }
  }
  
  @keyframes break-right {
    22% { transform: rotate(0) }
    25% { transform: rotate(5deg) }
    28% { transform: rotate(10deg) translateY(10%) }
    30%, 100% { transform: rotate(4deg) translateY(5%) }
  }
}

.headline--hide {
  --dur: 4s;
  
  .word:after {
    animation: hide-cover calc(var(--dur) * 2) ease-out infinite;
    border-top: 1vmin solid black;
    background-color: var(--color);
    content: '';
    height: 150%;
    left: 0;
    position: absolute;
    top: 100%;
    width: 100%;
    z-index: 2;
  }
  
  .char {
    --name: hide-jump;
    --del: calc(var(--char-index) * 0.04s);
    --td: cubic-bezier(0.215, 0.61, 0.355, 1);
    --dir: alternate;
    
    transform-origin: 50% 100%;
    
    &[data-char="i"]:after {
      --name: hide-peek;
      --dir: alternate;
      
      animation: var(--name) var(--dur) var(--td) infinite var(--dir);
      content: attr(data-char);
      visibility: visible;
    }
  }
  
  @keyframes hide-jump {
    0%, 10% { transform: translateY(0) }
    15% { transform: translateY(-25%) }
    20%, 100% { transform: translateY(100%) }
  }
  
  @keyframes hide-peek {
    0%, 35% { transform: translateY(0) }
    40%, 60% { transform: translateY(-40%) }
    70%, 90% { transform: translateY(-45%) skewY(10deg) }
    95%, 100% { transform: translateY(-46%) skewY(-10deg) }
  }
  
  @keyframes hide-cover {
    0%, 7% { transform: scaleX(0) }
    8%, 95% { transform: scaleX(1) }
    98%, 100% { transform: scaleX(0) }
  }
}

.headline--retreat {
  .word {
    animation: retreat-shrink 2s cubic-bezier(0.25, 1, 0.35, 1) infinite;
    transform-origin: 50% 100%;
  }
  
  .char {
    --name: retreat-stretch;
    --dur: 2s;
    --td: ease-out;
    
    transform-origin: 50% 100%;
  }
  
  @keyframes retreat-shrink {
    15% { transform: scale(1.001) }
    30%, 80% { transform: scale(0.25) }
    100% { transform: scale(1.001) }
  }
  
  @keyframes retreat-stretch {
    0%, 10% { transform: scaleY(1) }
    15% { transform: scaleY(0.5) }
    25% {
      transform:
        scaleY(4)
        rotate(calc(var(--distance-sine) * 65deg))
    }
    35% {
      transform:
        scaleY(0.80)
        rotate(calc(var(--distance-sine) * -25deg))
    }
    40% {
      transform:
        scaleY(1.10)
        rotate(calc(var(--distance-sine) * 15deg))
    }
    44% {
      transform:
        scaleY(0.98)
        rotate(calc(var(--distance-sine) * -10deg))
    }
    48% {
      transform:
        scaleY(1.01)
        rotate(calc(var(--distance-sine) * 5deg))
    }
    50% { transform: scaleY(1) }
  }
}

.headline--sway {  
  .char {
    --dur: 1s;
    --del: calc(var(--char-index) * -0.0125s);
    --name: sway;
    --td: linear;
    --dir: alternate;
  }
  
  @keyframes sway {
    from { transform: skew(-15deg) rotateX(10deg) }
      to { transform: skew(15deg) rotateX(-10deg) }
  }
}

.headline--tumble {
  .char {
    --dur: 0.8s;
    --name: bounce;
    --del: calc(var(--char-index) * -0.125s);
    --td: ease;
    
    color: transparent;
    overflow: visible;
    
    &:after {
      animation: tumble var(--dur) linear infinite;
      color: black;
      visibility: visible;
      z-index: 2;
    }
  }
  
  @keyframes bounce {
    25% { transform: translateY(-25%) }
    50% { transform: translateY(0) }
    75% { transform: translateY(-35%) }
  }
  
  @keyframes tumble {
    60% { transform: rotate(180deg) }
    100% { transform: rotate(360deg) }
  }
}
</style>
