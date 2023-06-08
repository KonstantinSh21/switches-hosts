<template>
    <div :id="`swicth${swicth.id}`" class="swicthes">
      swicthes {{ swicth.id }}
      <div v-for="line of swicth.idHost">
        <div 
          class="line"
          :style='{transform: line.transform, height: line.height}'
        ></div>
      </div>
    </div>
</template>

<script>


export default {
  name: 'Swicthes',
  props: {
    swicth: Object,
  },

  mounted() {
    window.addEventListener('load', () => {
      this.positionLine();
    })
  },
  
  methods: {
    getXPosition(swicth, swicthPosition) {
      let x;
      swicth.id % 2 === 0 ? x = swicthPosition.x : x = swicthPosition.x + swicthPosition.width;
      return x;
    },
    positionLine() {
      const swicth = document.getElementById(`swicth${this.swicth.id}`);
      const swicthPosition = swicth.getBoundingClientRect();

      const start = {
        x: this.getXPosition(this.swicth, swicthPosition),
        y: (swicthPosition.height / 2) + swicth.offsetTop
      };

      this.swicth.idHost.forEach(element => {
        const hostName = `host${element.id}`;

        if (hostName === document.getElementById(hostName).id) {
          let height, tang, arctg, angle, final;
          // переделать на поиск по ref
          const host = document.getElementById(hostName);
          const hostPosition = host.getBoundingClientRect();

          // Обозначение конечных координат линии до хоста
          final = {
            x: (hostPosition.width / 2) + hostPosition.x,
            y: (hostPosition.height / 2) + host.offsetTop,
          };

          height = Math.sqrt(Math.pow((final.x - start.x), 2) + Math.pow((final.y - start.y), 2)) - 50; // длина прямой после анимации
          tang = (final.y - start.y) / (final.x - start.x); // Тангенс
          arctg = Math.atan(tang); // Арктангенс
          angle = arctg * 180 / Math.PI; // угол в градусах

          if (tang < 0) {
            angle = 270 + angle;
          } else if (tang > 0) {
            angle = -(90 - angle);
          }   

          // разворот всех линий которые с права (не четные) на 180 градусов
          if (this.swicth.id % 2 === 0) {
            angle = 180 + angle;
          }
          
          element.transform = `translate(${start.x}px, ${start.y}px) rotate(${angle}deg) translateZ(0)`;
          element.height = (height + 'px');
        }
      });
    }
  },
}
</script>

<style>
.swicthes {
  width: 200px;
  border: 3px solid #000;
  margin: 20px 0;
  border-radius: 20px;
  height: 300px;
  box-sizing: border-box;
}

.swicthes:nth-child(2n+1) {
  margin-right: 50%;
}

.lines {
  position: absolute;
}

.line {
  position: absolute;
  width: 2.5px;
  background-color: #000000;
  height: 80px;
  left: 0;
  top: 0;
  transform: translateZ(0);
  transform-origin: 50% 0%;
}

.line:hover {
  background-color: red;
  z-index: 1;
}
</style>
