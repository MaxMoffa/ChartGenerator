
# ChartGenerator

La repository *ChartGenerator* contiene i file del sito web omonimo che permette la creazione di grafici per qualsiasi uso (Es. Presentazioni, Documenti, ...)

### Come funziona?
Per generare un grafico attraverso "Chart Generator" bisogna creare un file in formato '.csv' con una struttura specifica, ovvero: la prima riga deve contenere le info relative alle colonne, poi le successive righe verranno selezionate come singoli 'dataset' (in pratica tutti gli elementi su una riga rappresentano l'andamento di un valore)


Ecco un esempio di file in formato '.csv' valido: [Esempio.csv](https://maxmoffa.github.io/ChartGenerator/public/media/files/Esempio.csv)

### Sviluppo
Il sito web è stato costruito con l'ausilio di un framework di ultima generazione, ovvero *Svelte*

Altre info:
1. [Chart.js](https://www.chartjs.org/) per i grafici
2. [Svelte-grid](https://svelte-grid.now.sh/) per gestire la griglia della home
3. [Google Fonts](https://fonts.google.com/) per i font utilizzati
