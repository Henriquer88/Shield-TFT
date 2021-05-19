# Shield-TFT-
Primeiros passos com o Shield TFT
 
# Objetivo
 Apresentar as funções básicas do Display tft 2.4 touch , todo o desenvolvimento dos exemplos foi feito no Mbed.
 
 # Materiais 
* Nucleo F103
* Compilador MBED https://os.mbed.com/
* Display 2.4 Touch

# Display TFT 2.4
 
 Esse display tft de 2,4¨ tem resolução de 320×240 pixels, com um esquema de cores de 18 bits que permite a exibição de até 262.000 tonalidades diferentes, tela touch resistiva e   um slot para cartão microSD, tudo isso controlado pelo driver ILI9325 além de possuir comunicação paralela.
  Datasheet do  controlador do Display  https://cdn-shop.adafruit.com/datasheets/ILI9325.pdf
 
 
 <a href="https://imgur.com/NtV6pqn"><img src="https://i.imgur.com/NtV6pqn.png" title="source: imgur.com" /></a>
 
 * Pinagem

<a href="https://imgur.com/HqB6b2H"><img src="https://i.imgur.com/HqB6b2H.png" title="source: imgur.com" /></a>

# Programas e bibliotecas 

Para utilizar o Display TFT Touch precisaremos das três bibliotecas abaixo:

* ADA_GFX_kbv
* MCUFRIEND
* TFT_TOUCHSHIELD

# Progarmas 

##  Escrevendo no Display


```javascript
//************************ Biblioteca *****************************************//
#include "mbed.h"
#include "Arduino.h"
#include <MCUFRIEND_kbv.h>
MCUFRIEND_kbv tft;

//****************************************************************************//

//***********************Orientação  Display**********************************//


uint8_t Orientation = 1;  

//****************************************************************************//



//***********************Tabela de Cores**************************************//
#define BLACK   0x0000
#define BLUE    0x001F
#define RED     0xF800
#define GREEN   0x07E0
#define CYAN    0x07FF
#define MAGENTA 0xF81F
#define YELLOW  0xFFE0
#define WHITE   0xFFFF

//****************************************************************************//

//***********************Escrita no  Display**********************************//
void write ()
{
    tft.setTextColor(BLUE);
    tft.setTextSize(3);     // Tamanho do Texto no Display
    tft.setCursor(60, 30); //  Orientação do texto X,Y
    tft.println("DISPLAY TFT");


}

//****************************************************************************//



void setup(void)
{

    tft.reset();
    tft.begin();
    tft.setRotation(Orientation);
    tft.fillScreen(BLACK);  // Fundo do Display
    write();
    delay(1000);
}

void loop()
{

}


```
Compilando esse código no MBED, teremos o resultado abaixo :

<a href="https://imgur.com/QpR13FC"><img src="https://i.imgur.com/QpR13FC.jpg" title="source: imgur.com" /></a>

  Para fazermos a escrita no display, devemos utilizar as seguintes funções :
*  tft.setTextColor          Define a cor da fonte   
*  tft.setTextSize()         Define o tamnho da fonte a ser exibida no display
*  tft.setCursor(X,Y)        Define o posicionamento da palavra no plano XY
*  tft.println(" ")          Escreve uma palavra no display 


Se quisermos mudar a cor da tela de fundo , devemos utilizar a função  **tft.fillScreen( WHITE )**

<a href="https://imgur.com/mdVP9Ut"><img src="https://i.imgur.com/mdVP9Ut.jpg?1" title="source: imgur.com" /></a>


## Criando formas geométricas no display.
 Utlizando a biblioteca a ADA_GFX_kbv conseguimos criar diversas formas, tais como retângulos, circluos, triângulos etc.
 
 * Criando um Retângulo
```javascript
//************************ Biblioteca *****************************************//
#include "mbed.h"
#include "Arduino.h"
#include <MCUFRIEND_kbv.h>
MCUFRIEND_kbv tft;

//****************************************************************************//

//***********************Orientação  Display**********************************//


uint8_t Orientation = 1;  

//****************************************************************************//



//***********************Tabela de Cores**************************************//
#define BLACK   0x0000
#define BLUE    0x001F
#define RED     0xF800
#define GREEN   0x07E0
#define CYAN    0x07FF
#define MAGENTA 0xF81F
#define YELLOW  0xFFE0
#define WHITE   0xFFFF

//****************************************************************************//

//***********************Escrita no  Display**********************************//
void forma ()
{
    //tft.setCursor(100, 50);
    tft.drawRoundRect(60, 90, 190, 40, 1, WHITE); // (x,y,x1,y1,s)
    //tft.fillRoundRect(60, 90, 190, 40, 1, BLUE);
    //tft.fillCircle(250,190,20,WHITE);
    tft.setTextColor(RED);
    tft.setTextSize(3);
    tft.setCursor(70, 98); // Orientação X,Y
    tft.println("RECTANGLE");


}

//****************************************************************************//



void setup(void)
{

    tft.reset();
    tft.begin();
    tft.setRotation(Orientation);
    tft.fillScreen(BLACK);  // Fundo do Display
    forma();
    delay(1000);
}

void loop()
{

}
```

