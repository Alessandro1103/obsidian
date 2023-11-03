Date: 2023-11-03
Time: 22:49
Tags: #Java #UML #Appunti #Università 
Up: [[UML]]

---
# Appunti

## Segnatura
Possiamo fare 3 segnature: AttivitàComplesse, AttivitàAtomiche, SegnaliIO

AttivitàComplesse:
```
AttivitàPrincipale(/*parametri in ingresso*/):(/*parametri in uscita*/)
AttivitaDiFlussi(/*parametri in ingresso*/):(/*parametri in uscita*/)
```
AttivitàAtomiche:
```
AttivitàAlDiFuoriDiFlussi(/*parametri in ingresso*/):(/*parametri in uscita*/)
```
SegnaliIO:
```
SegnaliIO(/*parametri in ingresso*/):(/*parametri in uscita*/)
```
## Specifica Stati
Molto semplice, scriviamo solo quello che abbiamo disegnato nel diagramma degli stati
```
InizioSpecificaStatiClasse Pippo
	Stato {STATO_0, STATO_1...}
	Variabili di stato audiliarie:
		 oggetti di payload
		 dest/mitt rilevanti
	 Statoiniziale:
		 statoCorrente = Stato.STATO_0
FineSpecifica
```
## Specifica Transizioni
```
InizioSpecificaTransizioniClasse Classe
	Transizione:STATO_0 -> STATO_1
		Evento(payload)[condizione]{dest/mitt}/Evento(payload){dest/mitt}
	Evento: Evento(payload:tipo)
	Condizione: condizione
	Azione:
		pre: evento.mitt == this.link
		post: specifica del nuovo Evento
FineSpecifica
```
## Specifica Attività
### Specifica Attività Principale
```
InizioSpecificaAttivita Principale
	Principale()
VariabiliProcesso
	variabili di ingresso e uscita che serviranno dopo
InizioProcesso
	funzioni(parametriIngresso):(parametriUscita)
	while/if
	fork->thread
FineProcesso
FineSpecifica
```

Il fork è sempre bene realizzarlo nel seguente modo:
```
fork {
	thread t1: {
		funzioni
	}
	thread t2: {
		funzioni
	}
}
join t1, t2
```

### Specifica Attività Atomica

```
InizioSpecificaAttivitàAtomica Attività
	Attivita(parametriIngresso):(parametriUscita)
	pre:
		condizioni precedenti all'evento
	post:
		condizioni successive all'evento
FineSpecifica
```

### Specifica Attività I/O

```
InizioSpecificaAttivitàAtomica Attività
	Attivita(parametriIngresso):(parametriUscita)
	pre:
		condizioni precedenti all'evento
	post:
		condizioni successive all'evento
FineSpecifica
```

## Realizzazione classi

### Rappresentazione di una classe

![[Pasted image 20230709161254.png]]

Le proprietà immutabili hanno la condizione di essere #final
Per ogni attributo dobbiamo avere un #get e un #set, a meno che questo non sia final, allora avrà solo un get. Riscriviamo il #toString.
Se un attributo ha un vincolo numerico possiamo verificarlo nel costruttore e nel set chiamando #EccezionePrecondizioni, in questo caso va creato la classe di #EccezionePrecondizioni 
``` java
public class Persona { 
	private final String nome, cognome; 
	private final int giorno_nascita, mese_nascita, anno_nascita; 
	private boolean coniugato; 
	public Persona(String n, String c, int g, int m, int a) {
		nome = n;
		cognome = c;
		giorno_nascita = g; 
		mese_nascita = m;
		anno_nascita = a;
	}
	public String getNome() {
		return nome;
	}
	public String getCognome() {
		return cognome;
	} 
	public int getGiornoNascita() {
	return giorno_nascita;
	} 
	public int getMeseNascita() {
	return mese_nascita;
	}
	public int getAnnoNascita() { 
		return anno_nascita; 
	} 
	public void setConiugato(boolean c) {
		coniugato = c;
	} 
	public boolean getConiugato() {
		return coniugato;
	} 
	public String toString() {
		return nome + ’ ’ + cognome + ", " + giorno_nascita + "/" + mese_nascita + "/" + anno_nascita + ", " + (coniugato?"coniugato":"celibe"); 
	}
}
```

### Responsabilità singola

#### Molteplicità 0,1 

