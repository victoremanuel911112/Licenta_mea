Acest proiect reprezinta lucrarea mea de licenta ce a dezvoltat un sistem de monitorizare si control automat al parametrilor dintr-un spatiu de birouri, bazat pe feedbackul utilizatorilor. Acest proiect a fost strans legat de o infrastructura hardware care includea Raspberry Pi ce avea conectat la el acesti senzori:temperatura, umiditate, lumina, calitate al aerului. Partea hardware nu mai este, a ramas partea de soft. Dar chiar si asa voi explica pe scurt in ce a constat tot proiectul.

1. Obiectivele proiectului
- Monitorizarea parametrilor de mediu într-un spațiu de birou
- Implementarea unui sistem de achiziție de date în timp real
- Aplicarea conceptelor de **automatizare și control cu feedback**
- Integrarea hardware–software într-un sistem funcțional

2. Arhitectura Sistemului
- Unitatea de procesare: Raspberry Pi
- **Senzori utilizați:**
  - Temperatură și umiditate
  - Intensitatea luminii
  - Calitatea aerului
  - Nivel de zgomot

 Am gandit acest soft pentru Raspberry PI pentru ca functia de monitorizare sa arate parametrii inregistrati de senzori in real-time iar functia de feedback sa fie prin votul utilizatorilor. Fiecare parametru are un total de 5 voturi, fiecare vot poate sa fie intre un interval de -3 -> 3. La fiecare 5 voturi se face o medie aritmetica intre valori iar cand se atinge acest prag de voturi, se indica in ce directie trebuie sa se indrepte parametrul, mai scazut sau mai crescut. Aceasta directie arata preferinta participantilor din spatiul de birouri. Sa luam ca exemplu temperatura -3 inseamna ca e foarte frig, drept urmare daca media ar iesi -3 sau -2 trebuie ca incaperea sa fie incalzita, daca iesea 0.5 sau 1 inseamna ca spatiul trebuie racit incat indica ca e mai cald decat dorit. In momentul in care stiam preferinta utilizatorilor, faceam in asa fel incat senzorul sa inregistreze o valoare mai mare sau mai mica(nu se actiona automat din soft/cod) astfel incat sa indeplineasca dorinta utilizatorilor. Acest lucru il realizam prin a exercita un fenomen fizic asupra senzorului (de exemplu suflam spre el ca sa se incalzeasca). In acest proiect am avut si leduri rosii sau albastre, culoarea albastra ramanea aprinsa pana se realiza racirea iar cea rosie ramane aprinsa pana se realiza incalzire. Toata aceasta logica prezentata este valabila si pentru ceilalti parametrii.

3. Tehnologii utilizate
  -Python
  -Raspberry PI
  -GPIO/I2C/SPI
  -Senzori de mediu
  -Programare orientata pe module
4. Structura Proiectului
  ┌─────────────────────────────────────────────────┐
│         HARDWARE RASPBERRY PI                    │
├─────────────────────────────────────────────────┤
│ DHT22 (GPIO26)  →  Temp + Umiditate            │
│ ADS1115 (I2C)   →  Lumină + Calitate Aer       │
│ 8x LED (GPIO)   ←  Feedback vizual              │
└──────────────┬──────────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────────┐
│         LAYER HARDWARE (Python)                  │
├─────────────────────────────────────────────────┤
│ SensorManager  →  Citește senzori (2-3 sec)    │
│ LEDManager     →  Controlează LED-uri           │
└──────────────┬──────────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────────┐
│         LAYER BUSINESS LOGIC                     │
├─────────────────────────────────────────────────┤
│ Monitorizare continuă (±3 lux pentru lumină)   │
│ Logica voturilor (media → schimbare)           │
│ Verificare stabilitate (3 confirmări)          │
└──────────────┬──────────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────────┐
│         LAYER PERSISTENȚĂ                        │
├─────────────────────────────────────────────────┤
│ SQLite: feedback_birou.db                       │
│  - users (autentificare)                        │
│  - votes (istoricul voturilor)                  │
│  - sensor_data (date senzori)                   │
│  - feedback (comenzi sistem)                    │
└──────────────┬──────────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────────┐
│         LAYER PREZENTARE (Tkinter)              │
├─────────────────────────────────────────────────┤
│ LoginWindow      →  Autentificare               │
│ MainApplication  →  Dashboard principal          │
│ VotingWindow     →  Interfață votare            │
│ ChartsWindow     →  Grafice interactive         │
└─────────────────────────────────────────────────┘
