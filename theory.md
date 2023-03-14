
# memory management
esistono i costruttori ma non i distruttori siccome di questo si occupa il garbage collector

# attributi e metodi
Gli attributi costituiscono lo stato degli oggetti istanziati a partire dalla classe, il loro valore è diverso per ogni oggetto

I metodi definiscono il comportamento degli oggetti istanziati a partire dalla classe, il loro codice è lo stesso per ogni oggetto

# riferimenti
Le istanze di una classe si chiamano oggetti: ogni variabile il cui tipo sia una classe (o un’interfaccia) contiene un riferimento ad un oggetto

In Java, gli oggetti sono accessibili solo per riferimento
Ad ogni variabile di tipo riferimento può essere assegnato
il riferimento null

# passaggio parametri

I parametri il cui tipo sia uno dei tipi primitivi sono passati per copia
I parametri il cui tipo sia un tipo riferimento (classi, interfacce, array) sono passati per riferimento, ovvero per copia del riferimento
Quindi, gli oggetti sono sempre passati per riferimento
