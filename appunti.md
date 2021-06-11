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

Perché autoencoders
Quali sono i vantaggi rispetto ad altre soluzioni:

- parlo del fatto che sfruttiamo le api messe a disposizione di keras e tensorflow perché sono facili da usare, ci sono soluzioni alternative da citare (tool di twitter scritto in R => informarsi)
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
Discussione su perché non è stato usato e limite dell'accelleratore hardware non è stato reso ancora compatibile, quindi l'accelleratore dovrebbe essere disabilitato.
Solo i primi pacchetti del flusso passano dal kernel e poi passano dal fast path, solo in caso di pesanti modifiche hw e software possono essere analizzati.
Dove è stato usato e dove no e perché non è stato usato per i test. -->

4.4 Il nostro tool


Il picco da 2.5K non sappiamo come considerarlo perché non è un attacco ma è anomalo, quindi cosa bisogna fare? Avvisare l'amministrattore o cosa


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

Per dati stazionari si intende quando le proprietà statistiche dei dati non si evolvono nel tempo, questo non significa che i dati puntuali non variano, ma che il valore medio e la varianza rimangano costanti. Questa condizione sarebbe ideale per i nostri meccanismi di anomaly detection, ma è difficilmente attuabile in un contesto reale, in cui sono presenti dei trend e i dati potrebbero essere soggetti ad una stagionalità.


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
- stazionarietà dei dati => https://towardsdatascience.com/why-does-stationarity-matter-in-time-series-analysis-e2fb7be74454
- ogni quanto eseguire il train
<!-- - esempi soluzioni anti ddos distibuite -->
- https://blog.cloudflare.com/building-rakelimit/
- https://blog.cloudflare.com/cloudflare-architecture-and-how-bpf-eats-the-world/
- tabella lsmt
<!-- - immagini ricostruzioni -->
- listing 4.3 e 4.4 con lo stesso formato

<!-- Still dangerous to block/modify traffic belonging to
mission-critical apps without human intervention -->

specificare che la protezione può essere effettuata solo verso i servizi aziendali o con una maggiore attenzione verso quelli

rifare figura 2.2

<!-- conclusioni => 
Gli attacchi informatici nelle reti business sono sempre più pericolosi a causa della sempre maggiore dipendenza delle aziende dai sistemi informatici, per questo motivo il problema di un singolo distaccamento non deve creare malfunzionamenti all'intera azienda.
parlo dell'architettura e dei vantaggi dati
Un sistema con filtraggio distribuito come quello da noi proposto permette di non intasare il centro della rete, ma cerca di limitare i problemi direttamente nei CPE.
La soluzione da noi proposta permette di usare l'infrastruttura già esistente e permette di essere facilmente modellata per il monitoraggio di servizi specifici.
parlo della scelta del sistema per rilevare gli attacchi, gli attacchi DDoS tendenzialmente creano delle grandi differenze nel traffico dati, per questo motivo abbiamo adottato un meccanismo basato sul riconoscimento delle anomalie.
Lavorando su dei dati aggregati nella prima fase il sistema è in grado di ottenere migliori prestazioni rispetto ai sistemi signature-based, i quali devono analizzare ogni flusso e ha il vantaggio di non dovere effettuare aggiornamenti delle regole per riconoscere nuovi attacchi, ma solamente dei nuovi allenamenti del modello, in caso di traffico non stazionario.
Inoltre per i successivi allenamenti della rete si sarà a conoscenza degli intervalli di tempo in cui si sono verificate delle anomalie e se saranno confermate da un amministratore di rete, quei dati potranno essere esclusi e si continuerà a considerarli anomali.
Il sistema mirando al riconoscimento di anomalie generiche potrà essere facilmente esteso per riconoscimento di altre tipologie di attacchi.
 e degli autoencoders, tramite i quali analizziamo informazioni quantitative riguardo al traffico, il sistema è paragonabile ad altri sistemi di anomaly detection. Un sistema di a
Se il traffico generato da un attacco non scatena anomalie, potrà essere facilmente tollerato dalla rete senza creare disservizi.
In presenza di anomalia possiamo decidere il comportamento da tenere in base alla criticità del servizio protetto, ma in ogni caso l'amministratore di rete si troverà molto aiutato nel prendere le decisioni. -->
<!-- 
 Aggregare il traffico di tutte le sedi, per avere una panoramica ancora maggiore in caso di attacchi a basso low rate (vedi capitolo x) non riconosciuti.

  -->