![[Pasted image 20230709163802.png]]

Ovviamente abbiamo responsabilità verso Persona, in qualche modo Libro dovrà caricarsi Persona, visto che il link non ha niente di speciale, possiamo considerare semplicemente Persona come attributo di Libro. Come attributo deve avere get e set.

Persona:
``` java
public class Persona {
	private final String nome; 
	public Persona(String n) { 
		nome = n; 
	} 
	public String getNome() { 
		return nome; 
	} 
	public String toString() { 
		return nome ; 
	}
}
```

Libro:
``` java
public class Libro {
	private final String titolo;
	private final int annoStampa;
	private Persona autore;
	public Libro(String t, int a) {
		titolo = t;
		annoStampa = a;
	}
	public String getTitolo() {
		return titolo;
	}
	public String getAnnoStampa() {
		return annoStampa;
	}
	public Persona getAutore() {
		return autore;
	}
	public void setAutore(Persona p) {
		autore = a;
	}
	public String toString() {
		return titolo + (autore != null ? ", di " + autore.toString() : ", Anonimo") + ", dato alle stampe nel " + annoStampa; }
}
```

#### Molteplicità 1,1

![[Pasted image 20230709172335.png]]

Ovviamente abbiamo responsabilità verso Ente, in qualche modo AziendaPubblica dovrà caricarsi Ente, visto che il link non ha niente di speciale, possiamo considerare semplicemente Ente come attributo di AziendaPubblica. Come attributo deve avere get e set. Visto che ha molteplicità 1,1 deve esserci sempre 1 ente, ma il controllo lo facciamo solo quando è richiesto il get con #EccezioneMolteplicita. Se avessimo altri valori ancora, sarà sufficiente creare un HashSet e verificare che quando chiamiamo get, questi rispetti le condizioni di progetto (uguale a questo, ma con altri valori).

``` java 
public class AziendaPubblica extends Azienda {
	private final String nome, descrizione;
	private Ente gestore;
	public AziendaPubblica(String n, String d) {
	    nome = n;
	    descrizone = d;
  }
public String getNome() {
	return nome;
}
public String getCognome() {
	return cognome;
}
  public void setGestore(Ente e) {
    if (e != null)
      gestore = e;
  }
  public Ente getGestore() throws EccezioneMolteplicita {
    if (gestore == null)
      throw new EccezioneMolteplicita("Molteplicita min/max violata");
    return gestore;
  }
}
```

#### Molteplicità 0,*

![[Pasted image 20230709182607.png]]

``` java
public class Persona { 
	private final String nome; 
	private HashSet<Azienda> haLavorato; 
	public Persona(String n) { 
		nome = n; 
		haLavorato = new HashSet<Azienda>(); 
	} 
	public String getNome() { 
		return nome; 
	} 
	public void inserisciLinkHaLavorato(Azienda az) { 
		if (az != null) 
			haLavorato.add(az); 
	} 
	public void eliminaLinkHaLavorato(Azienda az) { 
		if (az != null) 
			haLavorato.remove(az);
	} 
	public Set getLinkHaLavorato() { 
			return (HashSet)haLavorato.clone(); 
	}
}
```

#### Molteplicità 0,1 con attributi

![[Pasted image 20230709182817.png]]

Visto che il link sembra diventare una vera e propria classe, diventa sempre più complicato accorparla ad una sola classe, possiamo gestire il link come una vera e propria struttura detta #TipoLink che negli esempi precedenti prende esattamente il posto delle associazioni. Tutti gli attributi del #TipoLink sono #final, perché non devono mutare.
In questo caso #inserisciLink deve controllare che il link non esista già, che quello che viene fornito sia valido e che il destinatario del collegamento sia effettivamente io.
 
Persona:
``` java
public class Persona { 
	private final String nome;
	private TipoLinkLavora link; 
	public Persona(String n) { 
		nome = n; 
	}
	public String getNome() { 
		return nome; 
	} 
	public void inserisciLinkLavora(TipoLinkLavora t) { 
	if (link == null && t != null && t.getPersona() == this) 
		link = t; 
	} 
	public void eliminaLinkLavora() { 
		link = null; 
	} 
	public TipoLinkLavora getLinkLavora() { 
		return link; 
	}
}
```

