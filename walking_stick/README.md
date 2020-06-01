# Bengala com Arduino

Basicamente neste projeto, sua ideia principal é de ajudar pessoas com deficiência visual (baseado em Arduíno) para garantir mais segurança ao caminhar. Ao se aproximar de algum objeto (obstáculo), a bengala apita, e ao se distanciar ela para de apitar. Não é nada complexo, apenas algumas linhas de código já podem garantir esse resultado.  

## Componentes:
| Quantidade | Componente |
| ---------- | ---------- |
| 1 | Arduino Uno |
| 1 | Sensor ultrassônico |
| ∞ | Jumpers |
| 1 | Buzzer |
| 1 | Protoboard (a sua escolha) |

## Imagem / Ideia:

![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/walking_stick/esquematico.png)

(De acordo com está imagem, você devera trocar os leds por 1 buzzer. Ligação simples, liguei o negativo no negativo e o positivo no positivo.)

## Vídeo: 
[clique aqui](https://youtu.be/iLylzgxo4Ts)

```
/***************************************\ 
**               Robotec               ** 
*          www.robotecweb.com.br        * 
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
int pingPin = 13; //entrada que emite
int entradaPin = 12; //entrada que recebe
 
int ledRojo = 5; //LED vermelho entrada 5
int ledVerde = 7; //LED verde entrada 7
 
int inSegura =  25;
 
void setup(){
  
  //Inicializamos os pinos com entrada e saida
  pinMode(pingPin, OUTPUT);
  pinMode(ledRojo, OUTPUT);
  pinMode(ledVerde, OUTPUT);
  pinMode(entradaPin, INPUT);
  
  Serial.begin(9600); //Inicializamos a comunicação serial
  
}
 
void loop(){
  
 //criamos duas variaveis, uma para duracao e outra para a distancia de longa duração, distancia em cm

  digitalWrite(pingPin, LOW); // Envia um pulso baixo
  delayMicroseconds(2);       // Espera 2 microsegundos
  digitalWrite(pingPin, HIGH);// Envia um pulso alto
  delayMicroseconds(5);       // Espera 5 microsegundos
  digitalWrite(pingPin, LOW); // Em espera
  
  /*
  Converemos a duracão do tempo a distancia
  a velocide do som é de 340metros/segundo que 
  é igual a 29 microsegundos por centimetro é por isto
  que vamos a dividir a duracão entre 29. 
  Depois de dividir entre 2 porque o tempo que viaja
  o som de ida e de volta, entao queremos um valor no qual
  ambos som's sao iguais, e é por isto que o som dividimos
  entre 2
  */

  distanciaEnCm = (duracion/29)/2;
  
  //Imprimimos a distancia
  Serial.print(distanciaEnCm);
  Serial.print("cm");
  Serial.println();
  

  if(distanciaEnCm > inSegura){
  
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledRojo, LOW);
      
  }
  else{
    
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledRojo, HIGH);
    
  }
  
  //delay
  delay(1000);
  
}
```