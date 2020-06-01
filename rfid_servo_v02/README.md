# Sistema de fechadura elétrica com RFID | Trava de porta v02

Primeiramente, vamos aos itens necessários:

| Quantidade | Componente |
| ---------- | ---------- |
| 1 | Arduino UNO |
| 1 | RFID – RC522 |
| 1 | Servo-Motor |
| ∞ | jumpers |
| 1 | Trinca de Porta |

## Vídeo: 

[vídeo](https://youtu.be/3iYkZ4IHtd8)

## Código para compilar no Arduino:

```
/***************************************\ 
**               Robotec               ** 
*            robotecweb.com.br          * 
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
* ESTE CODIGO É DA ROBOTEC COMPORATION  * 
*       FAVOR - MANTER O DOMINIO        *
**                                     ** 
\***************************************/

//Libs
#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>

//Ligações e definições
Servo myServo;
const int Buzzer = 6;
#define SS_PIN 10
#define RST_PIN 9
MFRC522 mfrc522(SS_PIN, RST_PIN);

//Variaveis
char st[20];

//Inicialização
void setup()
{
  pinMode(Buzzer, OUTPUT);
  myServo.attach(4);
  SPI.begin();
  mfrc522.PCD_Init();
}

//Loop
void loop()
{
  //verificação de novos cartões
  if ( ! mfrc522.PICC_IsNewCardPresent())
  {
    return;
  }
  //Seleciona um dos cartões
  if ( ! mfrc522.PICC_ReadCardSerial())
  {
    return;
  }
  String conteudo = "";
  byte letra;

  for (byte i = 0; i < mfrc522.uid.size; i++)
  {
    conteudo.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
    conteudo.concat(String(mfrc522.uid.uidByte[i], HEX));
  }

  conteudo.toUpperCase();


    if ((conteudo.substring(1) == "53 E4 02 2E") || (conteudo.substring(1) == "01 02 03 04")) //UID cartão e Celular
    {
      myServo.write(0); //função para abrir a porta
      digitalWrite(Buzzer, HIGH);
      delay(30);
      digitalWrite(Buzzer, LOW);
      delay(10000);
      myServo.write(90); //função para fechar a porta
      digitalWrite(Buzzer, HIGH);
      delay(30);
      digitalWrite(Buzzer, LOW);
    }
    else
    {
      digitalWrite(Buzzer, HIGH);
      delay(15);
      digitalWrite(Buzzer, LOW);
      delay(15);
      digitalWrite(Buzzer, HIGH);
      delay(15);
      digitalWrite(Buzzer, LOW);
      delay(15);     
    }
}
```

## Imagem do esquema: 

![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/rfid_servo_v02/Sistema-de-fechadura-eletrica-com-RFID-ligacoes.jpg)