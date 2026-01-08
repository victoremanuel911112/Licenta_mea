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
  - Python
  - Raspberry PI
  - GPIO/I2C/SPI
  - Senzori de mediu
  - Programare orientata pe module

4. Structura proiectului
  - Sectiunea Import-uri si configurare - Importa toate bibliotecile necesare si are functia de a detecta platforma de rulare
  - Sectiunea Functii utilitare hardware - Functii pentru citirea si conversia datelor de la senzori
  - Sectiunea Range-uri Optimale - Defineste intervalele optime pentru fiecare parametru de mediu
  - Sectiunea Baze de date - Gestioneaza persistenta datelor in SQLite
  - Sectiunea Signal handler - Gestioneaza inchiderea curata a aplicatiei
  - Clasa ImprovedFanWidget - Widget grafic pentru afisarea ventilatoarelor animate in interfata
  - Clasa LEDMananger -Controleaza cele 8-led-uri fizici conectati la GPIO
  - Clasa SensorManager - Nucleul aplicatiei, acesta gestioneaza toate citirile senzorilor si monitorizarea continua
  - Clasa LoginWindow - Ecranul de autentificare si creare conturi
  - Clasa MainApplication - interfata principala, pagina principala care include dashboardul si ofera optiunea de a intra si pe celelalte pagini pentru a vota sau a vedea grafice sau a vedea istoric comentarii sau istoric voturi
  - Clasa ChartsWindow - Interfata pentru analiza grafica avansata a datelor istorice
  - Clasa Voting Window - Interfata de votare pentru modificarea parametrilor de mediu
  - Sectiunea Executie Principala - Punctul de intra in aplicatie si gestionarea fluxului principal

