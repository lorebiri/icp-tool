# Deploy ICP Tool su GitHub Pages

## File da caricare nel repo `lorebiri/icp-tool`

```
lorebiri/icp-tool/
├── index.html              ← app web (con service worker + pulsanti download)
├── icp-tool.html           ← versione offline scaricabile dal sito
├── sw.js                   ← service worker (cache offline)
├── manifest.json           ← metadati PWA
└── ICP_Tool_Manuale.docx   ← manuale scaricabile dal sito
```

> I pulsanti "Scarica versione offline" e "Scarica manuale" nella welcome screen
> puntano rispettivamente a `./icp-tool.html` e `./ICP_Tool_Manuale.docx`.
> Devono essere presenti nel repo per funzionare.

---

## Prima volta (repo già esistente)

### 1. Vai sul repo
Apri https://github.com/lorebiri/icp-tool

### 2. Carica i file
Clicca **Add file → Upload files**, trascina tutti e 5 i file:
- `index.html`
- `icp-tool.html`
- `sw.js`
- `manifest.json`
- `ICP_Tool_Manuale.docx`

Poi clicca **Commit changes**.

### 3. Abilita GitHub Pages
- Vai su **Settings → Pages**
- In *Source* scegli **Deploy from a branch**
- Branch: `main`, cartella: `/ (root)`
- Clicca **Save**

### 4. Attendi il deploy
GitHub impiega ~1-2 minuti. Poi l'app è live su:

```
https://lorebiri.github.io/icp-tool/
```

---

## Aggiornamenti futuri

Ogni volta che modifichi l'app:

1. Vai su **Add file → Upload files** e carica il nuovo `index.html` (sovrascrive il precedente)
2. Se vuoi forzare il service worker a ricaricare la cache, apri `sw.js` e cambia la versione in cima:
   ```js
   const CACHE_NAME = 'icp-tool-v2';  // ← incrementa il numero
   ```

---

## Con Git da terminale (opzionale)

```bash
# Prima volta
git clone https://github.com/lorebiri/icp-tool.git
cd icp-tool
cp /percorso/output/index.html .
cp /percorso/output/sw.js .
cp /percorso/output/manifest.json .
git add .
git commit -m "Deploy ICP Tool"
git push

# Aggiornamenti
cp /percorso/nuovo/index.html .
git add index.html
git commit -m "Aggiornamento ICP Tool"
git push
```

---

## Verifica funzionamento offline

1. Apri l'app nel browser e aspetta il caricamento completo
2. Vai in **DevTools → Application → Service Workers** e verifica che sia attivo
3. Metti il browser offline (DevTools → Network → Offline)
4. Ricarica la pagina — deve funzionare ancora

---

## Note

- `localStorage` è per-dominio: i dati salvati su `lorebiri.github.io/icp-tool` sono separati da quelli della versione locale (doppio click su file)
- Il service worker fa cache dei file CDN (jsPDF) alla prima visita, quindi dopo la prima apertura online tutto funziona offline
- Per aggiungere il logo PNG ufficiale al posto dell'SVG: carica `logo.png` nel repo e sostituisci in `index.html` il `src` dell'img con `./logo.png`
