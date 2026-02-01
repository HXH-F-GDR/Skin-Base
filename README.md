Questa skin gestisce i valori frequenti usando la pseudo-classe :root.

Come funziona?

È una sorta di legenda che assegna un "soprannome" ai valori comuni (in questo caso i colori della palette e i due font principali).

Facciamo degli esempi concreti e prendiamo ad esempio un piccolissimo root con soli due colori codificati all'interno, bianco e nero. Il nostro root si presenterà così:


    :root{--primo: #FFF;

     --secondo: #000;}


Quando voglio richiamare un elemento all'interno del root, devo metterlo all'interno di var(). Quindi facciamo finta che io abbia queste voci nel css:


    .classe1 {background:#fff; border:3px solid #000; color:#000}

    .classe2 {background:#000; border:10px solid #fff; color:#fff}


Utilizzando :root diventeranno:


    .classe1 {background: var(--primo); border: 3px solid var(--secondo); color: var(--secondo)}

    .classe2 {background: var(--secondo); border: 10px solid var(--primo); color: var(--primo)}


Perché questo sistema è utile? Inanzitutto è più diretto che dover inserire tutte le volte il codice HEX dei colori, basta farlo una singola volta nel root, poi questo permette modifiche globali: se un giorno dovessi decidere che non voglio più che le parti nere del codice siano nere, ma decido di volerle grigio scuro, non dovrò cercare e sostituire ogni singolo #000 nel codice, ma mi basterà sostituire una sola volta il colore nel root e questo si applicherà a tutti i valori del css.

Quindi, concretamente, per passare da nero a grigio scuro, il root passerà da essere:

    :root{--primo: #FFF;
     --secondo: #000;}

 Ad essere, ad esempio:

     :root{--primo: #FFF;
     --secondo: #151515;}

 La seconda particolarità della skin è l'utilizzo di 
          
    * {box-sizing:border-box}
     

Il box-sizing predefinito nel web è box-sizing:content-box, ma in realtà moltissimi siti usano al suo posto border-box perché più semplice e coerente.

Come funzionano?

content-box vuol dire che se un elemento ha delle dimensioni predefinite, quelle dimensioni fanno riferimento SOLO al contenuto dell'elemento, non tenendo conto delle dimensioni dei border, dei margin e dei padding. Questo vuol dire che se in un div ho impostato width:100px e height:100px e dentro quel div metto un'immagine 100x100 che, però, ha padding:2px, border:5px e margin:3px, le dimensioni totali reali di quel div saranno width:120px e height:120px. Questo perché? Perché la larghezza sarà: 100px(valore iniziale)+2px(padding destro)+2px(padding sinistro)+5px(bordo destro)+5px(bordo sinistro)+3px(margin destro)+3px(margin sinistro)=120px, mentre l'altezza sarà: 100px(valore iniziale)+2px(padding alto)+2px(padding basso)+5px(bordo alto)+5px(bordo basso)+3px(margin alto)+3px(margin basso)=120px.
Tutto questo rende il calcolo delle dimensioni e gli allineamenti tra elementi difficile e macchinoso.

border-box risolve questa situazione, facendo in modo che se viene dichiarata una dimensione, quella dimensione è complessiva di padding, border e margin, a costo di ridurre le dimensioni del contenuto.
Nell'esempio di prima, del div 100x100 contenente un'immagine 100x100, se l'immagine ha padding:2px, border:5px e margin:3px, l'immagine verrà ridimensionata ad 80x80 per fare in modo che tutto il contenuto del div rientri nei 100x100 massimi dichiarati.
