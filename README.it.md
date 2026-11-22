# RF2 Server Manager

[English](README.md) · **Italiano** · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt.md)

**Scarica:** [ultima versione](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

**Sostieni il progetto:** [dona con PayPal](https://www.paypal.com/donate/?business=3T7ZTAXBQY3EN&no_recurring=0&item_name=Sostieni+Karma+TV%3A+progetti+e+canali+YouTube%2C+Instagram%2C+TikTok.+Support+my+projects+and+channels.+Grazie%21+Thanks%21&currency_code=EUR) – l'app è gratuita, ogni donazione aiuta a tenerla aggiornata.

---

Strumento per Windows che configura e avvia un server dedicato di RF2.
Non è un prodotto ufficiale e non è collegato a Studio 397 o Motorsport Games.

Al primo avvio l'app riconosce la lingua di Windows: italiano, inglese, spagnolo, francese, tedesco o portoghese. Le altre lingue diventano inglese. Il pulsante con la bandiera in alto a destra la cambia, e l'app ricorda la scelta.

## Cosa serve

- Windows 10 o 11 a 64 bit. .NET è già incluso nell'exe.
- Spazio su disco per il server e i contenuti.
- Microsoft Edge WebView2 Runtime, solo per il browser nella scheda Workshop. Senza, puoi incollare l'ID del Workshop a mano.

Il server dedicato e SteamCMD non sono inclusi: l'app può scaricarli da Valve e Steam con la configurazione guidata.

## Primo avvio

1. Avvia `RF2ServerManager.exe`. Non serve installarlo.
2. Se Windows mostra "PC protetto da Windows", scegli **Ulteriori informazioni** e poi **Esegui comunque**. Compare perché l'exe non ha una firma digitale.
3. Nella configurazione guidata scegli le cartelle di SteamCMD e del server, oppure lascia che l'app li scarichi.
4. Avvia il server una volta: crea i suoi file di configurazione. Se Windows chiede il permesso per il firewall, scegli **Consenti**.

## Aggiornamenti

All'avvio l'app guarda su GitHub se c'è una versione nuova. Se c'è, in fondo al menu a sinistra compare il riquadro **Aggiorna ora**. L'app la scarica, controlla la sua impronta SHA-256 e si riapre da sola; il server, se è acceso, resta acceso. Sotto il numero di versione, **Controlla aggiornamenti** ripete il controllo a mano. Se la cartella dell'app non è scrivibile (per esempio dentro Programmi), scarica la versione nuova dalla [pagina delle versioni](https://github.com/KarmaTV80/rf2-server-manager/releases).

## Contenuti che hai già nel gioco

Non serve riscaricarli né copiarli a mano. L'app cerca da sola la cartella del gioco, che puoi anche scegliere nel passo 1. Prepara. Nel passo 3. Contenuti premi **Aggiungi dal gioco**, seleziona auto e piste e premi **Copia nel server**. Il gioco viene solo letto.

In **Libreria** ogni contenuto mostra il suo stato: *Pronto*, *Da installare* oppure *Manca il pacchetto*, quando gli amici non possono scaricarlo. Il pulsante sulla riga fa la cosa giusta: installa, copia il pacchetto dal gioco oppure apre il Workshop sulla ricerca di quel contenuto. Auto e piste dell'evento si scelgono nel passo 4. Evento, con **Crea un nuovo evento**.

I contenuti installati nel gioco senza pacchetto `.rfcmp` (per esempio comprati da un sito) compaiono in fondo agli elenchi: di questi si copia nel server l'installazione, e potranno entrare solo i piloti che li hanno già, nella stessa versione.

I DLC ufficiali comprati funzionano sul server: l'app copia da sola il file di sblocco che il gioco prepara (`ServerUnlock.bin`). Gli aggiornamenti dei contenuti si applicano anche loro da soli.

## Giocare con altre persone

Sul router inoltra verso l'IP del PC:

| Porta | Protocollo | Uso |
|---|---|---|
| 54297 | TCP e UDP | Simulazione |
| 64297 | TCP | Scaricamento dei file da parte dei client |
| 64298 e 64299 | UDP | Steam: senza queste il server non compare nell'elenco del gioco |

**Non aprire mai le porte 5397 e 5398**: controllano il server e il gioco. Imposta sempre una password d'ingresso e una password admin diverse tra loro. Il pulsante **Controlla rete e porte** nel passo 10. Server ti aiuta nelle verifiche.

### CGNAT, doppio router e VPN

Se il tuo provider usa il CGNAT (un IP pubblico condiviso tra più clienti), aprire le porte sul router non serve: gli amici non raggiungono il server. Dalla versione 1.0.7 **Controlla rete e porte** ti avvisa quando trova un indirizzo CGNAT sulla strada verso internet. Puoi anche confrontare l'IP WAN mostrato nella pagina del router con l'IP pubblico mostrato dall'app: se sono diversi, sei dietro CGNAT o dietro un secondo router. In quel caso chiedi al provider un IP pubblico, oppure apri le porte su tutti e due i router. Le VPN (Hamachi, ZeroTier e simili) non sono gestite dall'app.

## Server sullo stesso PC del gioco

Un PC separato è la soluzione ideale, ma molti ne hanno uno solo, e l'app è fatta anche per questo caso:

- Il server dedicato è un programma separato: l'app lo installa con SteamCMD in una cartella sua, mai dentro quella del gioco.
- Gioco e server usano tutti e due la porta 5397 per la loro interfaccia web: prima di ogni avvio l'app sposta quella del server sulla 5398, così non si scontrano.
- Avviare il server mentre il gioco carica rallenta tutti e due: con **Avvia prima il gioco** l'app aspetta che il gioco sia al menu, poi avvia il server da sola.
- Per eventi grandi un PC separato resta meglio: il server non toglie risorse al gioco.

## Pacchetti e DLC a pagamento

- Gli amici scaricano auto, piste ed eventi solo dalla cartella `Packages` del server: ogni `.rfcmp` e `.rfmod` deve essere lì, altrimenti entrando ricevono un errore. La Libreria segna cosa manca (*Manca il pacchetto*) e può copiarlo dal gioco, e gli eventi creati con l'app mettono lì il loro `.rfmod` da soli.
- I DLC ufficiali a pagamento si aprono sul server solo con `ServerUnlock.bin`, che il gioco crea nella sua cartella `UserData` per i contenuti che possiedi. L'app lo copia nella cartella `UserData` del server prima di installare i contenuti e prima di ogni avvio. Se il server è su un altro PC, copia tu quel file, e di nuovo dopo aver comprato nuovi DLC.

## Anticheat

Nel passo 9. Chat e ping l'app può segnalare i piloti con giri o velocità impossibili e i salti da un punto all'altro della pista, confrontando ognuno con gli altri della stessa classe. Non scollega nessuno: avvisa e scrive tutto nel registro dei sospetti (`sospetti.log`), poi decide chi gestisce il server. Il server non vede dentro il PC dei piloti, quindi trova gli effetti dei trucchi, non i programmi.

## Dove sono i dati

- Impostazioni e registro: `%AppData%\RF2ServerManager`
- Password: solo nei file di configurazione del server, che le conserva in chiaro. Non finiscono nei profili.

## Segnalare un problema

Usa **Segnala** in alto a destra nell'app, oppure **Info → Segnala un problema** (dalla versione 1.0.6). L'app mostra il registro già senza nome utente di Windows, nomi dei piloti, Steam ID, indirizzi IP e messaggi della chat, lo salva in un file di testo e apre su GitHub il [modulo delle segnalazioni](https://github.com/KarmaTV80/rf2-server-manager/issues/new?template=segnalazione.yml): descrivi cosa è successo e allega il file. Le segnalazioni sono pubbliche e serve un account GitHub gratuito. Il pulsante **Apri cartella registro** è nel passo 1. Prepara.

## Limiti noti

- La creazione delle mod e l'installazione dei pacchetti guidano MAS2 e ModMgr in background, con le loro finestre nascoste: l'avanzamento si legge nel registro dell'app. Con "Avvia subito la sessione" anche la finestra del server parte ridotta a icona: si riapre dalla barra di Windows. Un aggiornamento di quegli strumenti può richiedere di adattare l'app.
- I contenuti a pagamento e i pacchetti ricopiati dal Workshop possono non installarsi: l'app mostra l'errore e ripulisce i file.
- Prove 2 non ha orario e durata propri nella configurazione del server.

## Condizioni d'uso

Gratuito, anche per campionati e leghe. Non è consentito modificarlo, decompilarlo, rivenderlo o distribuirlo da altri siti: condividi solo il link ufficiale. Testo completo in `LICENSE.txt` e nella finestra **Informazioni** dell'app.

Componenti di terze parti: FlaUI e Newtonsoft.Json (licenza MIT), Microsoft WebView2 SDK (licenza Microsoft), .NET (licenza MIT), caratteri Saira Extra Condensed e Barlow (SIL Open Font License, testi in `Licenze\`).
