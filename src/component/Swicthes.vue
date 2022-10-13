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
    // Нужно еще добавить инструмент который будет удалять нужную линию при удалении связи
    // Возможно нужно добавлять id линиям или каким-то еще способом, возможно пусть будут 
    // Нарисованы сразу все линии и добавить состояние для линий

    // Есть проблема с y нужно будет поправить, а именно не правильно высчитывается положение сверху от страницы, все кроме первых
    mounted() {
        window.addEventListener('load', () => {
            const swicthPosition = document.getElementById(`swicth${this.swicth.id}`).getBoundingClientRect();
            
            // нужно будет доработать x двя вариантов когда свич справо
            // Обозначение начальных координат линии от свича
            const start = {
                x: swicthPosition.x + swicthPosition.width,
                y: (swicthPosition.height / 2) + swicthPosition.top,
            }

            const app = document.getElementById('app')
            
            this.swicth.idHost.forEach(element => {
                // Оптимизировать
                if(`host${element}` === document.getElementById(`host${element}`).id) {
                    const hostPosition = document.getElementById(`host${element}`).getBoundingClientRect();
        
                    let d, tang, arctg, angle, scale, final;
                    // Обозначение конечных координат линии до хоста
                    final = {
                        x: (hostPosition.width / 2) + hostPosition.x,
                        y: (hostPosition.height / 2) + hostPosition.top,
                    }
                    
                    // Создаю линию и добавляю ее в #app
                    let line = document.createElement('div');
                    line.className = 'line'; // Линия 
                    app.appendChild(line);

                    d = Math.sqrt(Math.pow((final.x - start.x), 2) + Math.pow((final.y - start.y), 2)); // длина прямой после анимации
                    tang = (final.y - start.y) / (final.x - start.x) // Тангенс
                    arctg = Math.atan(tang); // Арктангенс
                    angle = arctg * 180 / Math.PI; // угол в градусах


                    // Тут какая-то ошибка иногда вектор отображается не в ту сторону на ровно на 180 градусов
                    // Нужно понять в каких и добавить не 90 градусов, а 270
                    console.log(tang);
                    console.log(this.swicth.id)
                    // debugger;


                    if (tang < 0) {
                        angle = 270 + angle;
                    } else if (tang > 0) {
                        angle = -(90 - angle);
                    }
                    // разворот всех стрелок которые с права (не четные) на 180 градусов
                    if (this.swicth.id % 2 == 0) {
                        angle = 180 + angle;
                    }

                    line.style.transform = `translate(${start.x}px, ${start.y}px) rotate(${angle}deg) translateZ(0)`;
                    
                    line.style.height = (d + 'px')
                    console.log(start.x)
                    console.log(start.y)
                }
            });
        })   
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
  