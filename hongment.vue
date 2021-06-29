<template>
    <div class="hongmeng">
        <div class="container">
            <ul class="ul">
                <li class="harmony"></li>
            </ul>
            <ul class="ul">
                <li class="harmony"></li>
            </ul>
        </div>
        <svg>
            <filter id="blur">
                <feGaussianBlur in="SourceGraphic" stdDeviation="0 6"/>
            </filter>
        </svg>
    </div>
</template>
<script>

export default {
    mounted(){
        const filter = document.querySelector('feGaussianBlur')
        const clearFilter = () => {
            const value = parseFloat(filter.getAttribute('stdDeviation').split(' ')[1]) - 0.06
            if (value > 0) {
                filter.setAttribute('stdDeviation', `0 ${value}`)
                requestAnimationFrame(clearFilter)
            } else {
                return
            }
        }
        setTimeout(clearFilter, 1200)
    }
}
</script>
<style lang='scss' scoped>
    .hongmeng{
        width:100vw;
        height: 100vh;
        background: rgb(36, 32, 32);
    }
    .ul {
      position: relative;
      width: 100px;
      height: 50px;
      padding: 10px;
      list-style: none;
      overflow: hidden
    }
    .ul:first-of-type {
      padding-bottom: 0
    }
    .ul:last-of-type {
      padding-top: 0;
      /* margin-top: -2px; */
      /* animation: container-move .1s 1.2s forwards */
    }

    .harmony {
      position: absolute;
      top: 10px;
      left: 10px;
      width: 70px;
      height: 70px;
      border: 15px solid white;
      border-radius: 50%;
      transform: translateY(50%);
      box-shadow: 0 0 6px white, inset 0 0 6px white;
      animation: move 1.2s forwards
    }
    .ul:last-of-type > .harmony {
      top: auto;
      bottom: 10px;
      transform: translateY(-50%);
      filter: url(#blur)
    }

    svg {
      width: 0;
      height: 0
    }

    @keyframes move {
      to { transform: none }
    }

    /* @keyframes container-move {
      to { margin-top: 0 }
    } */
  </style>
