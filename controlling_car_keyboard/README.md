# Comunicação serial / L298N / Carrinho

Sabe aqueles jogos que você usa apenas os botões direcionais (setinhas para cima, para baixo, para a esquerda e direita)? Então! Este projeto utilizaremos os botões ‘W’, ‘A’, ‘S’, ‘D’, para o controle de esquerda, direita, ir para frente e ir para trás de um carrinho. Este carrinho será baseado em um l298n (respectivamente com um Arduíno uno). Muito bacana este projeto pelo fato da comunicação simultânea entre o Arduíno e o computador.


## Componentes:
| Quantidade | Componente |
| ---------- | ---------- | 
| 1 | Arduino Uno |
| ∞ | Jumpers |
| 2 | Motores Mabuchi |
| 1 | L298N (ponte H) |
| 1 | Porta pilhas|

## Imagem / Ideia:

![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/controlling_car_keyboard/Circuito.png)

## Código: 

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
 
const int led = 10; //buzina
int EstadoBotao = 0; //Variavel para ler o status do pushbutton 
int IN1 = 4; //numero da porta do que devo ligar =IN1
int IN2 = 5;//numero da porta do que devo ligar =IN2
int IN3 = 6;//numero da porta do que devo ligar = IN3
int IN4 = 7;//numero da porta do que devo ligar = IN4
int temp = 250; //define tempo de execução 
void setup() //inicia o programa 
{
 
  Serial.begin(9600);   //numero da porta serial padrao 
  pinMode(led, OUTPUT); 
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
}
 
void loop()  // loop
{ 
 
  if (Serial.available() > 0) {   // biblioteca serial .aVailable
 
    char ler = int(Serial.read()); // define com o nome ler 
 
    switch (ler) { 
    case 'w':   //comando no teclado 
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, HIGH);
      digitalWrite(IN3, HIGH);
      digitalWrite(IN4, LOW);
      delay(temp);
      Serial.println("Frente"); // define para ir para frente
      break;
    case 'a'://comando do teclado 
      digitalWrite(IN1, HIGH);
      digitalWrite(IN2, LOW);
      digitalWrite(IN3, HIGH);
      digitalWrite(IN4, LOW);
      delay(temp);   
      Serial.println("Esquerda"); // define para ir para esquerda 
      break;
    case 'd':  ///comando do teclado
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, HIGH);
      digitalWrite(IN3, LOW);
      digitalWrite(IN4, HIGH);
      delay(temp); 
      Serial.println("Direita"); //define para ir para a direita 
      break;
    case 's': //comando do teclado
      digitalWrite(IN1, HIGH);
      digitalWrite(IN2, LOW);
      digitalWrite(IN3, LOW);
      digitalWrite(IN4, HIGH);
      delay(temp);   
      Serial.println("Tras"); // define para ir para tras 
      break;
    case 'o'://comando do teclado 
      digitalWrite(led, HIGH);
      delay(temp);   
      Serial.println("buzina"); // define para ir para esquerda
    case 'i'://comando do teclado 
      digitalWrite(led, LOW);
      delay(temp);   
      Serial.println("buzina desligada"); // define a buzina
  }
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, HIGH);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, HIGH);
    //delay(1);       
  }
 
 
}
```