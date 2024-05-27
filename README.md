# Practica-1
## Codi Complet
 ```cpp
  #include <Arduino.h>

  // put function declarations here:
  #define LED_BUILTIN 23
  #define DELAY 100

  const int pinAnalogo = 35;

  void setup() {
    // put your setup code here, to run once:
    pinMode(LED_BUILTIN, OUTPUT);
    Serial.begin(115200);
    //delay(DELAY);
    Serial.println("HOLA MUNDO");
    
  }

  void loop() {
    // put your main code here, to run repeatedly:
    Serial.println("ledhigh");
    digitalWrite(LED_BUILTIN, HIGH);
    //delay(DELAY);
    Serial.println("ledlow");
    digitalWrite(LED_BUILTIN, LOW);
    delay(DELAY);

    int valor = analogRead(pinAnalogo);
  
    // Mostramos el valor leído en el monitor serie
    Serial.print("Valor leído: ");
    Serial.println(valor);
    delay(DELAY);
    }
```
### Funcionament per parts del codi
__1. Inclusió de Biblioteques__
```cpp
#include <Arduino.h>
```
- Arduino.h: Inclou la llibreria bàsica d'Arduino

__2. Definicions__
```cpp
// put function declarations here:
  #define LED_BUILTIN 23
  #define DELAY 100

  const int pinAnalogo = 35;
```
- #define LED_BUILTIN 23: Defineix una macro per al pin del LED integrat, que és el pin 23.
- #define DELAY 100: Defineix una macro per un temps de retard de 100 mil·lisegons.
- const int pinAnalogo = 35: Declara una constant enter per al pin analògic, pin 35.
  
__3. Setup__
```cpp
 void setup() {
    // put your setup code here, to run once:
    pinMode(LED_BUILTIN, OUTPUT);
    Serial.begin(115200);
    //delay(DELAY);
    Serial.println("HOLA MUNDO");
    
  }
```
S'estableix la configuració inicial del programa:
- Serial.begin(115200): Inicialitza la comunicació sèrie en 115200 bauds.
- pinMode(LED_BUILTIN, OUTPUT): Configura el pin LED_BUILTIN com a sortida.
- Serial.println: Imprimeix per pantalla que el dispositiu es disponible per linkar amb Serial.println("HOLA MUNDO"): Imprimeix "HOLA MUNDO" al Monitor Serial.
- 
__4. Loop__
```cpp
  void loop() {
    // put your main code here, to run repeatedly:
    Serial.println("ledhigh");
    digitalWrite(LED_BUILTIN, HIGH);
    //delay(DELAY);
    Serial.println("ledlow");
    digitalWrite(LED_BUILTIN, LOW);
    delay(DELAY);

    int valor = analogRead(pinAnalogo);
  
    // Mostramos el valor leído en el monitor serie
    Serial.print("Valor leído: ");
    Serial.println(valor);
    delay(DELAY);
    }
```
- Serial.println("ledhigh"): Imprimeix "ledhigh" al Monitor Serial.
- digitalWrite(LED_BUILTIN, HIGH): Encén el LED. 
- Serial.println("ledlow"): Imprimeix "ledlow" al Monitor Serial.
- digitalWrite(LED_BUILTIN, LOW): Apaga el LED.
- delay(DELAY): Retarda el programa durant 100 mil·lisegons.
- int valor = analogRead(pinAnalogo): Llegeix el valor analògic del pin 35.
- Serial.print("Valor leído: "): Imprimeix "Valor leído: " al Monitor Serial.
- Serial.println(valor): Imprimeix el valor analògic llegit del pin 35 al Monitor Serial.
  

Aquest codi d'Arduino llegeix valors analògics d'un sensor i controla un LED mentre imprimeix missatges al Monitor Serial.

### Diagrama de Flux
```
Inici
  |
  v
Setup:
  - Configurar LED_BUILTIN com SORTIDA
  - Iniciar comunicació Serial a 115200 bauds
  - Imprimir "HOLA MUNDO"
  |
  v
Loop:
  - Imprimir "ledhigh"
  - Configurar LED_BUILTIN HIGH (LED ON)
  - Imprimir "ledlow"
  - Configurar LED_BUILTIN LOW (LED OFF)
  - Retard de 100 ms
  - Llegir valor analògic del pinAnalogo
  - Imprimir "Valor leído: " i el valor
  - Retard de 100 ms
  |
  v
Repetir Loop
```
### Diagrama de Temps

|Temps (ms) | 0    | 100  | 200  | 300  | 400  | 500  | 600  |
|-----------|------|------|------|------|------|------|------|
|LED        | HIGH | LOW  | HIGH | LOW  | HIGH | LOW  | HIGH |
|Missatge S |ledhigh|ledlow|Valor Llegit|ledhigh|ledlow|Valor Llegit|
|Retard     |------|100ms |------|100ms |------|100ms |------|

### Efectes del delay vist en l'oscil·loscopi

Amb un delay de 500 ms (0,5 segons) podem veure que per cada canvi el senyal és quadrat i periòdic. 

![delay500](https://github.com/AlexMun0z/Practica-1/assets/167424480/75739463-1c96-4533-9dc9-d4947cadce11)


Aquí hem modificat el delay fent-ho un comentant la línea delay, per aconseguir un delay de 0ms.
Tot i així, segueix haventtemps d'espera entre els dos canvis, encara que aquest correspon al temps que es tarden en executar les ordres del codi mateix.
Per tant, el loop triga molt més que les ordes de canvi de voltatges, per tant el LED es queda majoritàriament apagat.El canvi puntual que té el LED de l'estat apagat a encés es poc exacte i la senyal varia massa. 

![delay0mesmenys](https://github.com/AlexMun0z/Practica-1/assets/167424480/d4859f33-a97b-4179-b213-aa6a5e311ed2)



En aquest cas, s'ha canviat l'ordre d'encesa i apagat del LED mantenint el codi com en l'imatge anterior. La diferència ara respecte l'anterior és el LED majoritàriament es queda encés.

![delay0menysmes](https://github.com/AlexMun0z/Practica-1/assets/167424480/ca4d9dd9-3f87-436e-af51-892983263a47)


