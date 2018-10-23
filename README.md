# semaforo
/*
 Programa para un cruce de semaforos con 4 para trafico y 3 para peatones
*/
// Declaramos el pin de los pulsadores de los peatones
  bool A = 0;
  bool B = 0;

//Declaramos el pin de los semaforos que duran 3 min de trafico
const int verde3 = 2;
const int amarillo3 = 3;
const int rojo3 = 4;
//Declaramos el pin de los semaforos que duran 2 min de trafico
const int verde2 = 5;
const int amarillo2 = 6;
const int rojo2 = 7;
//Declaramos el pin de los semaforos  de peatones
const int peatonver = 9;
const int peatonroj = 8;
const int peatonBver =10;
const int peatonBroj = 11;

//Declaramos los retardos
const int menor = 1800;   //RETARDO LED AMARILLO
const int mayor = 200;   //RETARDO LED ROJO Y VERDE
const int parpadeo = 360; //RETARDO PARPADEO VERDE
//Delaramos el almacen de estado de la variable y resultado

 


void setup() {
 // Con un ciclo activamos los pines del 2 al 12 como salidas
 for (int pin = 2; pin < 12; pin++) { 
  pinMode(pin, OUTPUT);
  pinMode(12,INPUT_PULLUP);
  pinMode(13,INPUT_PULLUP);
  
  Serial.begin(9600);
  
 pinMode(12,LOW);
 pinMode(13,LOW);
  
  
   A = digitalRead(12);  //Lee el estado del botÛn y lo almacena
   B = digitalRead(13);  //Lee el estado del botÛn y lo almacena


 
 }
 
}

void loop(){
inicio:
/*for (int pin = 2;pin <=13;pin++){
  digitalWrite(pin,LOW);
}*/
  
  Serial.print("valorA:  ");
  Serial.print(A);
  Serial.print("/t");
  Serial.print("valorB:  ");
  Serial.println(B);
  delay(2);


 
 
 //while (A == 0 && B == 0);{

Serial.println("peaton pulse");
  for (int i = 0; i < 90;i++){
  
   A = digitalRead(12);
   B = digitalRead(13);
   
    if (A == 1 || B == 1){
      delay(mayor);
       
      goto roj;
      
    }
  
  
 
  //PRIMER ESTADO SEMAFORO 3 min EN VERDE
  digitalWrite(verde3,1);    //PARPADEAR VERDE3
  digitalWrite(amarillo3,0);
  digitalWrite(rojo3,0);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,0);
  digitalWrite(rojo2,1);
  //SEMAFORO 5 min
  digitalWrite(peatonver,0);
  digitalWrite(peatonroj,1);
  digitalWrite(peatonBroj,0);
  digitalWrite(peatonBver,1);
  delay(mayor);
  }

  //PARPADEAR VERDE SEMAFORO 3 min
  for (int i = 0;i < 4;i++){
  digitalWrite(verde3,1);
  delay(parpadeo);
  digitalWrite(verde3,0);
  delay(parpadeo);
  }
  
  //SEGUNDO ESTADO SEMAFORO 3 min EN AMARILLO
  digitalWrite(verde3,0);
  digitalWrite(amarillo3,1); //CUANDO AMARILLO ESTE EN HIGH EL DELAY SERA MENOR 
  digitalWrite(rojo3,0);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,0);
  digitalWrite(rojo2,1);
  //SEMAFORO 5 min
  digitalWrite(peatonver,0);
  digitalWrite(peatonroj,1);
  digitalWrite(peatonBroj,1);
  digitalWrite(peatonBver,0);
 
  delay(menor);
  
Serial.println("peaton2 pulse");

   for (int i = 0; i < 60;i++){
  
  A = digitalRead(12);  //Lee el estado del botÛn y lo almacena
  B = digitalRead(13);  //Lee el estado del botÛn y lo almacena 
    
    if (A == 1 || B == 1){
      
      delay(mayor);
      goto roj;
      
    }
    

  //TERCER ESTADO SEMAFORO 3 min EN ROJO
  digitalWrite(verde3,0);
  digitalWrite(amarillo3,0);
  digitalWrite(rojo3,1);
  //SEMAFORO 2 min
  digitalWrite(verde2,1);
  digitalWrite(amarillo2,0);
  digitalWrite(rojo2,0);
  //SEMAFORO 5 min

  digitalWrite(peatonver,1);
  digitalWrite(peatonroj,0);
  digitalWrite(peatonBroj,1);
  digitalWrite(peatonBver,0);
  
  delay(mayor);
   }
   
  //PARPADEAR VERDE SEMAFORO 2 min
 
 for (int i = 0;i < 4;i++){
  digitalWrite(verde2,1);
  delay(parpadeo);
  digitalWrite(verde2,0);
  delay(parpadeo);
  }

  
  //SEMAFORO 3 min EN AMARILLO
  digitalWrite(verde3,0);
  digitalWrite(amarillo3,0);  
  digitalWrite(rojo3,1);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,1);
  digitalWrite(rojo2,0);
  //SEMAFORO 5 min
  digitalWrite(peatonver,0);
  digitalWrite(peatonroj,1);
  digitalWrite(peatonBroj,1);
  digitalWrite(peatonBver,0);
  
  delay(menor);
  goto inicio;

 //}
 
roj: 

delay(1000);

  

  Serial.print("valorA:  ");
  Serial.print(A);
  Serial.print("/t");
  Serial.print("valorB:  ");
  Serial.println(B);
  delay(2);
   
 if (A == B){
 
 

   
   digitalWrite(verde3,0);
  digitalWrite(amarillo3,1);  
  digitalWrite(rojo3,0);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,1);
  digitalWrite(rojo2,0);
  //SEMAFORO 5 min
  digitalWrite(peatonver,0);
  digitalWrite(peatonroj,1);
  digitalWrite(peatonBroj,1);
  digitalWrite(peatonBver,0);
  delay(menor);


  digitalWrite(verde3,0);
  digitalWrite(amarillo3,0);  
  digitalWrite(rojo3,1);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,0);
  digitalWrite(rojo2,1);
  //SEMAFORO 5 min
  digitalWrite(peatonver,1);
  digitalWrite(peatonroj,0);
  digitalWrite(peatonBroj,0);
  digitalWrite(peatonBver,1);
  delay(mayor*80);
   
 }

    
 
 
else   //paso de peatones 2 m

  {
   delay(3000);
   digitalWrite(verde3,0);
  digitalWrite(amarillo3,1);  
  digitalWrite(rojo3,0);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,1);
  digitalWrite(rojo2,0);
  //SEMAFORO 5 min
  digitalWrite(peatonver,0);
  digitalWrite(peatonroj,1);
  digitalWrite(peatonBroj,1);
  digitalWrite(peatonBver,0);
  delay(menor);


  digitalWrite(verde3,0);
  digitalWrite(amarillo3,0);  
  digitalWrite(rojo3,1);
  //SEMAFORO 2 min
  digitalWrite(verde2,0);
  digitalWrite(amarillo2,0);
  digitalWrite(rojo2,1);
  //SEMAFORO 5 min
  digitalWrite(peatonver,1);
  digitalWrite(peatonroj,0);
  digitalWrite(peatonBroj,0);
  digitalWrite(peatonBver,1);
  delay(mayor*40);
   
 
}
 
}
