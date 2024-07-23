# <a name="main"></a>**3.3 - Conversors: InputStreamReader i OutputStreamWriter**
Una vegada vistes les jerarquies de les classes **InputStream-OutputStream** per una banda, i **Reader-Writer** per una altra, veurem ara unes classes que serviran per a passar d'una jeraquia a una altra. És a dir, poder passar un **InputStream** a **Reader**, o el que és el mateix, un flux orientat a bytes en un flux orientat a caràcters. I el mateix amb el OutputStream i el Writer.

- **InputStreamReader**: passa un **InputStream** a **Reader**. Accepta com a paràmetre el **InputStream** i dóna com a resultat un **Reader**.
- **OutputStreamWriter**: passa un **OutputStream** a **Writer**. Accepta com a paràmetre el **OutputStream** i dóna com a resultat un **Writer**.

A més en el constructor dels dos, **InputStreamReader** i **OutputStreamWriter**, tenim la possibilitat d'especificar el tipus de codificació, a més del InputStream o OutputStream. Açò ens serà molt útil, perquè fins el moment no podíem triar el tipus de codificació d'un **FileReader** o **FileWriter** que era UTF-8 en el cas de Linux, i ASCII (millor dit la seua extensió ISO-8859-1) en el cas de Windows. 

Mirem aquest exemple, en el qual transformem el mateix fitxer d'una configuració a una altra. Aprofitem algun dels fitxers que ja disposem (per exemple f5.txt, que tenia caràcters especials com vocals accentuades). En l'exemple el tindrem en codificació UTF-8, ja que està provat en Linux. El transformarem a ISO-8859-1. Copieu el següent codi en un fitxer anomenat **Exemple\_2\_61.kt** :

package exemples

import java.io.InputStreamReader

import java.io.FileInputStream

import java.io.OutputStreamWriter

import java.io.FileOutputStream

fun main(args: Array<String>) {

`	`val f\_ent = InputStreamReader(FileInputStream("f5.txt"), "UTF-8")

`	`val f\_eix = OutputStreamWriter(FileOutputStream("f5\_ISO.txt"), "ISO-8859-1")

`	`var car = f\_ent.read()

`	`while (car != -1) {

`		`f\_eix.write(car)

`		`car = f\_ent.read()

`	`}

`	`f\_eix.close()

`	`f\_ent.close()

}

Hem posat l'entrada explícitament que siga de UTF-8. En realitat no faria falta, ja que si treballem en Linux, aquesta serà la codificació per defecte, i per tant seria la que utilitzaria un FileReader.



FileReader f\_ent = new FileReader("f5.txt")

Anem a fer una altra versió del mateix programa. A banda de no especificar la codificació del fitxer d'entrada, utilitzarem els decoradors **BufferedReader** i **PrintWriter** per a poder anar còmodament línia a línia. Copieu el següent codi en un fitxer anomenat **Exemple\_2\_62.kt** :

package exemples

import java.io.FileReader

import java.io.BufferedReader

import java.io.FileOutputStream

import java.io.OutputStreamWriter

import java.io.PrintWriter

fun main(args: Array<String>) {

`	`val f\_ent = BufferedReader(FileReader ("f5.txt"))

`	`val f\_eix = PrintWriter(OutputStreamWriter(FileOutputStream ("f5\_ISO.txt"), "ISO-8859-1"))

`	`var cad = f\_ent.readLine()

`	`while (cad != null) {

`		`f\_eix.println(cad)

`		`cad = f\_ent.readLine()

`	`}

`	`f\_eix.close()

`	`f\_ent.close()

}



Llicenciat sota la [Llicència Creative Commons Reconeixement NoComercial CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)
