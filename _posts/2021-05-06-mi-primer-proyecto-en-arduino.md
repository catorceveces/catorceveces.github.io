---
layout: post
title: Mi primer proyecto en Arduino
tags: [arduino, electronica, programacion]
---

La [técnica de productividad Pomodoro](https://es.wikipedia.org/wiki/Técnica_Pomodoro) consiste en contabilizar bloques de tiempo de 25 minutos, seguidos de pausas de 5 minutos, y descansos más largos luego de cuatro ciclos. El fundamento es eliminar las interrupciones, debido a que, durante el lapso de 25 minutos, se debe estar absolutamente focalizado en aquello que se está haciendo.

La estructura podría expresarse de este modo:

* Efectuar una tarea durante 25 minutos.
* Descansar 5 minutos.
* Repetir los incisos anteriores cuatro veces.
* Efectuar un descanso extenso de 20 minutos.
* Repetir.

Existen aplicaciones para el celular que temporizan los bloques de cada ciclo Pomodoro. Sin embargo, que utilicemos una app para mejorar nuestra productividad a través de un método que busca *eliminar las distracciones* no parece una gran idea. Basta con que agarremos el celular para distraernos.

Entonces pensé en armar un prototipo de gadget en Arduino. Algo que podamos tener en el escritorio, dedicado sólo a cumplir la función de contabilizar ciclos.

### Elementos empleados.

* Arduino Nano.
* Protoboard principal.
* Protoboard secundaria.
* LCD 16x02. — Basada en Hitachi HD44770.
* Potenciómetro lineal de carbón de 10K. — Regulación del contraste del LCD.
* Dos resistencias de 200 Ohm.
* Dos resistencias de 10 kOhm.
* Dos botones.
* Dos luces LED.
* Cables macho/macho para realizar las conexiones.

<div class="row" align="center">
	<img src="https://raw.githubusercontent.com/catorceveces/pomobox/main/pics/image.jpeg" width="560" height="315">
</div>

### Idea de funcionamiento.

Sencillo. Al enchufar el Arduino, la pantalla LCD ingresará a un menú de inicio: al presionar un botón comenzará a contabilizar ciclos Pomodoro (y se exhibirán en pantalla cuántos hemos completado en la sesión). Al presionar otro botón, el proceso se cancelará, reiniciando los valores.

### Esquema.

<div class="row" align="center">
	<img src="https://raw.githubusercontent.com/catorceveces/pomobox/main/pics/scheme.png" width="560" height="315">
</div>

### Problemas de código.

Ya construido el circuito, tenemos que resolver dos problemas importantes inherentes a la programación:

* Recordar el estado (o modo) que se desea al presionar un botón *y soltarlo*.

El funcionamiento de un botón en un circuito electrónico está dado por la conexión de una de sus patas a 5 voltios y la restante a ground. En la medida en que el botón NO es presionado, no hay conexión entre las dos patas del botón, y el pin de comunicación con Arduino es bajado a ground a través de la resistencia. Al presionarlo, ambas patas se conectan, el circuito se cierra y el pin recibe los 5 voltios.

De esto surge que, para iniciar el ciclo de Pomodoro presionando uno de los botones, necesitamos que el Arduino “recuerde” de algún modo que el botón fue presionado. Puesto que mantenerlo constantemente pulsado sería imposible. — Es decir, que al presionar el botón, el circuito se cierre y se abra, pero que operativamente funcione como si el circuito se mantuviera cerrado (que inicie el temporizador de bloques Pomodoro).

¿Solución? Definir variables globales con valores booleanos que usaremos en el void loop:

```
// variables globales

int pomoState = LOW;        // check instance
int currentPlay;            // estado de play
int currentStop;            // estado de stop
int previousPlay = HIGH;    // última pulsación

void setup() {
                            // código del void setup()
}

void loop() {

	currentPlay = digitalRead(playPin);			// lectura del estado de play

	if (currentPlay == HIGH && previousPlay == HIGH) {	// si es igual a previosPlay
  	if (pomoState == LOW) {					// si pomoState está en LOW

      pomoState = HIGH;						 // cambia el valor booleano
      currentStop = digitalRead(stopPin);			// asignamos valor a currentStop

      while (digitalRead(stopPin) == currentStop) {     	// registrada la pulsación de play
			}					// se ejecutará el código dentro
		}						// del while loop, hasta que se
	}							// presione el botón de stop

	if (digitalRead(stopPin) != currentStop) {           	// lectura del botón de stop
		pomoState = LOW;      
  }

  previousPlay = currentPlay;

}
```

Ver en [Gist](https://gist.github.com/catorceveces/9b600154d177d88ecab4260501f86fe1)

* While loop. Limitación a cláusulas if / else.

Una vez que resolvimos el punto anterior, debemos escribir el código que se ejecutará dentro del while loop (mientras NO se presione el botón de stop). Al ejecutar código DENTRO de un while, no podemos emplear otros loops si queremos registrar la pulsación del stop (detener el ciclo). Otros loops nos mantendrían dentro del bucle indefinidamente. De modo que la lógica de los bloques de tiempo debemos construirla limitándonos a cláusulas if / else. Al mismo tiempo, es necesario registrar la cantidad de ciclos de 25 minutos, puesto que, luego de 4 períodos, corresponde un descanso largo de 20 minutos. Para ello, definimos otras variables globales. Una registrará si estamos en descanso o no (boolean), y la restante registrará la cantidad de ciclos Pomodoro realizados.

```
// variable global

periods = 0;
boolean onBreak = false;

void setup() {
                                                // código del void setup()
}

void loop() {

    while (digitalRead(stopPin) == currentStop) {         // del fragmento de código previo

      if (onBreak == false) {                             // comienza a contar un ciclo de 25 min      
        // código que finaliza en:      
      periods ++;
      onBreak = true;
      }

      else if (onBreak == true && periods % 4 !=0) {      // comienza a contar un ciclo de 5 min      
        // código que finaliza en:      
      onBreak = false;
      }

      else if (onBreak == true && periods % 4 == 0) {     // comienza a contar un ciclo de 20 min      
        // código que finaliza en:                        // ya que los ciclos realizados son      
      onBreak = false;                                    // un múltiplo de 4
      }

    }
}
```

Ver en [Gist](https://gist.github.com/catorceveces/3bf6cb94bbd5dd40c698d293e3292001).

El resultado:

<div class="row" align="center">
<iframe align="center" width="560" height="315" src="https://www.youtube.com/embed/g9jUZnzG37Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

El código completo con esquemáticos en [GitHub](https://github.com/catorceveces/pomobox).
