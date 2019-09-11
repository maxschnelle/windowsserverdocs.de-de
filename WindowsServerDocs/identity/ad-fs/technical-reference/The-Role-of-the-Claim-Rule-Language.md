---
title: Rolle der Anspruchsregelsprache
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: dda9d148-d72f-4bff-aa2a-f2249fa47e4c
ms.technology: identity-adfs
ms.openlocfilehash: 0c2d411be7ef807198df30074ea706d7c5398617
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869360"
---
# <a name="the-role-of-the-claim-rule-language"></a>Rolle der Anspruchsregelsprache
Die Anspruchs Regel Sprache Active Directory-Verbunddienste (AD FS) (AD FS) fungiert als administrativer Baustein für das Verhalten von eingehenden und ausgehenden Ansprüchen, während die Anspruchs-Engine als Verarbeitungs-Engine für die Logik in der Anspruchs Regel Sprache fungiert, die definiert die benutzerdefinierte Regel. Weitere Informationen zur Verarbeitung aller Regeln durch die Anspruchs-Engine finden Sie [unter der Rolle der Anspruchs](The-Role-of-the-Claims-Engine.md)-Engine.  

## <a name="creating-custom-claim-rules-using-the-claim-rule-language"></a>Erstellen benutzerdefinierter Anspruchsregeln mithilfe der Anspruchsregelsprache  
AD FS bietet Administratoren die Möglichkeit, benutzerdefinierte Regeln zu definieren, die Sie verwenden können, um das Verhalten von Identitäts Ansprüchen mit der Anspruchs Regel Sprache zu bestimmen. Mithilfe der Syntaxbeispiele für die Anspruchsregelsprache in diesem Thema können Sie benutzerdefinierte Regeln erstellen, die Ansprüche gemäß der Anforderungen Ihrer Organisation aufzählen, hinzufügen, löschen oder modifizieren. Benutzerdefinierte Regeln können durch Eingabe eines Syntaxausdrucks der Anspruchsregelsprache in die Regelvorlage **Ansprüche mit einem benutzerdefinierten Anspruch senden** erstellt werden.  

Regeln werden durch Semikolons voneinander getrennt.  

Weitere Informationen dazu, wann benutzerdefinierte Regeln verwendet werden sollten, finden Sie unter [Verwenden einer benutzerdefinierten Anspruchs Regel](When-to-Use-a-Custom-Claim-Rule.md).  

## <a name="using-claim-rule-templates-to-learn-about-the-claim-rule-language-syntax"></a>Verwenden von Anspruchsregelvorlagen zum Erlernen der Syntax der Anspruchsregelsprache  
AD FS bietet auch eine Reihe von vordefinierten Anspruchs Ausstellungs-und Anspruchs Annahme-Regel Vorlagen, mit denen Sie gängige Anspruchs Regeln implementieren können. Mithilfe des Dialogfelds **Anspruchsregeln bearbeiten** lassen sich vordefinierte Regeln erstellen, wobei auch die zugrundeliegende Syntax der Anspruchsregelsprache angezeigt wird, indem Sie auf die Registerkarte **Regelsprache anzeigen** für diese Regel klicken. Mithilfe der Informationen in diesem Abschnitt und der Hilfestellung durch die Funktion **Regelsprache anzeigen** lässt sich das Erstellen eigener, benutzerdefinierter Regeln erschließen.  

Ausführlichere Informationen zu Anspruchs Regeln und Anspruchs Regel Vorlagen finden Sie [unter Rolle der Anspruchs Regeln](The-Role-of-Claim-Rules.md).  

## <a name="understanding-the-components-of-the-claim-rule-language"></a>Grundlegendes zu den Komponenten der Anspruchsregelsprache  
Die Anspruchs Regel Sprache besteht aus den folgenden Komponenten, getrennt durch den Operator "= >":  

-   Eine Bedingung  

-   Eine Ausstellungsanweisung  