Compilando esse código no MBED, teremos o resultado abaixo :

<a href="https://imgur.com/yduBaTw"><img src="https://i.imgur.com/yduBaTw.jpg" title="source: imgur.com" /></a>

Para desenharmos um retângulo utilizamos a função  **  tft.drawRoundRect(X,Y,X1,Y1,S COR)**
*  X   Deslocamento  do retañgulo no plano X
*  Y   Deslocamento  do retângulo no plano Y
*  X1  Tamanho do retângulo em relação ao plano X
*  Y1  Tamanho do retângulo em relação ao plano Y
*  S   Arredondamento das laterais do retângulo


Se quisermos fazer um retângulo com uma determinada cor de fundo, devemos utilizar a função  **tft.fillRoundRect(60, 90, 190, 40, 1, BLUE)**

<a href="https://imgur.com/58mXztE"><img src="https://i.imgur.com/58mXztE.jpg" title="source: imgur.com" /></a>

## Criando  Circulos 
```javascript
// ************** Display TFT-  ILI9341 Circle************** \\


//************************ Biblioteca *****************************************//
#include "mbed.h"
#include "Arduino.h"
#include <MCUFRIEND_kbv.h>
MCUFRIEND_kbv tft;

//****************************************************************************//

//***********************Orientação  Display**********************************//


uint8_t Orientation = 1;  

//****************************************************************************//



//***********************Tabela de Cores**************************************//
#define BLACK   0x0000
#define BLUE    0x001F
#define RED     0xF800
#define GREEN   0x07E0
#define CYAN    0x07FF
#define MAGENTA 0xF81F
#define YELLOW  0xFFE0
#define WHITE   0xFFFF

//****************************************************************************//

//***********************Escrita no  Display**********************************//
void forma ()
{

    //tft.drawCircle(150,110,80,WHITE);
    tft.fillCircle(150,110,80,WHITE);
    tft.setTextColor(RED);
    tft.setTextSize(3);
    tft.setCursor(95, 98); // Orientação X,Y
    tft.println("CIRCLE");


}

//****************************************************************************//



void setup(void)
{

    tft.reset();
    tft.begin();
    tft.setRotation(Orientation);
    tft.fillScreen(BLACK);  // Fundo do Display
    forma();
    delay(1000);
}

void loop()
{

}
```
Para desenharmos um círculo utilizamos a função  **  tft.drawCircle(X,Y,R,COR)**
*  X   Deslocamento  do retañgulo no plano X
*  Y   Deslocamento  do retângulo no plano Y
*  R   Raio da circunfência 

Compilando esse código no MBED, teremos o resultado abaixo :

<a href="https://imgur.com/g0Oxw0P"><img src="https://i.imgur.com/g0Oxw0P.jpg" title="source: imgur.com" /></a>

Se quisermos fazer um retângulo com uma determinada cor de fundo, devemos utilizar a função  ** tft.fillCircle(150,110,80,WHITE)**