TipoLinkLavoro:
``` java
public class TipoLinkLavora { 
	private final Persona laPersona; 
	private final Azienda laAzienda; 
	private final int annoAssunzione; 
	public TipoLinkLavora(Azienda x, Persona y, int a) throws EccezionePrecondizioni { 
		if (x == null || y == null) throw new EccezionePrecondizioni ("Gli oggetti devono essere inizializzati"); 
		laAzienda = x; 
		laPersona = y; 
		annoAssunzione = a; 
	} 
	public boolean equals(Object o) { 
		if (o != null && getClass().equals(o.getClass())) { 
			TipoLinkLavora b = (TipoLinkLavora)o; 
			return b.laPersona == laPersona && b.laAzienda == laAzienda; 
		} 
		else 
			return false; 
	} 
	public int hashCode() { 
		return laPersona.hashCode() + laAzienda.hashCode(); 
	} 
	public Azienda getAzienda() { 
		return laAzienda; 
	}
	public Persona getPersona() { 
		return laPersona; 
	} 
	public int getAnnoAssunzione() { 
			return annoAssunzione; 
		} 
}
```


### Molteplicità 0,* con attributi

![[Pasted image 20230709184405.png]]

Visto la complicatezza del link è giusto creare un #TipoLink adeguato

TipoLinkHaLavorato:
``` java
public class TipoLinkHaLavorato {
	private final Persona persona;
	private final Azienda azienda;
	private final int annoInizio;
	private final int annoFine;
	public TipoLinkHaLavorato(Persona p, Azienda a, int ai, int af) throws EccezionePrecondizioni {
		if (p==null || a==null) 
			throw EccezionePrecondizioni("Gli oggetti vanno inizializzati")
		persona = p;
		azienda = a;
		annoInizio = ai;
		annoFine = af;
	}
	public Persona getPersona() {
		return persona;
	}
	public Azienda getAzienda() {
		return azienda;
	}
	public int getAnnoInizio() {
		return annoInizio;
	}
	public int getAnnoFine() {
		return annoFine;
	}
	public boolean equals(Object o) {
		if (o!=null && getClass().equals(o.getClass())) {
			TipoLinkHaLavorato tlha = (TipoLinkHaLavorato) o;
			return tlha.getAzienda()==this.azienda && tlha.getPersona()==this.persona;
		}
		else
			return false;
	}
	public int hashCode() {
		return persona.hashCode() + azienda.hashCode();
	}
}
```

Persona:
``` java
public class Persona {
	private final String nome;
	private HashSet<TipoLinkHaLavorato> azienda;
	public Persona(String n) {
		nome=n;
		azienda = new HashSet<TipoLinkHaLavorato>();
	}
	public String getNome() {
		return nome;
	}
	public void inserisciTipoLinkHaLavorato(TipoLinkHaLavorato tlha) {
		if (tlha!=null && tlha.getPersona()==this)
			azienda.add(tlha);
	}
	public void eliminaTipoLinkHaLavorato(TipoLinkHaLavorato tlha) {
		if (tlha!=null && tlha.getPersona()==this)
			azienda.remove(tlha);
	}
	public Set<TipoLinkHaLavorato> getInsiemeAzienda() {
			return (HashSet<TipoLinkHaLavorato) azienda.clone();
	}
} 
```


### Responsabilità doppia -> Manager

In questa situazione visto che esiste un oggetto centrare, non appartenente a nessuno dei due, devo creare un TipoLinkOccupazione, la molteplicità influisce solo condizioni e il tipo che che vado ad assegnare a "link", se avessi avuto più valori avrei avuto un insieme e quindi un HashSet. Devo implementare quindi 2 class per le 2 classi, 1 TipoLink per il link e 1 Manager
Attenzione che il controllo delle molteplicità le fa direttamente il manager in questo caso, perche il link c'e o non c'e da entrambe le parti. Se avessi 01 solo da un latro il controllo lo faccio solo su uno e quindi sul InserisciPerManager o anche inserisciTipoLink.

![[Pasted image 20230709153316.png]]

Persona, come una normale classe ha:
- attributi, tra cui anche l'associazione, link
- costruttore
- get di ogni attributo
- inserisci e elimina dei TipiLink che chiamano il Manager, avendo un link come parametro dobbiamo vedere che si riferisce a noi, e che non sia null
- inserisci e elimina per il Manager, dobbiamo vedere che non sia null

