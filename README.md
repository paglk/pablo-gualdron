int trigPin = 7;  //Definimos los pines con los que trabajaremos
int echoPin = 8;
int LEDR = 10;
int LEDV = 11;
float velocidad = 0.0343;  //velocidad del sonido en cm/us
const int valorUmbral = 50;
long duracion, distancia ;

void setup()
{
    pinMode(trigPin, OUTPUT);  //Declaramos el pin digital 7 como salida
    pinMode(echoPin, INPUT);   //Declaramos el pin digital 8 como entrada
    pinMode(LEDR, OUTPUT);   //Declaramos el pin digital 10 como salida
    pinMode(LEDV, OUTPUT);   //Declaramos el pin digital 11 como salida 
    digitalWrite (LEDR , LOW);  //Definimos la salida digital 10 con un estado bajo
    digitalWrite (LEDV , LOW);  //Definimos la salida digital 11 con un estado bajo
 }
void loop()
  {   
    digitalWrite(trigPin, LOW);        // Nos aseguramos de que el trigger está desactivado
    delayMicroseconds(2);              // Para asegurarnos de que el trigger está LOW
    digitalWrite(trigPin, HIGH);       // Activamos el pulso de salida
    delayMicroseconds(10);             // Esperamos 10µs. El pulso sigue active este tiempo
    digitalWrite(trigPin, LOW);        // Cortamos el pulso y a esperar el ECHO
    duracion = pulseIn(echoPin, HIGH) ; //pulseIn mide el tiempo que pasa entre que el pin declarado (echoPin) cambia de estado bajo a alto (de 0 a 1)
    distancia = velocidad* duracion / 2;   //Dividimos entre 2 porque queremos coger el tiempo de ida (y no ida y vuelta)
                                         // y entre 29,1 porque es 1 dividido entre la velocidad del sonido(1/(vel sonido) en cm/us
    if ( distancia < valorUmbral){
        digitalWrite (LEDR , HIGH);     //Si el sensor detecta una distancia menor a 20 cm enciende el LED Rojo
        digitalWrite (LEDV , LOW);      // y apaga el verde
    }
    else{       // de lo contrario
        digitalWrite (LEDR , LOW);    //apaga el rojo
        digitalWrite (LEDV , HIGH);   //enciende el verde
        }
  }
