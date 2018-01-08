Eeldused:
1) Toimiv Arduino, millel juba on bootloader.
2) atmega168 kiip
3) 16MHz kristall
4) Juhtmed ja kaine mõistus
5) USB to ttl converter, soovitavalt 5V ja DTR pinniga Arduino resettimiseks ja sünkroniseerimiseks.
6) 10KΩ takisti
7) 100 nF kondensaator

1. Kopeeri kaasas olevast failist sisu enda installi kaustas oleva boards.txt faili lõppu
/arduino-1.8.6/hardware/arduino/avr/boards.txt

Kui sul Arduino IDE töötas, siis tee sellele restart.

2. Võta töötav arduino board, soovitatavalt UNO

3. Ava examples ArduinoISP

4. Eemalda koodis #define USE_OLD_STYLE_WIRING eest // (uncomment)

5. Lae kood enda valitud töötavale arduinole.

6. Ühenda oma atmega168 kiip Arduinoga
#VCC = 5V
Arduino -- Atmega 168
D10 	-> 1
VCC 	-  10KΩ -> 1 (Pull up resistor to pin 1)
VCC 	-> 7
GND 	-> 8
D11 	-> 17
D12 	-> 18
D13 	-> 19

Võimalusel ühenda pinnidesse 9 ja 10 16MHz oscillatoor, on võimalik võtta ka töötava plaadi kiibilt clock, ühendades kiipide pinnid 9 -> 9 ja 10 -> 10
Ilma kvartsita kirjutamine ebaõnnestub, kui plaat oli eelnevalt seatud töötama 16MHz kristalliga. Kindlam on ühendada kvartsiga.

7. Vali plaadiks "ATmega168 8MHz" ja programmaatoriks "Arduino as ISP"

8. Vajuta burn bootloader

9. Kui kõik läheb hästi, siis teavitab seda IDE ning kui kiibile ühendada PIN 19(D13) külge LED, see ei vilgu.
Led vilgub, kui ühendada kvarts kiibi küljest lahti ja groundida korraks PIN 1(RESET).

10. Et laadida nüüd kiibile koodi on vajalik ühendada see töötava kiibi küljest lahti. Ja ühendada USB TTL kiibiga. Saab ka üle Arduino, kui on v
õimalus Arduino küljest oma atmega kiip lahti võtta.
TTL -- Arduino
TX  -> 2 (RXD)
RX  -> 3 (TXD)
DTR - 100 nF - 1 (RESET)

11. Valida programmatooriks jällegi enda lemmik, näiteks AVR ISP mkII
Ja proovida peale laadida Blink programmi, kui kõik on õigesti tehtud, hakkab Pin 13 külge ühendatud LED vilkuma.

Siit edasi saab juba teha kõike, mida ikka Arduinoga. 
Sellise ostsillaatori kasutamisel tuleb aga meeles pidada, et kasutada ainult baud rate kuni 20000, suurematel kiirustel läheb veaprotsent talumatuks.

Järgnevalt lehelt leiab baud rate ja error rate suhted.
http://www.avrfreaks.net/sites/default/files/AT90USB1287%20Baud%20Rate%20Table%20-%208MHz%20%26%2016MHz.png 
Error rate peabolema < 2%, et edukalt kasutada serial ühendust.
Antud juhend on testitud Arduino IDE 1.8.5-ga
