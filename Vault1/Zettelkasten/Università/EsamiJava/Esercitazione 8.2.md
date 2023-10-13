Progetto
![[Pasted image 20230709101731.png]]

Realizzazione

```java
public class Localita {
	private final String nome;
	private final String indirizzo;
	public Localita(String nome, String indirizzo) {
		this.nome = nome;
		this.indirizzo = indirizzo;
	}
	public String getNome() {return this.nome;}
	public String getIndirizzo() {return this.indirizzo;}
	public String toString() {return this.nome + ' ' + this.indirizzo;}
}
public class Ente {
	private final String codice;
	private final String nome;
	public Ente(String codice, String nome) {
		this.codice = codice;
		this.nome = nome;
	}
	public String getCodice() {return this.codice;}
	public String getNome() {return this.nome;}
	public String toString() {return this.codice + ' ' + this.nome;}
}
// versione mia, sbagliata
public class AziendaPubblica extends Azienda {
	private Ente ente;
	public AziendaPubblica(String nome, String descrizione, Ente ente) {
		super(nome, descrizione);
		this.ente = ente;
	}
	public getEnte() throws EccezioneMolteplicita {
		if (ente==null)
			throw EccezioneMolteplicita("Molteplicità min/max violata");
		return this.ente;
	}
	public void inserisciEnte(Ente e) {
		if (e!=null)
			this.ente = e;
	}
	public String toString() {return super.toString() + " " + this.ente;}
}
// versione prof, corretta
public class AziendaPubblica extends Azienda {
	private Ente ente;
	public AziendaPubblica(String nome, String descrizione) {
		super(nome, descrizione);
		this.ente = ente;
	}
	public getEnte() throws EccezioneMolteplicita {
		if (ente==null)
			throw EccezioneMolteplicita("Molteplicità min/max violata");
		return this.ente;
	}
	public void inserisciEnte(Ente e) {
		if (e!=null)
			this.ente = e;
	}
	public String toString() {return super.toString() + " " + this.ente;}
}
public class AziendaPrivata extends Azienda{
	private float capitaleSociale;
	public AziendaPrivata(String nome, String cognome, float capitaleSociale) {
		super(nome, cognome);
		this.capitaleSociale = capitaleSociale;
	}
	public getCapitaleSociale() {
		return this.capitaleSociale;
	}
	public void setCapitaleSociale(float capitaleSociale) {
		this.capitaleSociale = capitaleSociale;
	}
	public String toString() {
		return super.toString() + ' ' + this.capitaleSociale;
	}
}
// errore grave, dove avendo accorpato localita ho comunque creato un tipolink e che ha reso inutile accorpare
public abstract class Azienda {
	private final String nome;
	private final String descrizione;
	private HashSet<TipoLinkSede> sede;
	private HashSet<TipoLinkControlla> controlla;
	public Azienda(String nome, String descrizione) {
		this.nome = nome;
		this.descrizione = descrizione;
		sede = new HashSet<TipoLinkSede>();
	}
	public String getNome() {
		return this.nome;
	}
	public String getDescrizione() {
		return this.descrizione;
	}
	public Set<TipoLinkSede> getSede() {
		if (sede.size()<1)
			throw new EccezioneMolteplicita("Molteplicita minima violata");
		return (HashSet<TipoLinkSede) sede.clone();
	}
	public void inserisciLinkSede(TipoLinkLocalita tll) {
		if (tll != null)
			sede.add(tll); 
	}
	public void eliminaLinkSede(TipoLinkLocalita tll) {
		if (tll != null)
			sede.remove(tll);
	}
	public void inserisciLinkControlla(TipoLinkControlla tlc) {
		if (tlc != null && tlc.getAzienda() == this)
			ManagerControlla.inserisci(tlc);
	}
	public void eliminaLinkControlla(TipoLinkControlla tlc) {
		if (tlc != null && tlc.getAzionda() == this)
			ManagerControlla.elimina(tlc);
	}
	public void inserisciPerManager(ManagerControlla mc) {
		if (mc!=null)
			controlla.add(mc.getLink());
	}
	public void eliminaPerManager(ManagerControlla mc) {
		if (mc!=null)
			controlla.remove(mc.getLink());
	}
}
// versione del prof
public abstract class Azienda {
  protected final String nome;
  protected final String descrizione;
  protected HashSet<Localita> sede;
  private final int MOLT_MIN_SEDE = 1;
  protected HashSet<TipoLinkControlla> controllata; // le aziende controllate da this
  protected TipoLinkControlla controllante; // l'azienda controllante (l'azienda che controlla this)
  protected Azienda(String nome, String descrizione) {
    this.nome = nome;
    this.descrizione = descrizione;
    sede = new HashSet<Localita>();
    controllata = new HashSet<TipoLinkControlla>();
    controllante = null;
  }
  public String getNome() {
    return nome;
  }
  public String getDescrizione() {
    return descrizione;
  }
  public void inserisciLinkSede(Localita l) {
    if (l != null)
      sede.add(l);
  }
  public void eliminaLinkSede(Localita l) {
    if (l != null)
      sede.remove(l);
  }
  public Set<Localita> getLinkSede() throws EccezioneMolteplicita {
    if (sede.size() < MOLT_MIN_SEDE)
      throw new EccezioneMolteplicita("Molteplicita' minima violata");
    return (HashSet<Localita>) sede.clone();
  }
  public void inserisciLinkControllante(TipoLinkControlla c) {
    if (c != null && c.getControllata() == this) {
      ManagerControlla.inserisci(c);
    }
  }
  public void eliminaLinkControllante(TipoLinkControlla c) {
    if (c != null && c.getControllata() == this) {
      ManagerControlla.elimina(c);
    }
  }
  public TipoLinkControlla getLinkControllante() {
    return controllante;
  }
  public void inserisciLinkControllata(TipoLinkControlla c) {
    if (c != null && c.getControllante() == this) {
      ManagerControlla.inserisci(c);
    }
  }
  public void eliminaLinkControllata(TipoLinkControlla c) {
    if (c != null && c.getControllante() == this) {
      ManagerControlla.elimina(c);
    }
  }
  public Set<TipoLinkControlla> getLinkControllata() {
    return (HashSet<TipoLinkControlla>) controllata.clone();
  }
  public void inserisciControllantePerManagerControlla(ManagerControlla a) {
    if (a != null) {
      controllante = a.getLink();
    }
  }
  public void eliminaControllantePerManagerControlla(ManagerControlla a) {
    if (a != null) {
      controllante = null;
    }
  }
  public void inserisciControllataPerManagerControlla(ManagerControlla a) {
    if (a != null) {
      controllata.add(a.getLink());
    }
  }
  public void eliminaControllataPerManagerControlla(ManagerControlla a) {
    if (a != null) {
      controllata.remove(a.getLink());
    }
  }
}
public class TipoLinkSede {
	private final Azienda azienda;
	private final Localita localita;
	public TipoLinkSede(Azienda azienda, Localita localita) {
		if (azienda == null || localita == null) 
			throw new EccezionePrecondizioni("Gli oggetti devono essere inizializzati");
		this.azienda = azienda;
		this.localita = localita;
	}
	public Azienda getAzienda() {
		return this.azienda;
	}
	public Localita getLocalita() {
		if (localita.size()<1)
			throw new EccezioneMolteplicita("Molteplicita minima violata")
		return this.localita;
	}
	@Override
	public boolean equals(Object o) {
		if (o!=null && getClass().equals(o.getClass())) {
			TipoLinkSede tls = (TipoLinkSede) o;
			return tls.getAzienda() == this.azienda && tls.getLocalita() == this.localita;
		}
		else
			return false;
	}
	@Override
	public int hashCode() {
		return azienda.hashCode() + localita.hashCode();
	}
	public String toString() {
		return this.azienda + ' ' + this.localita;
	}
}
public class TipoLinkControlla {
	private Azienda controllante;
	private Azienda controllata;
	public TipoLinkControlla(Azienda controllante, Azienda controllata) {
		if (controllante==null || controllata == null) 
			throw new EccezioniPrecondizioni("Gli oggetti devono essere inizializzati");
		this.controllante = controllante;
		this.controllata = controllata;
	}
	public Azienda getControllante() {
		if (controllante.size()>1)
			throw new EccezioneMolteplicita("Molteplicita massima violata");
		return this.controllante;
	}
	public Azienda getControllata() {
		return this.controllata;
	}
	@Override
	public boolean equals(Object o) {
		if (o!=null && getClass().equals(o.getClass)) {
			TipoLinkControlla tlc = (TipoLinkControlla) o;
			return tlc.getControllata() == this.controllante && tlc.getControllante() == this.controllante;
		}
		else
			return false;
	}
	@Override
	public int hashCode() {
		return controllante.hashCode + controllata.hashCode;
	}
	@Override
	public String toString() {
		return this.controllante + ' ' + this.controllata;
	}
}
public class EccezionePrecondizioni extends Exception {
	private String messaggio;
	public EccezionePrecondizioni(String messaggio) {
		this.messaggio = messaggio;
	}
	public String toString() {
		return this.messaggio;
	}
}
public class EccezioneMolteplicita extends Exception {
	private String messaggio;
	public EccezionePrecondizioni(String messaggio) {
		this.messaggio = messaggio;
	}
	public String toString() {
		return this.messaggio;
	}
}
public class ManagerControlla {
	private TipoLinkControlla link;
	private ManagerControlla(TipoLinkControlla link) {
		this.link = link;
	}
	public static void inserisci(TipoLinkControlla tlc) {
		if (tlc != null) {
			ManagerControlla mc = new ManagerControlla(tlc);
			tlc.getControllata().inserisciPerManagerControlla(mc);
			tlc.getControllante().inserisciPerManagerControlla(mc);
		}
	}
	public static void elimina(TipoLinkControlla tlc) {
		if (tlc!=null)
			ManagerControlla mc = new ManagerControlla(tlc);
			tlc.getControllata().eliminaPerManagerControlla(mc);
			tlc.getControllante().eliminaPerManagerControlla(mc);
	}
	public TipoLinkControlla getLink() {
		return this.link;
	}
}
```