``` java
public class Persona {
	private final String nome;
	private TipoLinkOccupazione link;
	public Persona(String n) {
		nome = n;
	}
	public String getNome() { 
		return nome; 
	}
	public void inserisciLinkOccupazione(TipoLinkOccupazione t) {
		if (t != null && t.getPersona()==this)
			ManagerOccupazione.inserisci(t);
	}
	public void eliminaLinkOccupazione(TipoLinkOccupazione t) {
		if (t != null && t.getPersona()==this)
			ManagerOccupazione.elimina(t);
	}
	public TipoLinkOccupazione getLinkOccupazione() {
		return link;
	}
	public void inserisciPerManagerOccupazione(ManagerOccupazione a) {
		if (a != null) 
			link = a.getLink();
	}
	public void eliminaPerManagerOccupazione(ManagerOccupazione a) {
		if (a != null) 
			link = null;
	}
}
```

Stanza, come una normale classe ha:
- attributi, tra cui anche l'associazione, link
- costruttore
- get di ogni attributo
- inserisci e elimina dei TipiLink che chiamano il Manager, avendo un link come parametro dobbiamo vedere che si riferisce a noi, e che non sia null
- inserisci e elimina per il Manager, dobbiamo vedere che non sia null
``` java
public class Stanza {
	private final int numero;
	private TipoLinkOccupazione link;
	public Stanza(int n) { 
		numero = n; 
	}
	public int getNumero() {
		 return numero;
	}
	public void inserisciLinkOccupazione(TipoLinkOccupazione t) {
		if (t != null && t.getStanza()==this)
			ManagerOccupazione.inserisci(t);
	}
	public void eliminaLinkOccupazione(TipoLinkOccupazione t) {
		if (t != null && t.getStanza()==this)
			ManagerOccupazione.elimina(t);
	}
	public TipoLinkOccupazione getLinkOccupazione() {
		return link;
	}
	public void inserisciPerManagerOccupazione(ManagerOccupazione a) {
		if (a != null) 
			link = a.getLink();
	}
	public void eliminaPerManagerOccupazione(ManagerOccupazione a) {
		if (a != null) 
			link = null;
	}
}
```

TipoLinkOccupazione è un classico TipoLink, punti da ricordare:
- EccezionePrecondizioni: controlla che non venga chiamato quando mancano delle classi
- è un astrazione di valore, quindi devo rifare equals e hashcode
``` java
public class TipoLinkOccupazione {
	private final Stanza laStanza;
	private final Persona laPersona;
	private final int daAnno;
	public TipoLinkOccupazione(Stanza x, Persona y, int a) throws EccezionePrecondizioni {
		if (x == null || y == null)
		throw new EccezionePrecondizioni("Gli oggetti devono essere inizializzati");
		laStanza = x;
		laPersona = y;
		daAnno = a;
	}
	public boolean equals(Object o) {
		if (o != null && getClass().equals(o.getClass())) {
		TipoLinkOccupazione b = (TipoLinkOccupazione)o;
		return b.laPersona == laPersona && b.laStanza == laStanza;
		}
	else 
		return false;
	}
	public int hashCode() {
		return laPersona.hashCode() + laStanza.hashCode();
	}
	public Stanza getStanza() {
		return laStanza;
	}
	public Persona getPersona() {
		return laPersona;
	}
	public int getDaAnno() {
		return daAnno;
	}
}
```

Manager, con le seguenti caratteristiche:
- costruttore privato, chiamato dalle funzioni di inserisci e elimina
- un attributo al link collegato
- una funzione di inserisci ed elimina che prendono un TipoLink in ingresso, che non deve essere null, poi sono state inseriti dei controlli in INSERISCI sulle molteplicità che potrebbero non esserci. Valgono solo perche non possiamo avere più di 1 collegamento. Mentre su ELIMINA dobbiamo SEMPRE VERIFICARE che quello che stiamo togliendo sia il link corretto. Le funzioni di INSERISCI ed ELIMINA sono STATIC
``` java
public final class ManagerOccupazione {
	private ManagerOccupazione(TipoLinkOccupazione x) {
		link = x;
	}
	private TipoLinkOccupazione link;
	public TipoLinkOccupazione getLink() { 
		return link;
	}
	public static void inserisci(TipoLinkOccupazione y) {
		if (y != null && y.getPersona().getLinkOccupazione()==null && y.getStanza().getLinkOccupazione()==null) {
			ManagerOccupazione k = new ManagerOccupazione(y);
			y.getStanza().inserisciPerManagerOccupazione(k);
			y.getPersona().inserisciPerManagerOccupazione(k);
		}
	}
	public static void elimina(TipoLinkOccupazione y) {
		if (y != null && y.getPersona().getLinkOccupazione().equals(y)) {
			ManagerOccupazione k = new ManagerOccupazione(y);
			y.getStanza().eliminaPerManagerOccupazione(k);
			y.getPersona().eliminaPerManagerOccupazione(k);
		}
	}
}
```