Tolleranza => ntrusion tolerance is the ability of a system to continue providing (possibly degraded but) adequate services after a penetration.  the  intrusion  tolerance  of  DDoS  attacks  is  an﻿important issue to mitigate the damage during DDoS attacksfor providing the critical services continuously on Interne Per sviluppare un sistema tollerante agli attacchi DDoS bisogna agire preventivamente tramite l'introduzione per la differenziazione del servizio, 
https://www.sciencedirect.com/science/article/abs/pii/S0957417404000417
Tolerance
When the results of the detection algorithm come out to
be unsuccessful or when it becomes hard to apply a
detection process, it is important to find out the alterna-
tives. Tolerance mechanism is the alternative to this. 136
The techniques of tolerance mechanism work with a
very little or even no knowledge about the result of the
detection. Thus, it is the final stage of defense when
the other stages (prevention and detection) fail. Thus,
the goal of this mechanism is to provide maximum pos-
sible quality of service by minimizing the impacts of the
attack. The research found in this field can be classified
into congestion policing and fault tolerance.
Congestion policing. The main target of a bandwidth
flooding attack is to congest the resource. 45,66 The
impact of this type of attacks can be reduced or elimi-
nated by applying congestion policing mechanism. Re-
feedback 137 and NetFence 138 are two example mechan-
isms where congestion policing is applied to defend
DDoS attacksFault tolerance. Fault tolerance ensures high availability
of the system. In fault tolerance system, the basic idea
is to replicate or multiply the resource of a system such
as software, hardware. There are some research found
in this field which works to identify the applicability of
the fault toleran


in cloudfare usano la stessa soluzione per ovviare ai limiti della granularità delle metriche da collezionare https://blog.cloudflare.com/cloudflare-architecture-and-how-bpf-eats-the-world/


come limitare la banda eBPF 


pag. 26
API anzichè api
"...e di passare da una fase sperimentale a una di produzione in maniera molto rapida con poche righe di codice. Questo è valido di per sè per qualsiasi strumento di ML scritto in Python."
Manca riferimento a quell'articolo keras anomaly-detection.
Per quanto riguarda la pag. 26 il virgolettato riguarda keras e tensorflow


pag. 34
Storage dati su base temporale: parlare di come funzionano a cosa servono: prima di selezione features aggiungere sezione relativa allo storage dei dati su base temporale. Qui dilungati perché oltre che essere interessante al fine della discussione, è anche utile andare nel dettaglio:
https://graphite.readthedocs.io/en/latest/config-carbon.html
Usare le sezioni storage-schemas e storage-aggregation del link. Usare molto del teso di cui sopra e anche le immagini. Usare le sezioni storage-schemas e storage-aggregation del link. Usare molto del teso di cui sopra e anche le immagini.
Pagina 34 mi sembra una buona idea, parlo dei database temporali, ho approfondito molto l'argomento anche in generale oltre a capire come funziona grafite, perché vedendo come vengono gestiti i dati in Tiesse ho visto che i db temporali potevano tornare utilissimi anche per quanto riguardo il team studentesco e lo abbiamo iniziato ad usare anche per quello... Quindi posso aggiungere anche quello che è interessante e dire che è molto più comodo dei classici database. Comunque se per vedere la dimensione devo accedere da ssh non penso di avere l'accesso.


<!-- pag. 35
Acceleratore HW, parla di più! Spiega in generale come e cosa accelerano, indipendentemente dalla tecnologia Tiesse! Inoltre sei sicuro che questa sia la giusta sezione? Non è meglio parlarne quando descrivi il modulo Netfilter?
Non si capisce bene qual'è il problema con cui ti sei dovuto scontrare! Perché collectd va bene e il tuo modulo custom no? A cosa serviva il tuo modulo custom per quanto concerne le feauture??
Siccome l'impostazione della tesi è posata sul DoS, fai un ragionamento e una discussione delle feature legate ai DoS !!
Per quanto riguarda collectd in realtà non è difficile capire come mai funziona anche con l'acceleratore HW, il motivo è che collectd semplicemente legge dei contatori da file
Ma non c'è bisogno, se noti le metriche che raccogliamo noi non sono sul traffico specifico
L'unico intorto pesante fu su ndpi che Ivano lo modificò per farlo funzionare con l'acceleratore e qui basta che citi che Tiesse ha modificato l'ndpi per le metriche applicative
tutte le altre metriche n nriguarda il traffico specificoIl throughput sono i contatori delle interfacce che vengono aggiornati dal firmware delle NIC se non sbaglio; Il numero di connessioni necessità solamente del primo pacchettoE così via, comunque nella wiki di collectd qualcosa si trova riguardo ai pluginTutte queste cose scrivile, insomma fai una sorta di narrazione; va bene che la fai nella sezione featuresMa contestualizza bene cosa centra l'acceleratore con le metriche
Sì ma poi dilungati anche sui plguin collectd che usiamo noi se può servir
Ok grazie, vedo di sistemare, magari illustro il problema: ci servono ulteriori features per avere un anomaly detection più specifico verso le specifiche applicazioni. Poi dico come si potrebbe fare, ma illustro il problema dell'accelleratore hardware e di perché è un casino farlo, parlando di come mai ndpi e collectd non hanno quel problema -->

pag. 36
Schema della struttura del "nostro tool"

Lo pseudo codice e il codice è ancora più largo del corpo del testo normale...Cerca di restringere che si allunga anche.


<!-- Pag. 51
Dilungati su cosa blocca l'IP spoofing e su cosa rende "inutile" quindi l'anomaly-detecton per DoS mitigation. Considera che la tesi la deve capire anche un tecnico non puro networking...Entra nei dettagli tecnici qui -->





AVERE TRACCIA DEI FLUSSI PUÒ ESSERE UTILE PER ANALIZZARE I DATI NELLA FASE SUCCESSIVA ALL'ATTACCO