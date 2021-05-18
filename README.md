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
    tft.fillScreen(WHITE);  // Fundo do Display
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
*   tft.setTextColor         Define a cor da fonte   
*  tft.setTextSize()         Define o tamnho da fonte a ser exibida no display
*  tft.setCursor(X,Y)        Define o posicionamento do display no plano XY
*  tft.println(" ")          Escreve uma palavra no display 


## Mudando a tela de fundo 

Para fazermos essa mudança, basta executar a função   **tft.fillScreen( Cor )**

<a href="https://imgur.com/mdVP9Ut"><img src="https://i.imgur.com/mdVP9Ut.jpg?1" title="source: imgur.com" /></a>