### Generalizzazioni (ISA)

![[Pasted image 20230709162958.png]]

Questa è una classe semplice, se sapessi che non può essere chiamata, perché le classi figlie sono complete, diventerebbe una classe #abstract.
``` java
package Libro;
public class Libro { 
	protected final String titolo;
	protected final int annoStampa;
	public Libro(String t, int a) {
		titolo = t; annoStampa = a;
	} 
	public String getTitolo() { 
		return titolo; 
	} 
	public int getAnnoStampa() { 
		return annoStampa; 
	} 
	public String toString() { 
		return titolo + ", dato alle stampe nel " + annoStampa; 
	} 
}
```

La classe figlia ha tutte le caratteristiche di quella padre, quindi quello che abbiamo già lo chiamiamo con #super 

``` java
public class LibroStorico extends Libro {
	protected final String epoca;
	public LibroStorico(String t, int a, String e) {
		super(t,a);
		epo
		
		ca = e; 
	} 
	public String getEpoca() { 
		return epoca; 
	} 
	public String toString() { 
		return super.toString() + ", ambientato nell’epoca: " + epoca; 
	} 
}
```

 
### Eccezioni

Nella costruzioni delle classi possiamo avere 2 tipi di Eccezioni: #EccezioneMolteplicita o #EccezionePrecondizioni, la prima perché qualche molteplicità non è stata rispettata, di fatto è una eccezione che vogliamo lanciare noi, la seconda può includere la prima, si riferisce a quando inizializziamo qualcosa in maniera sbagliata.

EccezionePrecondizioni:
``` java
public class EccezionePrecondizioni extends Exception {
	private String messaggio;
	public EccezionePrecondizioni(String m) {
		messaggio = m;
	}
	public EccezionePrecondizioni() {
		messaggio = "Si e’ verificata una violazione delle precondizioni";} 
	public String toString() {
		return messaggio;
	}
}
```

EccezioneMolteplicità:
``` java
public class EccezioneMolteplicita extends Exception {
	private String messaggio;
	public EccezionePrecondizioni(String m) {
		messaggio = m;
	}
	public String toString() {
		return messaggio;
	}
}
```

### Fired

Se di una classe ci interessano gli stati e transizioni, magari questa funge come evento etc, allora va considerata come listener e le è permesso usare la funzione fired():

``` java
public class Giocatore implements Listener {
	public static enum Stato {
		ALLENAMENTO, INGIOCO, FINEGIOCO
	}
	Stato statoCorrente = Stato.Allenamento;
	double trattoPercorso;
	public Stato getStato() {
		return statoCorrente;
	}
	public void fired(Evento e) {
		TaskExecutor.getIstance().perform(new GiocatoreFired(this,e));
	}
}
```

la funzione #fired, non restituisce eventi e delega la gestione delle transizioni ad un #funtore 
molto più chiaro con l'esempio [[Esame 20-02-2020]]

### Subset
![[Pasted image 20230714172245.png]]

Dove Personaggio ha responsabilità singola su Quadro, mentre dedicatoA avrà bisogno di un Manager. L'implementazione la vediamo nelle classi quando andiamo a fare i get e i corrispondenti controlli

