![[Pasted image 20230710120912.png]]
![[Pasted image 20230710120951.png]]

Fase di Progetto (responsabilità obbligatorie (Domanda 2)):
![[Pasted image 20230710121143.png]]

Secondo il testo era sufficiente fare le classi Giocatore, GiocatoreRosso, e le associazioni (Domanda 3):
``` java
Classi {
	public abstract class Giocatore {
		private final String nome;
		private final String avatar;
		public Giocatore(String n, String a) {
			nome = n;
			avatar = a;
		}
		public String getNome() {
			return nome;
		}
		public String getAvatar() {
			return avatar;
		}
		public String toString() {
			return nome + ' ' + avatar;
		}
	}
	
	public class Giallo extends Giocatore {
		private TipoLinkFormatoG torello;
		public Giallo(String n, String a) {
			super(n,a);
		}
		public void inserisciTipoLinkFormatoG(TipoLinkFormatoG t) {
			if (t!=null && t.getGiallo()==this)
				ManagerFormatoG.inserisci(t);
		}
		public void eliminaTipoLinkFormatoG() {
			if (t!=null && t.getGiallo()==this)
				ManagerFormatoG.elimina(t);
		}
		public TipoLinkFormatoG getTipoLinkFormatoG() {
			return torello;
		}
		public void inserisciPerManagerFormatoG(ManagerFormatoG m) {
			if (m!=null) 
				torello = m.getTipoLinkFormatoG();
		}
		elimina void eliminaPerManagerFormatoG(ManagerFormatoG m) {
			if (m!=null)
				torello = null;
		}
	}
	
	public class Rosso extends Giocatore {
		private TipoLinkFormatoR torello;
		public Rosso(String n, String a) {
			super(n,a);
		}
		public void inserisciTipoLinkFormatoR(TipoLinkFormatoR t) {
			if (t!=null && t.getRosso()==this && )
				ManagerFormatoR.inserisci(t);
		}
		public void eliminaTipoLinkFormatoR() {
			if (t!=null && t.getRosso()==this && )
				ManagerFormatoR.elimina(t);
		}
		public TipoLinkFormatoR getTipoLinkFormatoR() {
			return torello;
		}
		public void inserisciPerManagerFormatoR(ManagerFormatoR m) {
			if (m!=null) 
				torello = m.getTipoLinkFormatoR();
		}
		elimina void eliminaPerManagerFormatoR(ManagerFormatoR m) {
			if (m!=null)
				torello = null;
		}
	}
	
	public class Torello {
		private final String nome;
		private LinkedList<TipoLinkFormatoG> giallo;
		private LinkedList<TipoLinkFormatoR> rosso;
		private int MIN_MOLTEPLICITA = 1;
		public Torello(String n) {
			nome = n;
			giallo = new LinkedList<TipoLinkFormatoG>();
			rosso = new LinkedList<TipoLinkFormatoR>();
		}
		public String getNome() {
			return nome;
		}
		public void inserisciTipoLinkFormatoG(TipoLinkFormatoG t) {
			if (t!=null && t.getTorello()==this)
				ManagerFormatoG.inserisci(t);
		}
		public void eliminaTipoLinkFormatoG(TipoLinkFormatoG t) {
			if (t!=null && t.getTorello()==this)
				ManagerFormatoG.elimina(t);
		}
		public List<TipoLinkFormatoG> getGiallo() {
			if (giallo.size()<MIN_MOLTEPLICITA)
				throw new EccezioneMolteplicita("Molteplicita minima violata")
			return (List<TipoLinkFormatoG>) giallo.clone();
		}
		public int getMinMolteplicita() {
			return MIN_MOLTEPLICITA;
		}
		public void inserisciPerManagerFormatoG(ManagerFormatoG m) {
			if (m!=null) 
				giallo.add(m.getGiallo());
		}
		public void inserisciPerManagerFormatoG(ManagerFormatoG m) {
			if (m!=null) 
				giallo.remove(m.getGiallo());
		}
		public void inserisciTipoLinkFormatoR(TipoLinkFormatoR t) {
		if (t!=null && t.getTorello()==this)
			ManagerFormatoR.inserisci(t);
		}
		public void eliminaTipoLinkFormatoR(TipoLinkFormatoR t) {
			if (t!=null && t.getTorello()==this)
				ManagerFormatoR.elimina(t);
		}
		public List<TipoLinkFormatoR> getRosso() {
			if (rosso.size()<MIN_MOLTEPLICITA)
				throw new EccezioneMolteplicita("Molteplicita minima violata")
			return (List<TipoLinkFormatoR>) rosso.clone();
		}
		public int getMinMolteplicita() {
			return MIN_MOLTEPLICITA;
		}
		public void inserisciPerManagerFormatoR(ManagerFormatoR m) {
			if (m!=null) 
				rosso.add(m.getRosso());
		}
		public void inserisciPerManagerFormatoR(ManagerFormatoR m) {
			if (m!=null) 
				rosso.remove(m.getRosso());
		}
	}
	
	public class ManagerFormatoG {
		private TipoLinkFormatoG link;
		private ManagerFormatoG(TipoLinkFormatoG t) {
			link=t;
		}
		public static void inserisci(TipoLinkFormatoG t) {
			if (t!=null) {
				ManagerFormatoG m = new ManagerFormatoG(t);
				t.getGiallo().inserisciPerManagerFormatoG(m);
				t.getTorello().inserisciPerManagerFormatoG(m);
			}
		}
		public static void elimina(TipoLinkFormatoG t) {
			if (t!=null) {
				ManagerFormatoG m = new ManagerFormatoG(t);
				t.getGiallo().eliminaPerManagerFormatoG(m);
				t.getTorello().eliminaPerManagerFormatoG(m);
			}
		}
		public TipoLinkFormatoG getTipoLinkFormatoG() {
			return link;
		}
	}
	
	public class ManagerFormatoR {
		private TipoLinkFormatoR link;
		private ManagerFormatoR(TipoLinkFormatoR t) {
			link=t;
		}
		public static void inserisci(TipoLinkFormatoR t) {
			if (t!=null && t.getTorello().getTipoLinkFormatoR==null) {
				ManagerFormatoR m = new ManagerFormatoR(t);
				t.getRosso().inserisciPerManagerFormatoR(m);
				t.getTorello().inserisciPerManagerFormatoR(m);
			}
		}
		public static void elimina(TipoLinkFormatoR t) {
			if (t!=null && t.getTorello().getTipoLinkFormatoR().equals(t)) {
				ManagerFormatoG m = new ManagerFormatoG(t);
				t.getRosso().eliminaPerManagerFormatoR(m);
				t.getTorello().eliminaPerManagerFormatoR(m);
			}
		}
		public TipoLinkFormatoR getTipoLinkFormatoR() {
			return link;
		}
	}
	
	public class EccezioneMolteplicita extends Exception {
		private String messaggio;
		public EccezioneMolteplicita(String m) {
			messaggio = m;
		}
		public String toString() {
			reuturn m;
		} 
	}
	
	public class EccezionePrecondizioni extends Exception {
		private String messaggio;
		public EccezioneMolteplicita(String m) {
			messaggio = m;
		}
		public EccezioneMolteplicita() {
			messaggio = "Si è verificata una violazione di precondizioni";
		}
		public String toString() {
			reuturn m;
		} 
	}
	
	public class TipoLinkFormatoG {
		private final Giallo giallo;
		private final Torello torello;
		public TipoLinkFormatoG(Giallo g, Torello t) throws EccezionePrecondizione {
			if (g=null || t==null) 
				throw new EccezionePrecondizione("Gli oggetti devono essere inizializzati");
			giallo = g;
			torello = t;
		}
		public Giallo getGiallo() {
			return giallo;
		}
		public Torello getTorello() {
			return torello;
		}
		public boolean equals(Object o) {
			if (o!=null && getClass().equals(o.getClass())) {
				TipoLinkFormatoG t = (TipoLinkFormatoG) o;
				return t.getGiallo()==giallo && t.getTorello()==torello;
			}
			else 
				return false;
		}
		public int hashCode() {
			return giallo.hashCode() + torello.hashCode();
		}
	}
	
	public class TipoLinkFormatoR {
		private final Rosso rosso;
		private final Torello torello;
		public TipoLinkFormatoG(Rosso r, Torello t) throws EccezionePrecondizione {
			if (g=null || r==null) 
				throw new EccezionePrecondizione("Gli oggetti devono essere inizializzati");
			rosso = r;
			torello = t;
		}
		public Giallo getRosso() {
			return rosso;
		}
		public Torello getTorello() {
			return torello;
		}
		public boolean equals(Object o) {
			if (o!=null && getClass().equals(o.getClass())) {
				TipoLinkFormatoG t = (TipoLinkFormatoG) o;
				return t.getRosso()==rosso && t.getTorello()==torello;
			}
			else 
				return false;
		}
		public int hashCode() {
			return rosso.hashCode() + torello.hashCode();
		}
	}
}
```

