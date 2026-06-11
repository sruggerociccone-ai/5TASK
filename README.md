# 5TASK
5 TASK CON LE RISPOSTE
import csv
import os


# TASK 5 - FUNZIONI

def leggi_brani(PERCORSO):
    
    BRANI = []

    with open(PERCORSO, mode="r", encoding="utf-8") as FILE:
        LETTORE = csv.DictReader(FILE)

        for RIGA in LETTORE:
            BRANI.append(RIGA)

    return BRANI


def conta_per_genere(BRANI):
    
    CONTEGGI = {}

    for BRANO in BRANI:

        GENERE = BRANO.get("track_genre") or "Sconosciuto"

        if GENERE not in CONTEGGI:
            CONTEGGI[GENERE] = 0

        CONTEGGI[GENERE] += 1

    return CONTEGGI




CARTELLA = os.path.dirname(os.path.abspath(__file__))
NOME_FILE = os.path.join(CARTELLA, "dataset.csv")

BRANI_TOT = leggi_brani(NOME_FILE)

print(f"Righe lette con CSV: {len(BRANI_TOT)}")


# TASK 1

BRANO_VIRGOLA = None

for BRANO in BRANI_TOT:

    TITOLO = BRANO.get("track_name") or ""

    if "," in TITOLO:
        BRANO_VIRGOLA = BRANO
        break

if BRANO_VIRGOLA:

    print("Esempio titolo con virgola corretto:")
    print(BRANO_VIRGOLA["track_name"])
    print(BRANO_VIRGOLA["artists"])



# TASK 2

RIGHE_CSV = len(BRANI_TOT)
RIGHE_SPLIT = 0  

print(f"Righe CSV: {RIGHE_CSV}")

if RIGHE_SPLIT > 0:

    DIFFERENZA = RIGHE_CSV - RIGHE_SPLIT

    print(f"Righe split (ieri): {RIGHE_SPLIT}")
    print(f"Differenza: {DIFFERENZA}")

else:

    print("Inserisci il valore di ieri per confrontare i risultati.")


# TASK 3

CONTEGGI = conta_per_genere(BRANI_TOT)

ORDINATI = sorted(
    CONTEGGI.items(),
    key=lambda X: X[1],
    reverse=True
)

for GENERE, NUMERO in ORDINATI:
    print(GENERE, NUMERO)


# TASK 4

BRANO_TOP = None
MAX_POP = -1
RIGHE_ERRATE = 0

for BRANO in BRANI_TOT:

    VAL = BRANO.get("popularity") or ""

    try:
        POP = int(float(VAL))
    except (ValueError, TypeError):
        RIGHE_ERRATE += 1
        continue

    if POP > MAX_POP:
        MAX_POP = POP
        BRANO_TOP = BRANO

print("\nBrano più popolare:")
print(BRANO_TOP["track_name"])
print(BRANO_TOP["artists"])
print(MAX_POP)

print("Righe errate:", RIGHE_ERRATE)


# TASK 5

print("Funzioni utilizzate correttamente.")


# TASK 6

TITOLI_UNICI = set()

for BRANO in BRANI_TOT:

    TITOLO = (BRANO.get("track_name") or "").strip()

    if TITOLO:
        TITOLI_UNICI.add(TITOLO)

UNICI = len(TITOLI_UNICI)
TOTALI = len(BRANI_TOT)



RISPOSTE

RISPOSTA TASK 1
il metodo csv gestisce meglio la virgola tenedola all'interno delle virgolette rispetto allo split che poi va a creare colonne in più
RISPOSTA TASK 2

Con split alcune righe venivano sbagliate perché le virgole facevano sbaliare mentre con  csv.DictReader invece tutte le righe vengono lette bene

RISPOSTA TASK 3

Il risultato non cambia dato che in realtà la differenza tra csv reader e split è qualitativa perché questo metodo non faceva cambiare il numero di righe ma mandava a capo le parole spezzandole a metà con all'interno delle virgole

RISPOSTA TASK 5

le funzioni ci aiutano a riordinare benere il codice e a facilitarne e per fare analisi di tipo diverso senza riscrivere tutto 

RISPSOTA TASK 6

si la statistica si sta gonfiando perché un brano compare in più geneir e quindi questo fa aumentare i dati e seconod me non è giusto perché si andrà a misurare di più rieptto a quello che si deve.

print("\nTotale righe:", TOTALI)
print("Titoli unici:", UNICI)
print("Duplicati:", TOTALI - UNICI)
