# <a name="main"></a>**4 - Simplificació en Kotlin**
Tots els programes anteriors funcionen en Kotlin perfectament, perquè estem utilitzant les classes de Java, i aquestes sense problemes funcionen en Kotlin, és una de les seues característiques.

Tanmateix, Kotlin proporcionarà funcionalitat extra en les classes, que ens permetrà simplificar prou els programes. Són molts els mètodes nous que ens proporcionarà. Ací tenim uns quants agrupats per temàtica.

Mètodes sobre bytes

- **readBytes()** : torna un **ByteArray** amb tots els bytes del fitxer, és a dir, tot el seu contingut en forma de bytes
- **writeBytes(*array*: ByteArray)** : escriu en el fitxer el contingut del ByteArray. Si el fitxer ja existia, el sobreescriura.
- **appendBytes(*array*: ByteArray)** : afegeix al final del fitxer els bytes del ByteArray.

Tornem a fer el primer exemple, Exemple\_2\_01.kt, utilitzant aquesta funcionalitat extra. Copieu el següent com **Exemple\_2\_01\_bis.kt**:

package exemples

import java.io.File

fun main(){

`	`val f = File("f1.txt")

`	`val tot = f.readBytes()

`	`for (c in tot){

`		`println(c.toChar())

`	`}

}

I com a exemple d'escriptura, podem fer Exemple\_2\_11.kt,on ho podem fer tot en una línia. Copieu el següent com **Exemple\_2\_11\_bis.kt**:

package exemples

import java.io.File

fun main() {

`	`val text = "Contingut per al fitxer."

`	`File("f3.txt").writeBytes(text.toByteArray())

}

Recordeu que en els dos exemples anteriors per comoditat estem utilitzant caràcters com a dades, i no seria el més correcte utilitzar bytes ni de lectura ni d'escriptura. Ho hem fet únicament per comoditat.

Mètodes sobre caràcters

- **readText(*charset*: CharSet)**: torna un String amb la tots els caràcters del fitxer. Opcionalment li podem dir el joc de caràcters (si no li ho diem utilitzarà UTF-8)
- **readLines(*charset*: CharSet)**: torna un List de Strings amb totes les línies del fitxer
- **writeText(*text*: String, *charset*: CharSet)**: escriu el string en el fitxer. Si el fitxer ja existia el sobreescriurà. Opcionalment podem posar el joc de caràcters que volem utilitzar. Si no el posem utilitzarà UTF-8. Observeu que ja disposàvem d'un mètode que escrivia tot un String anteriorment, per tant no és una gran millora, excepte pel fet de poder especificar el joc de caràcters. Açò sí que és de gran comoditat.
- **appendText(*text*: String, *charset*: CharSet)**: el mateix que l'anterior, però afegint al final.

Com a exemple anem a veure Exemple\_2\_21.kt. Copieu el següent com **Exemple\_2\_21\_bis.kt**:

package exemples

import java.io.File

fun main(){

`	`val tot = File("f1.txt").readText()

`	`for(c in tot){

`		`println(c)

`	`}

}

I com a exemple d'escriptura, l'adaptació de Exemple\_2\_31.kt. Copieu el següent com **Exemple\_2\_31\_bis.kt**:

package exemples

import java.io.File

fun main() {

`	`val text = "Contingut per al fitxer. Ara ja sense por a caràcters especials: ç, à, ú, ..."

`	`File("f5.txt").writeText(text)

}

I com a exemple de copiar un fitxer en un altre, fins i tot canviant el joc de caràcters, farem una altra versió del Exemple\_2\_61.kt. Copieu el següent com **Exemple\_2\_61\_bis.kt**:

package exemples

import java.io.File

fun main() {

`	`File("f5\_2.txt").writeText(File("f5.txt").readText(), Charsets.ISO\_8859\_1)

}

Mètodes de conversió

En ocasions és possible que no tinguem un mètode directament en File que ens vinga bé. Un exemple són els mètodes print (print, println, printf). Aleshores, senzillament a partir del File la classe que ens convinga de la jerarquia de InputStream/OutputStream o Reader/Writer. Són mètodes que ens tornen la classe desitjada:

- **inputStream()**: construeix in un InputStream que apunta al File, i el torna
- **inputStream()**: el mateix amb un OutputStream
- **reader(*charset*: Charset)**: el mateix amb un Reader, tenint la possibilitat d'especificar el joc de caràcters (si no s'especifica serà UTF-8)
- **writer(*charset*: Charset)**: el mateix amb un Writer
- **bufferedReader(*charset*: Charset)**: el mateix amb un BufferedReader
- **printWriter(*charset*: Charset)**: el mateix amb un Writer

Per exemple, el que hem comentat més amunt: si volem els mètodes print, senzillament obtenim un **PrintWriter** a partir del File. D'aquesta manera, el Exemple\_2\_41.kt ens quedaria d'una altra manera per a obtenir el PrintWriter que volíem. Copieu el següent com **Exemple\_2\_41\_bis.kt**:

package exemples

import java.io.File

fun main() {

`	`val f\_out = File("f6.txt").printWriter()

`	`val a = 5.25.toFloat()

`	`val b = "Hola."

`	`f\_out.print(b)

`	`f\_out.println("Què tal?")

`	`f\_out.println(a + 3)

`	`f\_out.printf("El número %d en hexadecimal és %x", 27, 27)

`	`f\_out.close();

}

Altres mètodes

Hi ha altres mètodes que poden ser molt útils. Per exemple aquell que copia directament un fitxer, o tot un directori recursivament, o que esborra recursivament, ...

- **copyTo(*destí*: File, *sobre\_escriure*: Boolean, *buffer*: Int)**: copia en el fitxer de destí. Per defecte no sobreescriurà, a no ser que posem true en el segon paràmentre. El tercer paràmetre és per a marcar la grandària del buffer de dades per a fer la còpia.
- **copyRecursively(*destí*: File, *sobre\_escriure*: Boolean)**: copia recursivament el File i tots els seus descendents en el File de destí. Per defecte no sobreescriurà, a menys que posem true en el segon paràmentre. Opcionalment es pot posar un tercer paràmetre per al tractament dels possibles errors
- **deleteRecursively():** esborra el file i tots els seus possibles descendents

També hi ha altres mètodes, com per exemple per a comprovar si el nom del File té extensió, o si comença o finalitza igual que un altre, o per a normalitzar la ruta (llevar possibles redundàncies), i altre més.

Es poden consultar totes les extensions que proporciona Kotline a la classe File en:

https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/java.io.-file/


Llicenciat sota la [Llicència Creative Commons Reconeixement NoComercial CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)
