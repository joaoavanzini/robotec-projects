# Fechadura eletrônica / Assistente pessoal (COM ARDUINO)

Provavelmente você já ouviu falar em mecanismos que fazem de tudo um pouco (algo bem futurista), mas, já estamos vivendo esta época, onde tudo é algo programável e comandado. Esta fechadura, não passa de um simples programa editável. Suas funcionalidades são: abrir e fechar uma tranca, mostrar temperatura do ambiente, luminosidade do ambiente, horário e dizer um simples bem-vindo.  Algumas horas de “coding” já chegamos a nosso resultado, que, não é tão simples quanto possamos imaginar. 

# Componentes:
| Quantidade | Componente |
| ---------- | ---------- | 
| 1 | Arduino Uno |
| ∞ | Jumpers |
| 1 | Protoboard (a sua escolha) |
| 1 | Servo motor |
| 1 | Buzzer |
| 1 | lcd (16×2 caracteres) |
| 1 | Sensor de luminosidade LDR 5mm |
| 1 | Sensor de temperatura NTC 10k 3mm |
| 1 | Sensor detector infravermelho IR |
| 3 | Resistores 10kΩ |
| 1 | Potenciômetro de 10k (ou 100k) |

# Imagem / Ideia:

![Esquemático](https://github.com/vicpb/robotec-projects/blob/master/int_lock_assist/Fechadura-eletronica.jpeg)

# Vídeo:
[Clique aqui](https://youtu.be/csXSZ7oqHQA)

# Código: 

```
/***************************************\ 
**               Robotec               ** 
*            robotecweb.com.br          * 
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
 
#include <IRremote.h>//biblioteca do controle remoto
#include <Servo.h> //biblioteca do servo motor
#include <LiquidCrystal.h> //biblioteca do lcd
 
Servo myservo;
int RECV_PIN = 8;//pino do controle
int seg=0,//segundos da hora
min=23,//minutos da hora
hor=14;//tempo da hora
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);//pinagem do lcd
const int Buzzer = 6;//pinagem do buzzer
const int PinoSensor = 0 ;//pinagem do sensor de temperatura
int ValorSensor = 0;
const int LDR = 1 ;//pinagem do sensor de luminosidade
int ValorLido = 1;
 
IRrecv irrecv(RECV_PIN);
 
decode_results results;
 
void setup()
{
  pinMode(Buzzer, OUTPUT);
  myservo.attach(9);
  Serial.begin(9600);
  irrecv.enableIRIn(); // Iniciou o receptor
 
  lcd.begin(16, 2);//bortão de entrada
  lcd.setCursor(1,0);
  lcd.print("Seja Bem-Vindo!");
  lcd.setCursor(3,1);
  lcd.print("Joao Victor");//seu nome
}
 
void loop() {
 
  if (irrecv.decode(&results)) {
    String s = String(results.value, HEX); //decodificar os resultados em hexadecimal do controle 
    if(s != "ffffffff"){
      Serial.println(s);
    }
 
    if(s == "e12458a7"){//função de girar o servo para fechar a porta
      myservo.write(2370);
      lcd.begin(16, 2); 
      lcd.setCursor(0, 0);
      lcd.print("'''''FECHADO'''''");
      lcd.setCursor(0,1);
      lcd.print(" YT/Roboteclink");
      digitalWrite(Buzzer, HIGH);
      delay(500); 
    }
    else if(s == "e124a05f"){
      myservo.write(570); // função de girar o servo para abrir a porta
      lcd.begin(16, 2); 
      lcd.setCursor(0, 0);
      lcd.print("'''''ABERTO'''''");
      lcd.setCursor(0,1);
      lcd.print(" YT/Roboteclink");
      digitalWrite(Buzzer, HIGH);
      delay(500); 
    }
 
   else if (s == "e12440bf"){ // relogio
   static unsigned long ult_tempo = 0;
int tempo = millis();
if(tempo - ult_tempo >= 1000) {
ult_tempo = tempo;
seg++;
}
if(seg>=60) {
seg = 0;
min++;
}
if(min>=60) {
min = 0;
hor++;
}
if(hor>=24) {
hor=0;
min=0;
}
lcd.clear();
lcd.setCursor(8,0);
lcd.print(hor);
lcd.setCursor(10,0);
lcd.print(":");
lcd.setCursor(11,0);
lcd.print(min);
lcd.setCursor(13,0);
lcd.print(":");
lcd.println(seg);
lcd.setCursor(0,0);
lcd.print("HORARIO:");
lcd.setCursor(0,1);
lcd.print(" YT/Roboteclink");
digitalWrite(Buzzer, HIGH);
delay(500); 
   }
   else if (s == "e124609f"){ // opção para deixar o arduino mudo
    pinMode(Buzzer, LOW);
   }
   else if (s == "e124e817"){// opção para deixaro arduino com o som
    pinMode(Buzzer, HIGH);
   }
   else if (s == "e12428d7"){//opçao para fazer o arduino mostrar a temperatura
    ValorSensor = analogRead(PinoSensor);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print(ValorSensor);
    digitalWrite(Buzzer, HIGH);
    delay(500);
   }
  else if (s == "e1246897"){
    ValorLido = analogRead(LDR);//opção para fazer o arduino mostrar a luminosidade
    if (ValorLido < 341){//se menor que 341, constar que tem pouca luminosidade
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.print(ValorLido);
      lcd.setCursor(0,1);
      lcd.print("pouca luz");
      digitalWrite(Buzzer, HIGH);
      delay(500);
    }
    if(ValorLido > 341){//se maior que 341 , constar que tem uma luminosidade boa no ambiente
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.print(ValorLido);
      lcd.setCursor(0,1);
      lcd.print("luminosidade boa");
      digitalWrite(Buzzer, HIGH);
      delay(500);
    }
    if (ValorLido > 682){// se maior que 682, mostrar que esta muito claro
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.print(ValorLido);
      lcd.setCursor(0,1);
      lcd.print("muito claro");
      digitalWrite(Buzzer, HIGH);
      delay(500);
    }
   }
    //Serial.println(results.value, HEX);
    irrecv.resume(); // Receba o próximo valor
     }
     else{
      digitalWrite(Buzzer, LOW);
  }
}
```