Sulla parte del diagramma degli Stati e Transizioni otteniamo il seguente schema di Progetto:
![[Pasted image 20230710154948.png]]
nella parte scritta del testo vi era la seguente frase: "Il giocatore può essere modificato solo quando è in gioco" questo va ad aggiungere delle condizioni nella classe di giocatore, e fa capire che non tutto è final, infatti la classe diventa:
``` java
public abstract class Giocatore {
		private final String nome;
		private String avatar;
		public Giocatore(String n, String a) {
			nome = n;
			avatar = a;
		}
		public String getNome() {
			return nome;
		}
		public String getAvatar() {
			return avatar;
		}
		public void setAvatar(String a) {
			if (statocorrente != Stato.NONINGIOCO)
				throw new RunTimeException("Non si può modificare il giocatore se non è in gioco");
			avatar = a;
		}
		public String toString() {
			return nome + ' ' + avatar;
		}
	}
```
sulle richieste va inserita anche la specifica Stati e Transizioni


Diagramma delle attività:
![[Pasted image 20230710160752.png]]
per quando richiede il compito lo schema va arricchito con la specifica di:
- Attività atomica di inserimento dei giocatori nel torello, motivando le scelte effettuate
- Attività complesse
Nella parte di realizzazione bisogna anche fare:
- Attività principale
- Attività atomica di inserimento dei giocatori nel torello

```
Inizio Specifica Attività Atomica
InserisciInTorello(t:Torello, isr:Insieme<GiocatoreRosso>, isg:Insime<GiocatoreGiallo>)
	Pre: isr isNotEmpty() AND isg isNotEmpty()
	Post: ForAll gr in isr: t e gr sono collegati da un TipoLinkFormatoR AND
			 ForAll gs in iss: t e gs sono collegati da un TipoLinkFormatoG
FineSpecifica
```

```
Inizio Specifica Attività Principale (t:Torello)
	Variabili di processo: giocatoriRossi: Insieme<GiocatoreRosso>, giocatoriGialli: Iniseme<GiocatoreGiallo>
	InizioProcesso:
		LeggiGiocatori(giocatoriRossi, giocatoriGialli)
		InserisciInTorello(giocatoriRossi, giocatoriGialli, t)
		fork {
			thread t1: {Gioca(t)}
			thread t2: {AttendiComando();}
		}
		join t1,t2
	FineProcesso
FineSpecifica
```
