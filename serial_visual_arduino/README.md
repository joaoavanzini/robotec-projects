# Visual Studio 2015 vs Arduino IDE

Arduino IDE, uma solução muito boa para apenas linhas de comandos, sem parte visual. No tutorial de hoje, iremos aprender a como montar partes visuais para a sua comunicação serial entre computador e Arduíno. 

Primeiramente, execute este código em seu Arduíno; ele não é necessário, porem, com ele podemos testar a comunicação serial. Seu funcionamento é simples, necessariamente utilize o “L” (minusculo) para ligar o led e o “D” (minusculo) para desligar o led.

# Vídeo:

[Vídeo](https://youtu.be/dpum4BGyhLY)

```
int led = 13;
 
void setup(){
  Serial.begin(9600);
  pinMode(led, OUTPUT);
}
 
void loop(){
   char ler = Serial.read();
 
 
   if (ler =='l')
   {
    digitalWrite(led, HIGH);
    Serial.println("led ligado");
   }
   else if (ler == 'd')
   {
    digitalWrite(led,LOW);
    Serial.println("led deligado");
   }
}
```

Após tudo funcional, abra o seu Visual Studio 2015 e coloque este código em seu compilador: (Não esqueça de fazer a parte visual, caso precise, o link do tutorial detalhado é este: [tutorial](https://youtu.be/dpum4BGyhLY))

```
Public Class Form1
 
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
 
        If SerialArduino.IsOpen() Then
            SerialArduino.Close()
        Else
            SerialArduino.Open()
            SerialArduino.Write("d")
        End If
 
    End Sub
 
    Private Sub btnLigar_Click(sender As Object, e As EventArgs) Handles btnLigar.Click
        SerialArduino.Write("l")
    End Sub
 
    Private Sub btnDesligar_Click(sender As Object, e As EventArgs) Handles btnDesligar.Click
        SerialArduino.Write("d")
    End Sub
 
    Private Sub Form1_FormClosed(sender As Object, e As FormClosedEventArgs) Handles Me.FormClosed
        If SerialArduino.IsOpen() Then
            SerialArduino.Close()
        End If
    End Sub
End Class
```

(coloque o nome dos botões em : btnDesligar e btnLigar)
(coloque o nome do SerialPort para : SerialArduino)
Após tudo funcional, o seu programa poderá ficar desse jeito:

![Exemplo](https://github.com/vicpb/robotec-projects/blob/master/serial_visual_arduino/Windows-Form-Aplication.png)