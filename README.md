# Generator & Scanner QR Code

Am construit un generator și scanner de coduri QR hardcodat pentru versiunea 2 (25x25) și pentru nivelul L de corecție a erorilor (Low = 7%).
Acest proiect a fost realizat ca parte a unui task academic, în colaborare cu un coleg de grupă. Am dezvoltat un generator și scanner de coduri QR de tip 2, utilizând limbajul Python.
Pe parcursul acestui proiect, am învățat despre funcționarea codurilor QR și am dobândit abilități valoroase de colaborare în echipă, un skill esențial în industria IT.


**READER**

Am folosit funcții din biblioteca cv2 pentru a transforma o imagine cu un QR code într-o matrice numpy cu valori de 0 pentru un modul negru și 255 pentru un modul alb. Practic, funcția qr_to_matrix preia imaginea, o centrează, o împarte în 25x25 de pătrate egale și verifică dacă în fiecare pătrat este mai mult alb sau negru. Astfel, se construiește exact matricea cu care pot lucra, formată din 255 și 0.

Inițial, încerc să aflu tipul măștii folosindu-mă de cei 3 biți din formatul bits și de o hardcodare specifică fiecărei măști în parte.
După ce am aflat tipul măștii, efectuez un XOR între matricea de date și masca respectivă, obținând astfel matricea inițială (a XOR masca XOR masca = a).
Citesc din cod și decodific începând de la primul byte de conținut și mă opresc când ajung la terminatorul 0000.
Afișez output-ul.
Notă: Menționez că înainte să implementez funcția qr_to_matrix, am folosit funcții din biblioteca qrcode pentru a crea matricea respectivă și a face debug pe cod. Am lăsat și acel cod în comentarii.

**GENERATOR**

Folosesc matrici din biblioteca numpy și funcții din matplotlib pentru a transforma matricea într-o imagine.

Initializez matricea cu elementele comune pentru orice cod QR de versiune 2: finding_patterns, orientation_pattern, timing_pattern.
Preiau string-ul din input și îl transform în binar, iar înaintea lui adaug cei 4 biți de tip de date (hardcodați) și byte-ul care specifică lungimea string-ului. Adaug bitii de corecție folosind algoritmul lui Reed-Solomon și funcții din această bibliotecă, iar la final adaug bitii de padding.
Notă: Algoritmul lui Reed-Solomon se bazează pe faptul că există un singur polinom de grad n-1 care trece prin n puncte. Astfel, dacă construiesc acest polinom, nu doar că voi ști sigur ce biți au fost corupți, dar voi avea și o metodă pentru a afla ce valoare transmiteau inițial (găsind valoarea polinomului în punctul respectiv).
Efectuez XOR cu toate cele 8 măști și calculez scorul pentru fiecare.
Afișez QR-ul cu scorul de penalizare cel mai mic.

**SURSE**

Am căutat informații pe diverse site-uri și am vizionat videoclipuri pe YouTube pentru a înțelege foarte bine cum funcționează codurile QR. Mai jos este lista link-urilor către aceste surse:

https://www.nayuki.io/page/creating-a-qr-code-step-by-step

https://www.youtube.com/watch?v=w5ebcowAJD8&t=1716s&ab_channel=Veritasium

https://www.researchgate.net/figure/The-structure-of-QR-code-in-version-2-M_fig5_333611998

https://www.youtube.com/watch?v=Rc3ul6RRANU&ab_channel=ProfessorJulioLombaldo

https://www.youtube.com/watch?v=sRgUrKWiXQs&ab_channel=NoOneAsked

https://www.youtube.com/watch?v=1pQJkt7-R4Q&t=650s&ab_channel=vcubingx
