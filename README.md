# RAM Dual-Clock Project (Clock Domain Crossing)

Acest proiect implementeaza o memorie RAM accesibila din doua domenii de ceas diferite. Modulul este util in aplicatii hardware unde doua subsisteme care functioneaza la frecvente diferite trebuie sa comunice printr-un spatiu de memorie partajat.

## Continutul proiectului

- `ram_dual_clock.sv` - modulul principal RAM dual-clock
- `synchronizer.sv` - modul folosit pentru sincronizarea semnalelor intre doua domenii de ceas
- `ram_dual_clock_tb.sv` - testbench pentru verificarea functionarii corecte

## Parametri configurabili

- `DATA_WIDTH` - latimea in biti a fiecarui cuvant din memorie (implicit 8)
- `ADDR_WIDTH` - latimea in biti a adreselor (implicit 6, adica 64 de pozitii)

## Descriere functionala

Modulul permite scrierea datelor intr-un domeniu de ceas si citirea lor dintr-un alt domeniu. Pentru a asigura transferul corect al semnalelor intre cele doua domenii, semnalele sunt trecute printr-un sincronizator cu doua registre. Acest mecanism reduce riscul aparitiei fenomenului de metastabilitate.

Scrierea se face la flancul pozitiv al semnalului `clock_write`, iar citirea la flancul pozitiv al semnalului `clock_read`.

Semnalele importante sunt:

- `write_enable`: activeaza scrierea
- `addr_write`: adresa la care se scrie
- `data_write`: datele de scris
- `addr_read`: adresa de la care se citeste
- `data_read`: datele citite

## Testbench

Testbench-ul simuleaza urmatorul scenariu:

1. Se scriu cinci valori in memorie, incepand de la adresa 0
2. Se dezactiveaza scrierea
3. Se asteapta cateva cicluri de ceas
4. Se citesc valorile scrise anterior, din domeniul `clock_read`

Semnalele `clock_write` si `clock_read` sunt generate la frecvente diferite (10 MHz si 20 MHz) pentru a simula un caz real de clock domain crossing.

Valoarea obtinuta pe `data_read` este verificata pentru a confirma ca operatiile de scriere si citire s-au realizat corect.

## Cum se simuleaza

1. Se compileaza fisierele folosind un simulator SystemVerilog (Vivado, ModelSim, etc.)
2. Se ruleaza `ram_dual_clock_tb.sv`
3. Se verifica rezultatele in consola sau folosind un waveform viewer

## Scopul proiectului

Proiectul poate fi folosit ca exemplu de crossing intre doua domenii de ceas si pentru demonstratii in cadrul unui portofoliu sau CV tehnic.
