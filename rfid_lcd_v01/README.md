# RFID + LCD | Trava de porta v01

Já pensou em como funciona uma porta de hotéis por cartão? Não?! Neste post iremos explicar como funciona.

## Primeiramente, vamos aos itens necessários:

| Quantidade | Componente |
| ---------- | ---------- |
| 1 | Arduino UNO |
| 1 | RFID – RC522 |
| 1 | LCD 16×2 |
| ∞ | jumpers |
| 1 | potenciômetro 10k (ou 100k) |


## O que é RFID?
De acordo com a [Wikipedia](https://pt.wikipedia.org/wiki/Identifica%C3%A7%C3%A3o_por_radiofrequ%C3%AAncia), um RFID é: “Identificação por radiofrequência (Radio-Frequency IDentification), um método de identificação automática através de sinais de rádio, recuperando e armazenando dados remotamente através de dispositivos denominados etiquetas RFID.”

No RFID comprado em [UsinaInfo](https://www.usinainfo.com.br/rfid-arduino-e-ibutton/kit-rc522-leitor-rfid-tags-chaveiro-cartao-2582.html), podemos encontrar 1 cartão UID e 1 chaveiro UID, neles temos apenas a função de leitura de dados.

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
* ESTE CODIGO É DA ROBOTEC CORPORATION  * 
*       FAVOR - MANTER O DOMINIO        *
**                                     ** 
\***************************************/

//libs
#include <SPI.h>
#include <MFRC522.h>
#include <LiquidCrystal.h>


//ligações
#define SS_PIN 10
#define RST_PIN 9
MFRC522 mfrc522(SS_PIN, RST_PIN);   // Cria instância com MFRC522

//Define os pinos que serão utilizados para ligação ao display
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);

//variavel vetor 
char st[20];


//inicialização
void setup() 
{
  //define o numero de colunas do lcd
  lcd.begin(16, 2);
  lcd.clear();
  
  Serial.begin(9600);   // Inicia comunicação Serial em 9600 baud rate
  SPI.begin();          // Inicia comunicação SPI bus
  mfrc522.PCD_Init();   // Inicia MFRC522

  lcd.setCursor(1, 0);
  Serial.println("Aproxime o seu UID...");
  Serial.println();
  lcd.print("Apx o seu UID...");
  
}


//Loop
void loop() 
{
  
  //Verifica novos cartões
  if ( ! mfrc522.PICC_IsNewCardPresent()) 
  {
    return;
  }
  //Seleciona um dos cartões
  if ( ! mfrc522.PICC_ReadCardSerial()) 
  {
    return;
  }
  
  //Mostra UID na serial
  Serial.print("UID da tag:");

  String conteudo= "";
  byte letra;
  for (byte i = 0; i < mfrc522.uid.size; i++) 
  {
     Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
     Serial.print(mfrc522.uid.uidByte[i], HEX);
     conteudo.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
     conteudo.concat(String(mfrc522.uid.uidByte[i], HEX));
  }
  
  Serial.println();
  lcd.clear();
  lcd.setCursor(3, 0);
  lcd.print("unblocked:");
  conteudo.toUpperCase();
  
  if (conteudo.substring(1) == "EA 3A 4C 73") //UID do chaveiro
  {
    lcd.setCursor(4,1);
    lcd.print("chaveiro");
    Serial.println("Chaveiro identificado!");
    Serial.println();
    delay(3000);
    lcd.clear();
  }
  
  if (conteudo.substring(1) == "53 E4 02 2E") //UID do cartão
  {
    lcd.setCursor(5,1);
    lcd.print("cartao");
    Serial.println("Cartao identificado");
    Serial.println();
    delay(3000);
    lcd.clear(); 
  }
  
}
```

Não esqueça da instalação da biblioteca MFRC522. Clique [aqui](https://robotecweb.com.br/MFRC522.zip) para baixa-lá.

## Imagem do esquema:

![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/rfid_lcd_v01/SketchFeitoCLogo.jpg)

## Observações:
Para a instalação na porta, precisamos de 1 servo motor e um trinco. Não falarei a respeito neste post, pois tenho um [vídeo](https://youtu.be/csXSZ7oqHQA) explicativo de como funciona este dispositivo (trinco – servo motor).
Para maior segurança, os dados são enviados através de comunicação serial para um computador ou outra simulação.