<template>
  <div :id="`swicth${swicth.id}`" class="swicthes">
    swicthes {{ swicth.id }}
  </div>
</template>

<script>


export default {
  name: 'Swicthes',
  props: {
    swicth: Object,
  },
  data() {
    return {
      lines: [],
    }
  },
  mounted() {
    window.addEventListener('load', () => {
      const swicth = document.getElementById(`swicth${this.swicth.id}`);
      const swicthPosition = swicth.getBoundingClientRect();

      const start = {
        x: this.getXPosition(this.swicth, swicthPosition),
        y: (swicthPosition.height / 2) + swicth.offsetTop
      };

      const app = document.getElementById('app');

      this.swicth.idHost.forEach(element => {
        const hostName = `host${element}`;

        if (hostName === document.getElementById(hostName).id) {
          let height, tang, arctg, angle, final;
          const host = document.getElementById(hostName);
          const hostPosition = host.getBoundingClientRect();

          // Обозначение конечных координат линии до хоста
          final = {
            x: (hostPosition.width / 2) + hostPosition.x,
            y: (hostPosition.height / 2) + host.offsetTop,
          };

          // Создаю линию и добавляю ее в #app
          let line = document.createElement('div');
          line.className = 'line'; // Линия
          this.lines.push({id: this.lines.length});
          app.appendChild(line);

          height = Math.sqrt(Math.pow((final.x - start.x), 2) + Math.pow((final.y - start.y), 2)); // длина прямой после анимации
          tang = (final.y - start.y) / (final.x - start.x) // Тангенс
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

          // назначаю
          line.style.transform = `translate(${start.x}px, ${start.y}px) rotate(${angle}deg) translateZ(0)`;
          line.style.height = (height + 'px');
        } else {
          
        }
      });
    })
  },
  methods: {
    getXPosition(swicth, swicthPosition) {
      let x;
      swicth.id % 2 === 0 ? x = swicthPosition.x : x = swicthPosition.x + swicthPosition.width;
      return x;
    }
  },
  watch: {

  }
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

.line {
  position: absolute;
  width: 2.5px;
  background-color: red;
  height: 80px;
  left: 0;
  top: 0;
  transform: translateZ(0);
  transform-origin: 50% 0%;
}
</style>