### <a name="conditions"></a>Bedingungen  
Die Bedingungen dienen in einer Regel dazu, Eingabeansprüche zu überprüfen und zu bestimmen, ob die Ausstellungsanweisung der Regel ausgeführt werden soll. Eine Bedingung stellt einen logischen Ausdruck dar, dessen Auswertung „true“ ergeben muss, damit der Hauptteil der Regel ausgeführt wird. Wenn dieser Teil fehlt, wird eine logische true angenommen. Das heißt, dass der Regeltext immer ausgeführt wird. Der Abschnitt Bedingungen enthält eine Liste der Bedingungen, die zusammen mit dem logischen Operator ("& &") kombiniert werden. Alle Bedingungen in der Liste müssen „true“ ergeben, damit der Bedingungsteil insgesamt „true“ ergibt. Die Bedingung kann entweder ein Anspruchsselektoroperator oder ein zusammengesetzter Funktionsaufruf sein. Diese beiden Möglichkeiten schließen sich gegenseitig aus – Anspruchsselektoren und zusammengesetzte Funktionen lassen sich nicht im Bedingungsteil derselben Regel verwenden.  

Bedingungen sind in Regeln optional. Beispielsweise besitzt die folgende Regel keine Bedingung:  

```  
=> issue(type = "http://test/role", value = "employee");  
```  

Es gibt drei Arten von Bedingungen:  

-   Einzelbedingung – dies ist die einfachste Form einer Bedingung. Überprüfungen werden nur für einen Ausdruck durchgeführt. Beispiel: Windows-Kontoname = Domäne Benutzer.  

-   Mehrere Bedingungen – diese Bedingung erfordert zusätzliche Überprüfungen, um mehrere Ausdrücke im Hauptteil der Regel zu verarbeiten. Beispiel: Windows-Kontoname = Domäne Benutzer und Gruppe = "kontosopurchasers".  

> [!NOTE]  
> Es gibt einen weiteren Bedingungstyp, der jedoch Bestandteil von Einzelbedingungen und Mehrfachbedingungen sein kann. Es wird als Bedingung für reguläre Ausdrücke (Regex) bezeichnet. Dabei wird ein Eingabeausdruck mit einem festgelegten Muster verglichen. Ein Verwendungsbeispiel wird unten gezeigt.  

Die folgenden Beispiele zeigen einige Syntaxformen, die aus den drei Bedingungstypen bestehen, aus denen benutzerdefinierte Regeln erstellt werden können.  

#### <a name="single--condition-examples"></a>Beispiele für einfache Bedingung  
Einausdrucks Bedingungen werden in der folgenden Tabelle beschrieben. Sie sind so aufgebaut, dass lediglich ein Anspruch mit einem bestimmten Anspruchstyp verglichen wird oder ein Anspruch mit einem bestimmten Anspruchstyp und einem zugehörigem Anspruchswert.  