``` java
public class TipoLinkDedicatoA {
	private final Personaggio ilPersonaggio;
	private final QuadroDedicato ilQuadroDedicato;
	public TipoLinkDedicatoA(QuadroDedicato q, Personaggio p) throws EccezionePrecondizioni{
		if (q==null || p==null)
			throw new EccezionePrecondizioni("Gli oggetti devono essere inizializzati");
		ilQuadroDedicato = q;
		ilPersonaggio = p;
	}
	public boolean equals(Object o) {
		if (o!=null && getClass().equals(o.getClass())) {
			TipoLinkDedicatoA b = (TipoLinkDedicatoA) o;
			return b.ilPersonaggio == ilPersonaggio && b.ilQuadroDedicato == ilQuadroDedicato;
		}
		return false;
	}
	public int hashCode() {
		return ilPersonaggio.hashCode() + ilQuadroDedicato.hashCode();
	}
}

public final class ManagerDedicatoA {
	private ManagerDedicatoA(TipoLinkDedicatoA x) {
		link=x;
	}
	private TipoLinkDedicatoA link;
	public TipoLinkDedicatoA getLink() {
		return link;
	}
	public static void inserisci(TipoLinkDedicatoA y) {
		if (y!=null && !y.getQuadroDedicato().estPresenteLinkDedicatoA()) {
			ManagerDedicatoA k = new ManagerDedicatoA(y);
			k.link.getQuadroDedicato().inserisciPerManagerDedicatoA(k);
			k.link.getPersonaggio().inserisciPerManagerDedicatoA(k);
		}
	}
	public static void elimina(TipoLinkDedicatoA y) {
		if (y!=null) {
			ManagerDedicatoA k = new ManagerDedicatoA(y);
			k.link.getQuadroDedicato().eliminaPerManagerDedicatoA(k);
			k.link.getPersonaggio().eliminaPerManagerDedicatoA(k);
		}
	}
}
```

Classi:
``` java
public class Personaggio {
	private String fileImmagine;
	private HashSet<Quadro> presente;
	private HashSet<TipoLinkDedicatoA> dedicato;
	public Personaggio(String fi) {
		fileImmagine = fi;
		presente = new HashSet<Quadro>();
		dedicato = new HashSet<TipoLinkDedicatoA>();
	}
	public String getFileImmagine() {
		return fileImmagine;
	}
	public void setFileImmagine(String fi) {
		fileImmagine=fi;
	}
	...
	public Set<TipoLinkDedicatoA> getLinkDedicatoA() throws EccezioneSubset {
		Iterator<TipoLinkDedicatoA> it dedicato.iterator();
		while (it.hasNext()) {
			QuadroDedicato q = it.next().getQuadroDedicato();
			if (!presente.contains(q))
				throw new EccezioneSubset("dedicatoA non è un sebset di presente");
		}
		return (HashSet<TipoLinkDedicatoA>) dedicato.clone();
	}
}

public class QuadroDedicato extends Quadro {
	protected String fileFilmato;
	protected TipoLinkDedicatoA dedicato;
	public QuadroDedicato(String fa, String ff) {
		super(fa);
		fielFilmato = ff;
		dedicato = null;
	}
	public String getFileFilmato() {
		return fileFilmato;
	}
	public void setFileFilmato(String ff) {
		fileFilmato = ff;
	}
	public boolean estPresenteLinkDedicatoA() {
		return dedicato!=null;
	}
	public void inserisciLinkDedicatoA(TipoLinkDedicatoA t) {
		if (t!=null && t.getQuadroDedicato()==this)
			ManagerDedicatoA.inserisci(t);
	}
	public void liminaLinkDedicatoA(TipoLinkDedicatoA t) {
		if (t!=null && t.getQuadroDedicato()==this)
			ManagerDedicatoA.elimina(t);
	}
	public void inserisciPerManagerDedicatoA(ManagerDedicatoA a) {
		if (a!=null)
			dedicato = a.getLink();
	}
	public void eliminaPerManagerDedicatoA(ManagerDedicatoA a) {
		if (a!=null)
			dedicato = null;
	}
	public TipoLinkDedicatoA getLinkDedicatoA() throws EccezioneMolteplicita, EccezioneSubset {
		if (!estPresenteLinkDedicatoA())
			throw new EccezioneMolteplicita("Violata molteplicità minima");
		if (!dedicato.getPersonaggio().getLinkPresente().contains(this))
			throw new EccezioneMolteplicita("dedicatoA non è un subset di presente");
		return dedicato:
	}
}
```

## Realizzazione stati e transizioni

