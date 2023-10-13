Diagramma delle Classi
![[Pasted image 20230708171453.png]]

Codice:
```java
package progetto.icona;
public class  Icona{
	private final String icona;
	private String immagine;
	public Icona(String icona, String immagine) {
		this.icona = icona;
		this.immagine = immagine;
	}
	public String getIcona() {return this.icona;}
	public String getImmagine() {return this.immagine;}
	public void setImmagine(String immagine) {this.immagine = immagine;}
	@Override
	public String toString() {return this.icona+' '+this.immagine;}
} 

package progetto.displayArea
public class displayArea() {
	private final String posizione;
	private final String background;
	public displayArea(String posizione, String background) {
		this.posizione = posizione;
		this.background = background;
	}
	public String getPosizione() {return this.posizione;}
	public String getBackground() {return this.background;}
	@Override
	public String toString() {return this.posizione + ' ' + this.background;}
}

package progetto.applicazione;
public class Applicazione {
	private final String nome;
	private final String nomefile;
	public Applicazione(String nome, String nomefile) {
		this.nome = nome;
		this.nomefile = nomefile;
	}
	public getNome() {return this.nome;}
	public getNomeFile() {return this.nomefile;}
	@Override
	public String toString() {return this.nome + ' ' + this.nomefile}
}

// animazione ha responsabilità su DisplayArea, posso mettere coinvolge come istanza di Animazione
// animazione ha responsabilità su IconaAttiva, posso mettere mostra come istanza di Animazione, ma visto che c'e responsabilità doppia mettiamo un manager e TipoLink
// visto che è posso avere diversi displayArea devo implementare un HashSet >= 1, e le relative funzioni
package progetto.animazione;
import progetto.displayArea.DisplayArea;
import java.util.HashSet;
public class Animazione {
	private final String link;
	private HashSet<DisplayArea> coinvolge;
	private HashSet<TipoLinkMostra> mostra;
	public Animazione(String link) {
		this.link = link;
		this.coinvolge = new HashSet<DisplayArea>();
	}
	public String getLink() {return this.link;}
	public void inserisciLinkCoinvolge(DisplayArea da) {
		if (da != null)
			coinvolge.add(da);
	}
	public void eliminaLinkCoinvolge(DisplayArea da) {
		if (da != null)
			coinvolge.remove(da);
	}
	public void inserisciLinkMostra(TipoLinkMostra tlm) {
		if (tlm != null && tlm.getAnimazione() == this)
			ManageMostra.inserisci(tlm);
	}
	public void eliminaLinkMostra(TipoLinkMostra tlm) {
		if (tlm != null && tlm.getAnimazione() == this)
			ManagerMostra.elimina(tlm);
	}
	public void inserisciPerManagerMostra(ManagerMostra a) {
		if (a!=null) 
			mostra.add(a.geLink());
	}
	public void eliminaPerManagerMostra(ManagerMostra a) {
		if (a!=null)
			mostra.remove(a.getLink());
	}
	public Set<DisplayArea> getLinkCoinvolge() {
		if (coinvolge.size() < 1)
			throw new EccezioneMolteplicita("Cardinalità minima violata");
		return (HashSet<DisplayArea>) coinvolge.clone();
	}
	public Set<TipoLinkMostra> getLinkMostra() {
		return (HashSet<TipoLinkMostra>) mostra.clone();
	}
}

public class IconaAttiva extends Icona{
	private final String suonoAlClick;
	private Applicazione applicazione;
	private LinkedList<TipoLinkMostra> mostra;
	private HashSet<TipoLinkOccupa> occupa;
	public IconaAttiva(String codice, String immagine, String suonoAlClick, Applicazione applicazione) {
		super(codice, immagine);
		this.suonoAlClick = suonoAlClick;
		this.applicazione = applicazione;
		mostra = new LinkedList<TipoLinkMostra>();
		occupa = new HashSet<TipoLinkOccupa>();
	}
	public String getSuonoAlClick() {return this.suonoAlClick;}
	public Applicazione getApplicazione() throws EccezioneMolteplicita{
		if (a==null)
			throw new EccezioneMolteplicita("Molteplicita min/max violate");
		return this.applicazione;
	}
	public List<TipoLinkMostra> getLinkMostra() throws EccezioneMolteplicita{
		if (mostra.size() <1)
			throw new EccezioneMolteplicita("Molteplicità minima violata");
		return (LinkedList<TipoLinkMostra>) mostra.clone();
	}
	public Set<TipoLinkOccupa> getLinkOccupa() throws EccezioneMolteplicita{
		if(occupa.size()<1)
			throw new EccezioneMolteplicita("Molteplicità minima violata");
		return (HashSet<TipoLinkOccupa>) occupa.clone();
	}
	public void inserisciApplicazione(Applicazione a) {
		if (a!=null)
			this.applicazione = a;
	}
	public void inserisciLinkOccupa(TipoLinkOccupa tlo) {
		if (tlo!=null && tlo.getIconaAttiva() == this)
			occupa.add(tlo);
	}
	public void eliminaLinkOccupa(TipoLinkOccupa tlo) {
		if (tlo!=null && tlo.getIconaAttiva() == this)
			occupa.remove(tlo);
	}
	public void inserisciLinkMostra(TipoLinkMostra tlm) {
		if (tlm != null && tlm.getIconaAttiva() == this)
			ManagerMostra.inserisci(tlm);
	}
	public void eliminaLinkMostra(TipoLinkMostra tlm) {
		if (tlm != null && tlm.getIconaAttiva() == this)
			ManagerMostra.elimina(tlm);
	}
	// ho aggiunto un controllo perche essendo una linkedlista devo essere sicuro non ci sia gia l'elemento
	public void inserisciPerManagerMostra(ManagerMostra mm) {
		if (mm!=null && !mostra.contains(mm.getLink()))
			mostra.add(mm.getLink());
	}
	public void eliminaPerManagerMostra(ManagerMostra mm) {
		if (mm!=null)
			mostra.remove(mm.getLink());
	}
}

public class ManagerMostra {
	private TipoLinkMostra link;
	private ManagerMostra(TipoLinkMostra) {
		this.link = link;
	}
	public static void inserisci(TipoLinkMostra y) {
		if (y != null) {
			ManagerMostra mm = new ManagerMostra(y);
			y.getAnimazione().inserisciPerManagerMostra(mm);
			y.getIconaAttiva().inserisciPerManagerMostra(mm);
		}
	}
	public static void elimina(TipoLinkMostra y) {
		if (y != null) {
			ManagerMostra mm = new ManagerMostra(y);
			y.getAnimazione().eliminaPerManagerMostra(mm);
			y.getIconaAttiva().eliminaPerManagerMostra(mm);
		}
	}
	public TipoLinkMostra getLink() {
		return link;
	}
}

public class EccezioneMolteplicita extends Exception {
	public EccezioneMolteplicita(String messaggio) {
		super(messaggio);
	}
}

public class TipoLinkMostra {
	private final IconaAttiva iconaAttiva;
	private final Animazione animazione;
	public TipoLinkMostra(IconaAttiva iconaAttiva, Animazione animazione) {
		if (iconaAttiva == null || animazione == null)
			throw new EccezionePrecondizioni("Gli oggetti devono essere inizializzati");
		this.iconaAttiva = iconaAttiva;
		this.animazione = animazione;
	}
	public IconaAttiva getIconaAttiva() {return this.iconaAttiva;}
	public Animazione getAnimazione() {return this.animazione;}
	@Override
	public boolean equals(Object o) {
		if (o!=null && getClass.equals(o.getClass)) {
			TipoLinkMostra m = (TipoLinkMostra) o;
			return m.iconaAttiva == this.iconaAttiva && m.animazione == this.animazione;
		}
		else
			return false;
	}
	@Override
	public int hashCode() {return iconaAttiva.hashCode() + animazione.hashCode()}
	@Override
	public String toString() {return this.iconaAttiva + ' ' + this.animazione}
}

public class TipoLinkOccupa {
	private final IconaAttiva iconaAttiva;
	private final DisplayArea displayArea;
	private final boolean interamente;
	public TipoLinkOccupa(IconaAttiva iconaAttiva, DisplayArea displayArea, boolean interamente) {
		if (iconaAttiva==null || displayArea==null) {
			throw new EccezionePrecondizione("Gli oggetti devono essere inzializzati");
		}
		this.iconaAttiva = iconaAttiva;
		this.displayArea = displayArea;
		this.interamente = interamente;
	}
	public IconaAttiva getIconaAttiva() {return this.iconaAttiva;}
	public DisplayArea getDisplayArea() {return this.displayArea;}
	public boolean getInteramnte() {return this.interamente;}
	@Override
	public boolean equals(Object o) {
		if (o!=null && getClass().equals(o.getClass())) {
			TipoLinkOccupa occ = (TipoLinkOccupa) o;
			return occ.iconaAttiva == this.iconaAttiva && occ.displayArea == this.displayArea;
		}
		else
			return false;
	}
	@Override
	public int hashSet() {return iconaAttiva.hashSet() + displayArea.hashSet();}
	@Override
	public String toString() {return this.iconaAttiva + ' ' + this.displayArea + ' ' + this.interamente;}
}

public class EccezionePrecondizioni extends Exception {
	public EccezioniPrecondizioni(String messaggio) {
		super(messaggio);
	}
}

// da completare
public final class OperazioniUtente {
	private OperazioniUtente() {}
	public static List<Animazione> invertiAnimazioni (IconaAttiva ia) {
		return null;
	}
	public static Set<IconaAttiva> chiMostra(Animazione e) {
		return null;
	}
}

```