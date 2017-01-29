# HOME-SENSORS
home sensors radar/motion sensor/leds/smoke detector/camera
Κωδικας για τον προγραμματισμο 
#define trigPin 7//radar input
#define echoPin 8//radar output
#define led 30 //ekso diadromou
#define led2 28//endiameso led
#define led3 26//endiameso  led 
#define led4 24//portas
#define ledsos 32 //led ektaktou anagkhs
#define ledsos2 34 //led ektaktou anagkhs
#define ledroof 36 //led ektaktou anagkhs

const int sensorPin= A4;
const int buzzer = 13; //ηχειακι
int smoke_level;// δηλωση ακερεου για ποσοτητα αεριων
int sound = 100;// ηχος που θα παραχθει από το ηχειιο

int ledPin = 36;                // choose the pin for the LED
int inputPin = 2;               //διαλεγουμε την μεθοδο εισαγωγης για τον εσθητηρα pir 
int pirState = LOW;             // αρχιζουμε υποθετοντας ότι δεν υπαρχει καμια κινηση
int val = 0;                    // μεταυλητη για την αναγνωρηση της καταστασης


//σημειοδηλωσης ολων των μεταβλητων και εσθητηρων
void setup(){
//gia to apostasiometro
Serial.begin (9600);
 pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(led, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);
  pinMode(buzzer, OUTPUT);
//δηλωθηκαν ως πηγες εξοδου τα ανωθεν led
//pir
  pinMode(ledPin, OUTPUT);      // δηλωθηκε ως πηγη εξοδου led  pinMode(inputPin, INPUT);     // δηλωθηκε ως πηγη εισοδου
  pinMode(ledroof,OUTPUT);//τα led της οροφης δηλωνονται για εξοδο
    pinMode(buzzer, OUTPUT);//ομοιος και το ηχειο
  Serial.begin(9600);


//kapnou
Serial.begin(9600); //sets the baud rate for data transfer in bits/second
pinMode(sensorPin, INPUT);//the smoke sensor will be an input to the arduino
pinMode(ledsos , OUTPUT); //δηλωθηκε ως πηγη εξοδου
pinMode(ledsos2 , OUTPUT);// δηλωθηκε ως πηγη εξοδου
pinMode(buzzer, OUTPUT);// δηλωθηκε ως πηγη εξοδου και θα παραγει ηχο
}

//εναρξη της επαναλαμβανομενης εκτελεσης του προγραμματος
void loop(){

//kapnou
smoke_level= analogRead(sensorPin); //το arduino διαβαζει την τιμη από τον εσθητηρα καπνου
Serial.println(smoke_level);//τυπωνει στην οθονη τα απότελεσματα της μετρησης του καπνου αναλογα με το τι αντιλαμβανετε ο εσθητηρας

smoke_level= analogRead(sensorPin); //το arduino διαβαζει τις τιμες από τον εσθητηρα καπνου
Serial.println(smoke_level);// τυπωνει στην οθονη τα απότελεσματα της μετρησης του καπνου αναλογα με το τι αντιλαμβανετε ο εσθητηρας
if(smoke_level > 350){ //οριζει ότι αν τα πιπεδα του καπνου είναι περισοτερα από αυτά που ορισαμε το ηχειο θα αρχισει να παιζει
tone(buzzer, 1000); // εκπεμπει σημα 1ος χερτζ
digitalWrite(ledsos, HIGH);// high οριζουμε την κατασταση λειτουργειας ενός εσθητηρα-led-buzzer
digitalWrite(ledsos2, LOW); );// low οριζουμε την κατασταση αδρανειας ενός εσθητηρα-led-buzzer
 delay(250);// καθηστερουμε στο προγραμμα καπιο χρονικο διαστιμα (0,2 sec) ετσι ώστε να μπορεσει να αναγνωρισει τις εντολες
  tone(buzzer, 3500); 
digitalWrite(ledsos,LOW );
digitalWrite(ledsos2, HIGH);   
delay(250);
  tone(buzzer, 2000); // Send 1KHz sound signal...
digitalWrite(ledsos, HIGH);
digitalWrite(ledsos2, LOW); 
  delay(250); 
  tone(buzzer, 3500); // Send 1KHz sound signal...
digitalWrite(ledsos,LOW );
digitalWrite(ledsos2, HIGH); 
 delay(250);     
}
else{//εναλακτικα αμα τα επιπεδα δεν ξεπερασουν το οριο που θετουμε δεν λειτουργει κατι από αυτα
noTone(buzzer);     // Stop sound...
digitalWrite(ledsos, LOW);
digitalWrite(ledsos2, LOW); 
  delay(1000); 
}






//apostashs diadromou
  long duration, distance;
  digitalWrite(trigPin, LOW); //αν η αποσταση είναι μεγαλη τοτε δεν εχουμε καμια αντιδραση από το προγραμμα
  delayMicroseconds(2);// καθηστερηση αναγνωρισης της εντολης
  digitalWrite(trigPin, HIGH);//ψυφιακη καταγραφη στην οθονη
  delayMicroseconds(10);//καθηστερηση στην αποτυπωση του καταγραφικου στην οθονη κάθε 10 sec
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);//οριζετε η διαρκια ως ανηχτη(να αναγνωριζει ποση ωρα εμεινε το αντικειμενο στην «εισοδο»)
  distance = (duration/2) / 29.1; //οριζουμε την αποοσταση στο 29,1 cm

 //δημιουργεια εναλακτικων για την αναγνωριση των αντικειμενων από 25cm και κατω
  if (distance <= 25) {//αν θα αναγνωρισει ένα αντικειμενο σε αποσταση από 1-25 εκ. θα αναψει με μικρη καθηστερηση όλα τα λεντ του διαδρομου διαδοχικα ανα 2
     digitalWrite(led, HIGH);
      delay(500);
    digitalWrite(led2, HIGH);
 delay(500);
    digitalWrite(led3, HIGH);
     delay(500);
    digitalWrite(led4, HIGH);
   delay(500);
}
//αλλιος αν δεν αναγνωρισει κατι από 25 και κατω θα παραμηηνουν όλα σβηστα
  else{
    digitalWrite(led,LOW);
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
  }

   if (distance > 20 || distance <= 0){
    Serial.println("Out of range");
    noTone(buzzer);
  }
  else {
    Serial.print(distance);
    Serial.println(" cm");// εικονικη καταγραφη στην οθονη μας και διπλα τοποθετηση του ορου cm  για να αναγνωριζει και ο 3ος χρηστης την πραγματικη αποσταση του αντικημενου
   
  }
//πιρ
  delay(500);
///αναγνωριζει αν υπαρχει καπια κινηση η διαφορα στο δωματιο από την φυσικη κατασταση που εχει απομνημονευσει και αν βρει κινηση αναβει τα φωτα
  val = digitalRead(inputPin);  // read input value
  if (val == HIGH) {            // check if the input is HIGH
    digitalWrite(ledPin, HIGH);  // turn LED ON
       delay(1050);

if (pirState == LOW) {
      // we have just turned on
      Serial.println("Motion detected!");// εκτυπωνει με το που ανηχνευσει κινηση τη φραση  motion detected και ενεργοποιει όλα τα φωτα 
      // We only want to print on the output change, not state
      pirState = HIGH;
    }
} else {
      digitalWrite(ledPin, LOW); // turn LED OFF
      delay(300);    
      if (pirState == HIGH){
      // we have just turned off
      Serial.println("Motion ended!");// εκτυπωνει ότι οπια κινηση γεινοταν τελειωσε και σβηνει τα φωτα
      // We only want to print on the output change, not state
      pirState = LOW;
     }
   }
 }
