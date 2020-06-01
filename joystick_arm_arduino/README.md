# Braço robótico controlado por Joystick's

Que tal controlar um braço robótico no estilo gamer? É isso oque vamos fazer! Para a construção deste, precisaremos de: 1 Arduino uno, 1 Arduino shield control v5.0, 1 mini braço robótico e 1 controle com joysticks – alguns jumpers serão necessários.

[Video](https://youtu.be/d--jv4dV-y4)

## Código: 

```
/***************************************\ 
**               Robotec               ** 
*            robotecweb.com.br          * 
*                                       *
*                                       *
*               UsinaInfo               *
*            usinainfo.com.br           *
*                                       *
*      inscreva-se no nosso canal       *
*       youtube.com/Roboteclink         *
*                                       *
*        curta a nossa fampage          *
*     facebook.com/Robotecoficial       *
*                                       *
* ESTE CODIGO É DA ROBOTEC CORPORATION  * 
*       FAVOR - MANTER O DOMINIO        *
**                                     ** 
\***************************************/

#include <VarSpeedServo.h> //Inclusão da biblioteca VarSpeedServo.h

/*Programação orientada a objeto - Criação de cada objeto para o movimento*/  
VarSpeedServo arm_up; //Novo objeto para o controle do servo para o movimento da subida
VarSpeedServo arm_front; //Novo objeto para o controle do servo para o movimento da frente
VarSpeedServo arm_claw; //Novo objeto para o controle do servo para o movimento da garra
VarSpeedServo arm_body; //Novo objeto para o controle do servo para o movimento do corpo - esquerda e direita
 
/*Inicialização do pino analógico para os eixos correspondentes ao movimento*/
int pino_x = A0; //Inicializa o pino analógico ao eixo X do joystick
int pino_y = A1; //Inicializa o pino analógico ao eixo Y do joystick
int pino_z = A3; //Inicializa o pino analógico ao eixo Z do joystick
int pino_w = A4; //Inicializa o pino analógico ao eixo W do joystick

/*Armazenamento do valor lido do joystick - ele será utilizado para a direção do movimento*/
int val_x; //Armazena o valor lido pelo eixo X do joystick
int val_y; //Armazena o valor lido pelo eixo Y do joystick
int val_z; //Armazena o valor lido pelo eixo Z do joystick
int val_w; //Armazena o valor lido pelo eixo W do joystick


/*Define as portas em que o servo motor está conectado ao Arduino*/
void setup() {
 arm_up.attach(8, 1, 180); //Define que o servo está conectado a porta 8 do Arduino
 arm_front.attach(0, 1, 180); //Define que o servo está conectado a porta 0 do Arduino
 arm_claw.attach(6, 1, 180); //Define que o servo está conectado a porta 6 do Arduino
 arm_body.attach(11, 1, 180); //Define que o servo está conectado a porta 11 do Arduino
}

/*Toda parte de movimentação, utilizando todos esses valores que estão aqui:*/
void loop() {
 val_x = analogRead(pino_x); //Recebe o valor lido pelo eixo X do joystick
 val_x = map(val_x, 0, 1023, 1, 180); //Converte o valor lido para um valor em graus (1 a 180º)
 arm_up.slowmove(val_x, 45); //Movimenta o servo até a posição definida pelo eixo X
 
 val_y = analogRead(pino_y); //Recebe o valor lido pelo eixo Y do joystick
 val_y = map(val_y, 0, 1023, 1, 180); //Converte o valor lido para um valor em graus (1 a 180º)
 arm_front.slowmove(val_y, 45); //Movimenta o servo até a posição definida pelo eixo Y
  
 val_z = analogRead(pino_z); //Recebe o valor lido pelo eixo Z do joystick
 val_z = map(val_z, 0, 1023, 1, 180); //Converte o valor lido para um valor em graus (1 a 180º)
 arm_claw.slowmove(val_z, 60); //Movimenta o servo até a posição definida pelo eixo Z
 
 val_w = analogRead(pino_w); //Recebe o valor lido pelo eixo W do joystick
 val_w = map(val_w, 0, 1023, 1, 180); //Converte o valor lido para um valor em graus (1 a 180º)
 arm_body.slowmove(val_w, 20); //Movimenta o servo até a posição definida pelo eixo W
 
 delay(30);
}
```

# Esquemático: 

![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/joystick_arm_arduino/bracorobotico.jpg)

| Links |
| ----- |
| [Braço Robótico](https://www.usinainfo.com.br/mini-bracos-roboticos/braco-robotico-em-mdf-para-arduino-completo-manual-de-montagem-3405.html) |
| [JoyStick](https://www.usinainfo.com.br/joystick-e-controles-ir/kit-joystick-arduino-em-acrilico-com-comando-analogico-duplo-parafusos-de-fixacao-5175.html) |
| [Arduino Sensor Shield V5](https://www.usinainfo.com.br/shields-para-arduino/arduino-sensor-shield-expansor-de-entradas-e-saidas-v50-3522.html) |