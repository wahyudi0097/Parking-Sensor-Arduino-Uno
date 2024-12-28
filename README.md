KETERANGAN
Sensor ultraisonik HC-SR04 adalah perangkat yang menggunakan gelombang ultrasonik untuk mengukur jarak antara sensor dan objek. Sensor ultrasonik HCSR04 digunakan untuk sistem pengukuran jarak aman.

ALAT DAN BAHAN
Arduino Uno= 1 Buah, Sensor  ultraisonik HC-SR04 = 1 Buah, Buzzer = 1 Buah, Kabel Jumper= 6 Buah, Breadboard = 1 buah, kabel USB = 1 buah, dan Laptop=1 Buah.

Kode Program 
/**************************************************************
 *  PARKING SENSOR WITH HC-SR04                               *
 *                                                            *
  *  This code receives data from the HC-SR04 proximity        *
 *  sensor, analyses  them, sends them to the serial monitor   *
 *  and produces intermittent sounds  to warn of an obstacle.  *
 **************************************************************/

//  Definition of trigger, echo, beep pins and other constants
#define trigger      2
#define  echo         3
#define beep        11
#define beep_start 100
#define min_distance  5

// Definition of sound speed (centimetres / microsecond)
#define c 0.0343

//  Definition of the variables
long tempo;
float space;

void setup() {
  // Definition of input and output
  pinMode(trigger, OUTPUT);
  pinMode(echo,  INPUT);
  pinMode(beep, OUTPUT);

  // Serial communication initialisation  (optional)
  Serial.begin(9600);
}

void loop() {
  // Before measurement,  the trigger is set to low level
  digitalWrite(trigger, LOW);
  delayMicroseconds(5);

  // Send one pulse (trigger goes high level for 10 microseconds)
  digitalWrite(trigger,  HIGH);
  delayMicroseconds(10);
  digitalWrite(trigger, LOW);

  //  Reading echo, via pulseIn, which returns the duration of the impuse (in microseconds)
  // The acquired data is then divided by 2 (forward and backward)
  tempo =  pulseIn(echo, HIGH) / 2;
  // Computation of distance in centimetres
  space  = tempo * c;

  // space is displayed in the serial monitor ([Ctrl] + [Shift]  + M)
  // approximated to the first decimal place
  Serial.println("Distanza  = " + String(space, 1) + " cm");

  // If the distance is less than one  metre
  if (space < beep_start) { 
    // Emits sounds at intervals proportional  to distance (1 m = 400 ms)
    tone(beep, 1000); 
    delay(40);
    //  Below min_distance cm it emits a continuous sound
    if (space > min_distance)  {
      noTone(beep); 
      delay(space * 4);
    }
  } 
  // Waits  50 milliseconds before another measurement
  delay(50);
}


KESIMPULAN
Sistem ini sangat efektif dalam membantu mencegah tabrakan kendaraan saat parkir, terutama di area sempit. Dengan memanfaatkan Arduino Uno sebagai pengendali utama, proyek ini memberikan solusi yang sederhana, ekonomis, dan mudah untuk diterapkan. Selain itu, proyek ini juga menjadi media pembelajaran yang baik untuk memahami integrasi antara perangkat keras dan perangkat lunak dalam teknologi berbasis mikrokontroler.
