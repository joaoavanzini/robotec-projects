# Estacionamento por Arduíno
Projeto estacionamento controlado por Arduíno Uno. Neste projeto, a ideia principal seria criar um estacionamento automatizado, onde mostra o dinheiro a ser pago, abre e fecha a cancela. Um projeto simples, porém bem legal a quem inicia neste mundo de microcontroladores.

## Componentes:

| Quantidade | Componente |
| ---------- | ---------- | 
| 1 | Arduino Uno |
| 1 | Servo Motor |
| 2 | Potenciômetros de 10k (ou 100k) |
| 1 | Tela lcd 16×2 caracteres |
| ∞ | Jumpers |

## Vídeos:
[1º Vídeo](https://youtu.be/EeewydyNeo0)
[2º Vídeo](https://youtu.be/Ka7J6hLeSoE)
[3º Vídeo](https://youtu.be/ioQXcg3PAIQ)

## Imagem / Ideia:
![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/automated_parking/projeto-estacionamento.png)

```
/***************************************\ 
**               Robotec               ** 
*           robotecweb.com.br           * 
*                                       *
*      inscreva-se no nosso canal       *
*    www.youtube.com/c/Roboteclink      *
*                                       *
*        curta a nossa fampage          *
*   www.facebook.com/Robotecoficial/    *
*                                       *
* ESTE CODIGO É DA ROBOTEC CORPORATION  * 
*       FAVOR - MANTER O DOMINIO        *
**                                     ** 
\***************************************/
#include "LiquidCrystal.h" //biblioteca para controle de telas LDCs
#include "Servo.h"         //biblioteca para controle de servomotores
 
//Criando um objeto da classe LiquidCrystal e
//inicializando com os pinos da interface.
LiquidCrystal lcd(9, 8, 5, 4, 3, 2);
Servo servoMotorObj;  //Criando um objeto da classe Servo
 
int const potenciometroPin = 0;  //pino analógico onde o potenciômetro está conectado
int const servoMotorPin    = 12; //pino digital associado ao controle do servomotor
int valPotenciometro;            //variável usada para armazenar o valor lido no potenciômetro
 
void setup() {
  //Inicializando o LCD e informando o tamanho de 16 colunas e 2 linhas
  //que é o tamanho do LCD JHD 162A usado neste projeto.
  lcd.begin(16, 2);
 
  //associando o pino digital ao objeto da classe Servo  
  servoMotorObj.attach(servoMotorPin);
}
 
void loop() {
  valPotenciometro = analogRead(potenciometroPin); //lendo o valor do potenciômetro (intervalo entre 0 e 1023)
 
 
  //mapeando o valor do potenciômetro para a escala do servo (0 e 180)
 
  valPotenciometro = map(valPotenciometro, 0, 1023, 0, 180);
 
 
  servoMotorObj.write(valPotenciometro); //definindo o valor/posição do servomotor  
    
  lcd.clear();                 //limpa o display do LCD.     
  lcd.print("estacionamento");     //imprime a string no display do LCD.
 
  lcd.setCursor(0,1);          //posiciona o cursor na coluna 0 linha 1 do LCD.
 
  //Mostrando no lcd a posição do braço do servomotor
  if (valPotenciometro < 90) {
    lcd.print("R$1.00:30 min");
  }   
  if (valPotenciometro == 90) {
    lcd.print("Centro");
  }   
  if (valPotenciometro > 90) {
    lcd.print("R$2.5o: 3 horas");
  }
 
  delay(30);            
}
```