``` java
public class MioOggettoConStato implements Listener {
	public static enum Stato {STATO_0, STATO_1, STATO_2, /*...*/ STATO_n} 
	private Stato statocorrente = Stato.STATO_0; 
	private Object varAux = null;
	public Stato getStato() { 
		return statocorrente
	}
	// gestione delle transizioni
}
```

successivamente dobbiamo aggiungere la Gestione delle transizioni:
questa avviene con la classe fired() che prende come parametro l'evento scatenante, per farlo conoscere a tutti deve farlo conoscere all'Enviroment. La funzione fired() è specificata dall'interfaccia di Listener:

``` java
public interface Listener { 
	public void fired(Evento e);
}
public class OggettoConStato implements Listener { …
		// Gestine delle transizioni public void fired(Evento e) { …
	} 
}
```

Fired deve essere eseguito concorrentemente, deve quindi essere in grado di chiamare un #funtore 

==Bisogna controllare prima di eseguire che il destinatario sia io, per farlo vediamo l'opposto ovvero se il destinatario non sia io e non sia un messaggio mandato in broadcast==
``` java
class GiocatoreFired implements Task { 
	private boolean eseguita = false; 
	private Giocatore g; 
	private Evento e;
	public GiocatoreFired(Giocatore g, Evento e) { 
		this.g = g; 
		this.e = e; 
	}
	public synchronized void esegui() { 
		if (eseguita || (e.getDestinatario() != g && e.getDestinatario() != null)) 
			return;
		eseguita = true; 
		switch (g.getStato()) { 
			… 
			case INGIOCO: 
				if (e.getClass() == Bastone.class)
					if (g.trattopercorso < 100) { 
						… 
						// il cast lo facciamo sempre 
						EventoScatenante evento = (EventoScatenante) e; // in questo caso Bastone bastone = (Bastone) e;
						classe.oggettoDelPayload =  evento.getPayload(); 
						Environment.aggiungiEvento(new Bastone(//classe non fired, //destinazione)); 
						g.statocorrente = Stato.INGIOCO;
					} 
					else { 
					// trattopercorso >= 100 …
				} break;
			… 
			default: 
				throw new RuntimeException("Stato corrente non riconosciuto.");
		} 
	}
	public synchronized boolean estEseguita() { 
		return eseguita; 
	} 
}
```

molto più chiaro con l'esempio [[Esame 20-02-2020]]
in ogni case, facciamo il controllo se la classe evento sia quella dell'evento scatenante (vedere grafico stati e transizioni). Poi chiamiamo la il nuovo evento: con Environment e cambiamo stato. Dentro

## Realizzazione attività 

Per una realizzazione di una attività ci facciamo sempre ad un #funtore e a delle classi che implementano Task(funtore), spesso le cose richieste le abbiamo già scritte nel diagramma delle attività o nelle segnature

### Realizzazione Attività complessa

``` java
public class Classe implements Runnable {
	private boolean eseguita;
	// attribuiti
	public Classe(/*attributi*/) {
		//assegnazione
	}
	public synchronized void run() {
		if (estEseguita() == true)
			return 
		eseguita = true;
		// tutte operazioni
	}
	public synchronized boolean estEseguita() {
		return eseguita;
	}
}
```

se parliamo di attività complesse dentro ci sono spesso richiami ad altre funzioni, queste vengono eseguiti dal TaskExecutor, per esempio:

``` java
Attivita a = new Attivita(/*parametri*/);
TaskExecutor.getIstance().perform(a);
boolean res = a.getResult();
```

se parliamo invece di semplici segnali I/O:

``` java
segnaliIO.funzione(/*paramtri*/);
```

se parliamo invece di thread:
``` java
Attivita a1 = new Attivita(/*parametri*/);
Thread t1 = new Thread(a1);
t1.start();
Attivita a2 = new Attivita(/*parametri*/);
Thread t2 = new Thread(a2);
t2.start();
try {
	t1.join();
	t2.join();
} catch (InterruptedException e) {
	e.printStackTrace();
}
```
==ricorda l'errore==

### Realizzazione Attività Atomica

``` java
public class Classe implements Task {
	private boolean eseguita;
	// attribuiti
	public Classe(/*attributi*/) {
		//assegnazione
	}
	public synchronized void esegui() {
		if (estEseguita() == true)
			return 
		eseguita = true;
		// tutte operazioni
	}
	public synchronized boolean estEseguita() {
		return eseguita;
	}
}
```


---
# References
