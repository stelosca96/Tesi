<!-- aggiungere una sezione Tesi in collaborazione con Tiesse spa: -->

<!-- <!-
- Scrivo quello dell'abstractafd
lavoro svolto in collaborazione e in parte in presenza presso l'azienda spa di Ivrea -->

<!-- Sezione in cui parlo di cui fa Tiesse spa
- presento azienda
- location e sedi distaccate
- parlare della collaborazione con il poli => sempre in collaborazione per ricerca e sviluppo in particolare negli ultimi anni con un focus sugli aspetti di sicurezza e analisi dati di rete e non solo hw => prendere spunto anche dal sito
- prendere ispirazione dalla slide tiesse di itasec -->

<!-- TITOLO TESI => Anomaly detection per il rilevamento di attacchi DDoS o trovarne altri -->


<!-- il mio tool => cambiare nome -->


<!-- fare stare esempi di codice in una pagina -->

figura 4.1 => togliere logo


<!-- 

Sistem anti-DDoS: stato dell'arte
Anomaly Detection: stato dell'arte -->



3.7 Motivazione scelte

Perchè autoencoders
Quali sono i vantaggi rispetto ad altre soluzioni:

- parlo del fatto che sfruttiamo le api messe a disposizione di keras e tensorflow perchè sono facili da usare, ci sono soluzioni alternative da citare (tool di twitter scritto in R => informarsi)
- gli autoencoders si prestano bene nel caso in cui non sappiamo a priori definire delle features astratte => ci basiamo solo sulla forma e non sul contenuto => non cerchiamo feature particolari per determinati  pattern https://blog.keras.io/building-autoencoders-in-keras.html
- le forme possono cambiare da cliente a clientee
- facili da usare, si passa velocemente da una fase experimental a prodution grazie al python e alla semplicità

Il nostro tool

<!-- Metologia per collezione dei dati:
- Metodo classico: modulo kernel
- eBPF: trattato successivamente

Mettere immagine netfilter in orizzontale
Per l'impossibilità di introdurre i syn su un router in produzione, ma abbiamo fatto un  -->

Mettere immagine collectd https://collectd.org/images/architecture-schematic.png

<!-- Gestione dati: parlo della raccolta dati, cosa è stato fatto: raccolta features più granulari oltre che il syn rate, come è stato fatto netfilter/modulo kernel(soluzione classica) e rimando alla capitolo 5 per una discussione più approfondita.
Discussione su perchè non è stato usato e limite dell'accelleratore hardware non è stato reso ancora compatibile, quindi l'accelleratore dovrebbe essere disabilitato.
Solo i primi pacchetti del flusso passano dal kernel e poi passano dal fast path, solo in caso di pesanti modifiche hw e software possono essere analizzati.
Dove è stato usato e dove no e perchè non è stato usato per i test. -->

4.4 Il nostro tool


Il picco da 2.5K non sappiamo come considerarlo perchè non è un attacco ma è anomalo, quindi cosa bisogna fare? Avvisare l'amministrattore o cosa


Stazionarietà dei dati => Quanto variano, periodo in cui variano => Più sono stazionari più è facile, altrimenti bisogna valutare di riallenarla o algoritmi di incremental learning, e dati che non so come trattare
paper cisco da citare
http://library.usc.edu.ph/ACM/KKD%202017/pdfs/p1723.pdf

<!-- Giustificare il margine -->

<!-- Scrivere che le reti neurali non sono facili da padroneggiare a 360° => sono sistemi non lineari decisamente complessi con risultati abbastanza imprevedibili -->

Accennare come vengono allenate le reti

<!-- Il focus non è solo sulle reti, per la produzione si può lavorare meglio per trovare la rete ottima -->

applicazione alternativa dell'anomaly detection tramite autoencoders => vedi slide itasec


rimuovere logo kaspersky 
<!-- e diritti tiesse -->

com'è il flusso di dati ndpi?
<!-- 
Nella caso in cui si vogliano aggiungere dei software per monitorare questi servizi esisto solitamente tre soluzioni: la prima e la più complicata è quella di fare aggiungere il codice all'interno del kernel linux, ma bisogna avere le giuste motivazionie e passeranno anni prima della distribuzione, la seconda è quella di creare un modulo kernel personalizzato da integrare, questo potrebbe portare a vulnerabilità blbla, la terza la esporeremo succesivamente.

%Todo: Cercare articolo dove ne parla

La prima versione del nostro software è stata sviluppata scrivendo un modulo kernel che utilizzasse netfilter. Questa soluzione è la strada tradizionalmente usata nel mondo Linux e in Tiesse per l'implementazione delle proprie personalizzazioni nei prodotti. -->




<!-- conclusioni anomaly detection -->

spiegare il motivo della scelta degli autoencoders => leggere articolo

spiegare funzionamento mitigation:

- versione A semplificata
  - ordina in flussi da quello che trasmette di più in base alla feature che ha scatenato l'anomalia
  - interfaccia per bloccare e blocco inserito tramite ebpf
- versione B con anomaly detection
  - versione automatica con una rete per flussi
  - spiegare vantaggi e svantaggi
  - spiegare come funziona
  - se riesco parlare dei test




- l test di nmap è adatto anche a identificare port scanning di botnet
- Attacchi DDoS famosi
- Allenamento rete neurale
- stazionarietà dei dati
- ogni quanto eseguire il train
- confronto con altre soluzioni
- esempi soluzioni anti ddos distibuite
- https://blog.cloudflare.com/building-rakelimit/
- https://blog.cloudflare.com/cloudflare-architecture-and-how-bpf-eats-the-world/
- tabella lsmt
- immagini ricostruzioni
- listing 4.3 e 4.4 con lo stesso formato