|                                                                                                                   Beschreibung der Bedingung                                                                                                                    |                           Syntaxbeispiel der Bedingung                            |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
|               Diese Regel besteht aus einer Bedingung zum Überprüfen eines Eingabe Anspruchs mit einem angegebenen Anspruchstyp (<http://test/name>""). Wenn ein passender Anspruch in den Eingabeansprüchen vorhanden ist, kopiert die Regel den passenden Anspruch bzw. die Ansprüche in die Menge der Ausgabeansprüche.               |         ``` c: [type == "http://test/name"] => issue(claim = c );```          |
| Diese Regel weist eine Bedingung auf, um einen Eingabe Anspruch mit einem angegebenen Anspruchstyp ("<http://test/name>") und einem Anspruchs Wert ("Terry") zu überprüfen. Wenn ein passender Anspruch in den Eingabeansprüchen vorhanden ist, kopiert die Regel den passenden Anspruch bzw. die Ansprüche in die Menge der Ausgabeansprüche. | ``` c: [type == "http://test/name", value == "Terry"] => issue(claim = c);``` |

Komplexere Bedingungen werden im nächsten Abschnitt angezeigt, einschließlich Bedingungen zum Überprüfen auf mehrere Ansprüche, Bedingungen zum Überprüfen des Ausstellers eines Anspruchs und Bedingungen zum Überprüfen von Werten, die mit einem Muster für reguläre Ausdrücke zu vergleichen sind.  

#### <a name="multiple--condition-examples"></a>Beispiele mit mehreren Bedingungen  
In der folgenden Tabelle finden Sie ein Beispiel für Bedingungen mit mehreren Ausdrücken.  


|                                                                                                                   Beschreibung der Bedingung                                                                                                                    |                                        Syntaxbeispiel der Bedingung                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| Diese Regel besitzt eine Bedingung, überprüfen Sie, ob zwei zur Eingabe, Ansprüche, jeweils mit einem festgelegten Anspruchstyp ("<http://test/name>" und "<http://test/email>"). Wenn die zwei übereinstimmenden Ansprüche in den Eingabeansprüchen vorhanden sind, kopiert die Regel den Namensanspruch in die Menge der Ausgabeansprüche. | ``` c1: [type  == "http://test/name"] && c2: [type == "http://test/email"] => issue (claim  = c1 );``` |

#### <a name="regular--condition-examples"></a>Beispiele für reguläre Bedingungen  
In der folgenden Tabelle finden Sie ein Beispiel für eine reguläre, Ausdrucks basierte Bedingung.  

|Beschreibung der Bedingung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Diese Regel weist eine Bedingung auf, die einen regulären Ausdruck verwendet, um nach einem e-Mail-Anspruch@fabrikam.comzu suchen, der auf "" endet. Wenn ein übereinstimmender Anspruch in den Eingabeansprüchen gefunden wird, kopiert die Regel den übereinstimmenden Anspruch in den Ausgabeanspruchssatz.|```c: [type  == "http://test/email", value  =~ "^. +@fabrikam.com$" ] => issue (claim  = c );```|  

### <a name="issuance-statements"></a>Ausstellungsanweisungen  
Benutzerdefinierte Regeln werden basierend auf den Ausstellungs Anweisungen (*Problem* oder *Hinzufügen* ) verarbeitet, die Sie in der Anspruchs Regel programmieren. Abhängig vom gewünschten Ergebnis kann entweder die „issue“-Anweisung (Ausgeben) oder die „add“-Anweisung (Hinzufügen) in die Regel geschrieben werden, um den Eingabeanspruchssatz oder den Ausgabeanspruchssatz zu besetzen. Eine benutzerdefinierte Regel, die explizit die „add“-Anweisung verwendet, fügt Anspruchswerte nur in den Eingabeanspruchssatz ein, während eine benutzerdefinierte Regel, die explizit die „issue“-Anweisung verwendet, Anspruchswerte sowohl in den Eingabeanspruchssatz als auch in den Ausgabeanspruchssatz einfügt. Dies kann nützlich sein, wenn ein Anspruchswert nur von darauffolgenden Regeln in den Anspruchsregelsätzen verwendet werden soll.  

In der folgenden Abbildung wird beispielsweise der eingehende Anspruch durch das Anspruchsausgabemodul dem Eingabeanspruchssatz hinzugefügt. Wenn die erste benutzerdefinierte Anspruchs Regel ausgeführt wird und die Kriterien des Domänen Benutzers erfüllt sind, verarbeitet das Anspruchs Ausstellungs Modul die Logik in der Regel mithilfe der Add-Anweisung, und der Wert des **Editors** wird dem Eingangs Anspruchssatz hinzugefügt. Da der Wert des Editors im Eingangs Anspruchssatz vorhanden ist, kann Regel 2 die Issue-Anweisung in der Logik verarbeiten und den neuen Wert **Hello**generieren, der dem Ausgangs Anspruchssatz und dem Eingangs Anspruchssatz zur Verwendung durch die nächste Regel in der hinzugefügt wird. Regelsatz. In Regel 3 können jetzt alle Werte, die im Eingangs Anspruchssatz vorhanden sind, als Eingabe für die Verarbeitung der Logik verwendet werden.  

![Rollen AD FS](media/adfs2_customrule.gif)  

#### <a name="claim-issuance-actions"></a>Anspruchsausstellungsaktionen  
Der Hauptteil der Regel stellt eine Anspruchsausstellungsaktion dar. Die Sprache erkennt zwei Anspruchsausstellungsaktionen:  

-   **„issue“-Anweisung:** Die „issue“-Anweisung erstellt einen Anspruch, der sowohl in den Eingabeanspruchssatz als auch in den Ausgabeanspruchssatz kopiert wird. Die folgende Anweisung stellt beispielsweise eine neue Anforderung anhand ihres Eingabeanspruchssatzes aus.  

    ```c:[type == "Name"] => issue(type = "Greeting", value = "Hello " + c.value);```  

-   **„add“-Anweisung:** Die „add“-Anweisung erstellt eine neue Anforderung, die nur dem Eingabeanspruchssatz hinzugefügt wird. Die folgende Anweisung fügt z. B. dem Eingabeanspruchssatz einen neuen Anspruch hinzu:  

    ```c:[type == "Name", value == "domain user"] => add(type = "Role", value = "Editor");``` 

Die „issue“-Anweisung definiert, welche Ansprüche durch die Regel ausgegeben werden, wenn die Bedingungen zutreffen. Es gibt zwei Formen der „issue“-Anweisung, die sich durch die Anzahl der Argumente und das Verhalten der Anweisung unterscheiden:  

-   **Normal**: Normale „issue“-Anweisungen können Ansprüche ausgeben, wenn die Regel mithilfe von Literalwerten formuliert ist oder die Werte direkt in übereinstimmenden Ansprüchen zu finden sind. Eine normale „issue“-Anweisung besteht aus einem oder beiden der folgenden Formate:  

    -   *Anspruchskopie*: Bei der Anspruchskopie wird eine Kopie des vorhandenen Anspruchs in den Ausgabeanspruchssatz kopiert. Diese Form der Ausstellung ist nur in Kombination mit der Ausstellungsanweisung „issue“ sinnvoll. In Kombination mit der Ausstellungsanweisung „add“ hat sie keinerlei Auswirkung.  

    -   *Neuer Anspruch*: In diesem Format wird ein neuer Anspruch erstellt, wobei die Werte für verschiedene Anspruchs Eigenschaften angegeben werden. „Claim.Type“ muss angegeben werden, alle anderen Anspruchseigenschaften sind optional. Die Reihenfolge der Argumente wird in dieser Form ignoriert.  

-   **Attributspeicher**: Bei dieser Form werden Ansprüche mit Werten erstellt, die von einem Attributspeicher abgerufen werden. Es ist möglich, mehrere Anspruchs Typen mit einer einzelnen Ausstellungs Anweisung zu erstellen, was für Attribut Speicher wichtig ist, die während des Attribut Abrufs Netzwerk-oder Datenträger-e/a-Vorgänge (e/a-Vorgänge) durchführen. Daher ist es wünschenswert, die Anzahl der Roundtrips zwischen dem Richtlinienmodul und dem Attributspeicher zu begrenzen. Es ist auch zulässig, für einen Anspruchstyp jeweils mehrere Ansprüche zu erstellen. Wenn der Attributspeicher mehrere Werte für einen Anspruchstyp zurückliefert, erstellt die Ausstellungsanweisung automatisch einen Anspruch für jeden Anspruchswert. Ein Mechanismus des Attributspeichers ersetzt die Platzhalter im Abfrageargument durch die Parameterargumente. Die Platzhalter verwenden dieselbe Syntax wie die .net String. Format ()-Funktion (z {1} {2}. b., usw.). Die Reihenfolge der Argumente für diese Art der Ausstellung ist wichtig, und es muss die in der folgenden Grammatik vorgeschriebene Reihenfolge sein.  

Die folgende Tabelle beschreibt einige allgemeine Syntaxkonstruktionen für beide Ausstellungsanweisungen in Anspruchsregeln.  

|Ausstellungsanweisungstyp|Beschreibung der Ausstellungsanweisung|Syntaxbeispiel für Ausstellungsanweisung|  
|---------------------------|----------------------------------|-------------------------------------|  
|Normal|Die folgende Regel gibt immer den gleichen Anspruch aus, wenn ein Benutzer den angegebenen Anspruchstyp und den Wert enthält:|```c: [type  == "http://test/employee", value  == "true"] => issue (type = "http://test/role", value = "employee");```|  
|Normal|Die folgende Regel konvertiert einen Anspruchstyp in einen anderen. Beachten Sie, dass der Wert des Anspruchs, der der Bedingung „c“ entspricht, in der Ausstellungsanweisung verwendet wird.|```c: [type  == "http://test/group" ] => issue (type  = "http://test/role", value  = c.Value );```|  
|Attributspeicher|Die folgende Regel verwendet den Wert eines eingehenden Anspruchs, um den Active Directory Attribut Speicher abzufragen:|```c: [Type  == "http://test/name" ] => issue (store  = "Enterprise AD Attribute Store", types  =  ("http://test/email" ), query  = ";mail;{0}", param  = c.Value )```|  
|Attributspeicher|Die folgende Regel verwendet den Wert eines eingehenden Anspruchs, um einen zuvor konfigurierten strukturierte Abfragesprache (SQL)-Attribut Speicher abzufragen:|```c: [type  == "http://test/name"] => issue (store  = "Custom SQL store", types  =  ("http://test/email","http://test/displayname" ), query  = "SELECT mail, displayname FROM users WHERE name ={0}", param  = c.value );```|  

#### <a name="expressions"></a>Ausdrücke  
Ausdrücke werden auf der rechten Seite sowohl für Anspruchsselektorbeschränkungen als auch für Parameter für Ausstellungsanweisungen verwendet. Es gibt verschiedene Arten von Ausdrücken, die die Sprache unterstützt. Alle Ausdrücke in der Sprache operieren auf Zeichenfolgen, d. h., dass Zeichenfolgen als Eingabe angenommen und als Ausgabe erzeugt werden. Zahlen und andere Datentypen wie beispielsweise Datum/Uhrzeit werden in Ausdrücken nicht unterstützt. Die Sprache unterstützt folgende Arten von Ausdrücken:  

-   Zeichenfolgenliteral: Zeichen folgen Wert, begrenzt durch das Anführungszeichen (") auf beiden Seiten.  

-   Verkettung von Ausdrücken als Zeichenfolgen: Das Ergebnis ist eine Zeichenfolge, die durch Verkettung der linken und rechten Werte erzeugt wird.  

-   Funktionsaufruf: Die-Funktion wird durch einen Bezeichner identifiziert, und die Parameter werden als durch Trennzeichen getrennte Liste von Ausdrücken, die in Klammern eingeschlossen sind ("()"), übermittelt.  

-   Der Anspruch der Anspruchs Eigenschaft in Form eines Variablen namens Punkt-Eigenschaftsnamen: Das Ergebnis des Werts der-Eigenschaft des identifizierten Anspruchs für eine bestimmte Variablen Bewertung. Die Variable muss zunächst an einen Anspruchsselektor gebunden werden, bevor sie in dieser Weise verwendet werden kann. Es ist nicht zulässig, die an einen Anspruchsselektor gebundene Variable in den Beschränkungen für denselben Anspruchsselektor zu verwenden.  

Die folgenden Anspruchseigenschaften sind verfügbar:  

-   Claim.Type  

-   Claim.Value  

-   Claim.Issuer  

-   Claim.OriginalIssuer  

-   Claim.ValueType  

-   Claim. Properties\[-\_Eigenschaften\] Name (diese Eigenschaft gibt eine leere Zeichenfolge zurück, wenn die _name-Eigenschaft in der Properties-Auflistung des Anspruchs nicht gefunden werden kann. )  

Die RegexReplace-Funktion kann innerhalb eines Ausdrucks für Aufrufe verwendet werden. Diese Funktion übernimmt einen Eingabeausdruck und vergleicht ihn mit dem angegebenen Muster. Wenn das Muster übereinstimmt, wird die Ausgabe der Übereinstimmung durch den Ersatzwert ersetzt.  

#### <a name="exists-functions"></a>Exists-Funktion  
Die Exists-Funktion kann in einer Bedingung verwendet werden, um das Vorhandensein eines Anspruchs im Eingabeanspruchssatz zu prüfen, der mit der Bedingung übereinstimmt. Wenn übereinstimmende Ansprüche vorhanden sind, wird die Ausstellungsanweisung nur einmal aufgerufen. Im folgenden Beispiel wird der Anspruch „origin“ genau einmal ausgegeben, nämlich dann, wenn mindestens ein Anspruch im Eingabeanspruchssatz vorhanden ist, bei dem der Aussteller „MSFT“ festgelegt wurde. Dabei ist die tatsächliche Anzahl der Ansprüche unerheblich, bei denen dies der Fall ist. Mit dieser Funktion wird verhindert, dass doppelte Ansprüche ausgestellt werden.  

```  
exists([issuer == "MSFT"])  
   => issue(type = "origin", value = "Microsoft");  
```  

## <a name="rule-body"></a>Hauptteil der Regel  
Der Hauptteil der Regel kann nur eine einzelne Ausgabeanweisung enthalten. Wenn Bedingungen verwendet werden, ohne die Exists-Funktion zu nutzen, wird der Hauptteil der Regel jedes Mal ausgeführt, wenn der Bedingungsteil übereinstimmt.  

## <a name="additional-references"></a>Weitere Verweise  
[Erstellen einer Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](https://technet.microsoft.com/library/dd807049.aspx)  