<a href="https://imgur.com/XV4qUA1"><img src="https://i.imgur.com/XV4qUA1.jpg?1" title="source: imgur.com" /></a>

 Criando um Triângulo
 ```javascript
 // ************** Display TFT-  ILI9341 Triangle******************************\\


//************************ Biblioteca *****************************************//
#include "mbed.h"
#include "Arduino.h"
#include <MCUFRIEND_kbv.h>
MCUFRIEND_kbv tft;

//****************************************************************************//

//***********************Orientação  Display**********************************//


uint8_t Orientation = 1;  

//****************************************************************************//



//***********************Tabela de Cores**************************************//
#define BLACK   0x0000
#define BLUE    0x001F
#define RED     0xF800
#define GREEN   0x07E0
#define CYAN    0x07FF
#define MAGENTA 0xF81F
#define YELLOW  0xFFE0
#define WHITE   0xFFFF

//****************************************************************************//

//***********************Escrita no  Display**********************************//
void forma ()
{

    tft.drawTriangle(40, 200, 150, 100, 280, 200, WHITE); 
    tft.setTextColor(RED);
    tft.setTextSize(3);
    tft.setCursor(86, 160); // Orientação X,Y
    tft.println("TRIANGLE");


}

//****************************************************************************//



void setup(void)
{

    tft.reset();
    tft.begin();
    tft.setRotation(Orientation);
    tft.fillScreen(BLACK);  // Fundo do Display
    forma();
    delay(1000);
}

void loop()
{

}
  ```
  
  Compilando esse código no MBED, teremos o resultado abaixo :
  
  <a href="https://imgur.com/6QXZmFz"><img src="https://i.imgur.com/6QXZmFz.jpg?1" title="source: imgur.com" /></a>
  
  Para desenharmos um círculo utilizamos a função  **  tft.drawTriangle(A,B,C,A1,B1,C1 ,COR)**
  
 * (A,A1),(B,B1) e (C,C1)  são os vertíces do triângulo

 Se quisermos fazer um triângulo com uma determinada cor de fundo, devemos utilizar a função  ** tft.fillTriangle(40, 200, 150, 100, 280, 200, WHITE)**  
 
 <a href="https://imgur.com/VieGKzo"><img src="https://i.imgur.com/VieGKzo.jpg" title="source: imgur.com" /></a>


# Utilizando o Toutch

Antes de utilizarmos o touch é necessário  sua calibração, isso é importantre para mepear os valores dos pontos na tela do display

<a href="https://imgur.com/RVW7MT3"><img src="https://i.imgur.com/RVW7MT3.png" title="source: imgur.com" /></a>

* Calibrando o Touch

```javascript
// ************** Display TFT-  ILI9341 Toutch********************************\\


//************************ Biblioteca*****************************************//
#include "mbed.h"
#include "Arduino.h"
#include <MCUFRIEND_kbv.h>
MCUFRIEND_kbv tft;
#include "TouchScreen_kbv_mbed.h"

//******************************Configuração do Display***********************//
const PinName XP = D8, YP = A3, XM = A2, YM = D9; 
const int TS_LEFT=121,TS_RT=922,TS_TOP=82,TS_BOT=890;
DigitalInOut YPout(YP);
DigitalInOut XMout(XM);
TouchScreen_kbv ts = TouchScreen_kbv(XP, YP, XM, YM);
TSPoint_kbv tp;

// Valores para detectar a pressão do toque 
#define MINPRESSURE 10
#define MAXPRESSURE 1000

long map(long x, long in_min, long in_max, long out_min, long out_max)
{
    return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
}
//***********************Orientação  Display**********************************//

uint8_t Orientation = 0;

//****************************************************************************//



//***********************Tabela de Cores**************************************//

#define BLACK   0x0000
#define BLUE    0x001F
#define RED     0xF800
#define GREEN   0x07E0
#define CYAN    0x07FF
#define MAGENTA 0xF81F
#define YELLOW  0xFFE0
#define WHITE   0xFFFF

//****************************************************************************//


Serial pc(USBTX, USBRX);


void disp()

{
    
        tft.setTextSize(2);
        tft.setTextColor(MAGENTA,BLACK);
        
    while (1) {
        
        tp = ts.getPoint();
        YPout.output();
        XMout.output(); 
        
        tft.setCursor(0, (tft.height() * 2) / 4);
        tft.printf("tp.x=%d tp.y=%d   ", tp.x, tp.y);

    }
    


}



void setup(void)
{

    tft.reset();
    tft.begin();
    tft.setRotation(Orientation);
    tft.fillScreen(BLACK);
    disp();
}

void loop()
{


}


```

Algumas funçoes importantes para habilitar o touch

* TouchScreen_kbv         -  Biblioteca responsável por conter as funçoes do touch 
* ts.getPoint()           -  Função para captura dos dados do display
* uint8_t Orientation     -  Função responsável pela orientação do display
* tft.printf()            -  Escreve um  valor de uma variável no display


Valores obtidos com  calibração medidos as extremidaddes do display:

* Ponto 1 - 894  94
* Ponto 2 - 891  873
* Ponto 3 - 164  876
* Ponto 4 - 164  89
 
<a href="https://imgur.com/UEgY0eT"><img src="https://i.imgur.com/UEgY0eT.jpg" title="source: imgur.com" /></a>
 
 
 # Criando um botão no display Toutch
 
 




