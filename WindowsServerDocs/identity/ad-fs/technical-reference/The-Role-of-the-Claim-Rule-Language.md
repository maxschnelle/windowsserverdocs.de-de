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
ms.openlocfilehash: 05728f04f6fb924cf3793bc843df3832c7c383f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855691"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-the-claim-rule-language"></a>Rolle der Anspruchsregelsprache
Die Active Directory-Verbunddienste (AD FS)-Anspruch fungiert als administrativer Baustein für das Verhalten von eingehenden und ausgehenden Ansprüchen, während das anspruchsmodul als Verarbeitungsmodul für die Logik der anspruchsregelsprache fungiert, definiert die benutzerdefinierte Regel. Weitere Informationen dazu, wie alle Regeln von der Anspruchs-Engine verarbeitet werden, finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md).  
  
## <a name="creating-custom-claim-rules-using-the-claim-rule-language"></a>Erstellen benutzerdefinierter Anspruchsregeln mithilfe der Anspruchsregelsprache  
AD FS bietet Administratoren die Möglichkeit, benutzerdefinierte Regeln zu definieren, die sie verwenden können, um das Verhalten von Identitätsansprüchen mithilfe der anspruchsregelsprache bestimmen. Mithilfe der Syntaxbeispiele für die Anspruchsregelsprache in diesem Thema können Sie benutzerdefinierte Regeln erstellen, die Ansprüche gemäß der Anforderungen Ihrer Organisation aufzählen, hinzufügen, löschen oder modifizieren. Benutzerdefinierte Regeln können durch Eingabe eines Syntaxausdrucks der Anspruchsregelsprache in die Regelvorlage **Ansprüche mit einem benutzerdefinierten Anspruch senden** erstellt werden.  
  
Regeln werden durch Semikolons voneinander getrennt.  
  
Weitere Informationen zur Verwendung benutzerdefinierte Regeln finden Sie unter [verwenden Sie eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
## <a name="using-claim-rule-templates-to-learn-about-the-claim-rule-language-syntax"></a>Verwenden von Anspruchsregelvorlagen zum Erlernen der Syntax der Anspruchsregelsprache  
AD FS bietet auch eine Reihe von vordefinierten Anspruch Ausstellung und -Anspruch, dass die Annahme von Regelvorlagen, die Sie verwenden können, um allgemeine implementieren Anspruchsregeln. Mithilfe des Dialogfelds **Anspruchsregeln bearbeiten** lassen sich vordefinierte Regeln erstellen, wobei auch die zugrundeliegende Syntax der Anspruchsregelsprache angezeigt wird, indem Sie auf die Registerkarte **Regelsprache anzeigen** für diese Regel klicken. Mithilfe der Informationen in diesem Abschnitt und der Hilfestellung durch die Funktion **Regelsprache anzeigen** lässt sich das Erstellen eigener, benutzerdefinierter Regeln erschließen.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelvorlagen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md).  
  
## <a name="understanding-the-components-of-the-claim-rule-language"></a>Grundlegendes zu den Komponenten der Anspruchsregelsprache  
Die anspruchsregelsprache besteht aus den folgenden Komponenten, getrennt durch die "= >"-Operator:  
  
-   Eine Bedingung  
  
-   Eine Ausstellungsanweisung  
  
### <a name="conditions"></a>Bedingungen  
Die Bedingungen dienen in einer Regel dazu, Eingabeansprüche zu überprüfen und zu bestimmen, ob die Ausstellungsanweisung der Regel ausgeführt werden soll. Eine Bedingung stellt einen logischen Ausdruck dar, dessen Auswertung „true“ ergeben muss, damit der Hauptteil der Regel ausgeführt wird. Wenn dieser Teil fehlt, wird der logische Wert „true“ stets impliziert, d. h., der Hauptteil der Regel wird in diesem Fall immer ausgeführt. Der Bedingungsteil enthält eine Liste der Bedingungen, die zusammen mit der logischen und-Operator kombiniert werden ("& &"). Alle Bedingungen in der Liste müssen „true“ ergeben, damit der Bedingungsteil insgesamt „true“ ergibt. Die Bedingung kann entweder ein Anspruchsselektoroperator oder ein zusammengesetzter Funktionsaufruf sein. Diese beiden Möglichkeiten schließen sich gegenseitig aus – Anspruchsselektoren und zusammengesetzte Funktionen lassen sich nicht im Bedingungsteil derselben Regel verwenden.  
  
Bedingungen sind in Regeln optional. Beispielsweise besitzt die folgende Regel keine Bedingung:  
  
```  
=> issue(type = "http://test/role", value = "employee");  
```  
  
Es gibt drei Arten von Bedingungen:  
  
-   Einzelbedingung – dies ist die einfachste Form einer Bedingung. Überprüfungen werden nur ein einziger Ausdruck getroffen. Windows-Konto z. B. Name = Domänenbenutzer.  
  
-   Mehrfachbedingung – dieser Bedingungstyp erfordert zusätzliche Überprüfungen, um mehrere Ausdrücke im Hauptteil Regel; zu verarbeiten. Windows-Konto z. B. Name = Domänenbenutzer und Group = Contosopurchasers.  
  
> [!NOTE]  
> Es gibt einen weiteren Bedingungstyp, der jedoch Bestandteil von Einzelbedingungen und Mehrfachbedingungen sein kann. Es wird als eine Bedingung für reguläre Ausdrücke (Regex) bezeichnet. Dabei wird ein Eingabeausdruck mit einem festgelegten Muster verglichen. Ein Verwendungsbeispiel wird unten gezeigt.  
  
Die folgenden Beispiele zeigen einige Syntaxformen, die aus den drei Bedingungstypen bestehen, aus denen benutzerdefinierte Regeln erstellt werden können.  
  
#### <a name="single--condition-examples"></a>Einzelne - Beispiele für die erste Bedingung  
Single - Bedingungen mit Ausdrücken in der folgenden Tabelle beschrieben werden. Sie sind so aufgebaut, dass lediglich ein Anspruch mit einem bestimmten Anspruchstyp verglichen wird oder ein Anspruch mit einem bestimmten Anspruchstyp und einem zugehörigem Anspruchswert.  
  
|Beschreibung der Bedingung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Diese Regel besitzt eine Bedingung zu prüfen, ein Eingabeanspruch mit einem festgelegten Anspruchstyp ("http://test/name"). Wenn ein passender Anspruch in den Eingabeansprüchen vorhanden ist, kopiert die Regel den passenden Anspruch bzw. die Ansprüche in die Menge der Ausgabeansprüche.|``` c: [type == "http://test/name"] => issue(claim = c );```|  
|Diese Regel besitzt eine Bedingung zu prüfen, ein Eingabeanspruch mit einem festgelegten Anspruchstyp ("http://test/name") und einem Anspruchswert ("Terry"). Wenn ein passender Anspruch in den Eingabeansprüchen vorhanden ist, kopiert die Regel den passenden Anspruch bzw. die Ansprüche in die Menge der Ausgabeansprüche.|``` c: [type == "http://test/name", value == "Terry"] => issue(claim = c);```|  
  
-Werden komplexe Bedingungen angezeigt, im nächsten Abschnitt, einschließlich der Bedingungen zu prüfen, ob mehrere Ansprüche, Bedingungen, um den Aussteller des Anspruchs zu überprüfen und Bedingungen auf Werte, die mit einem Muster eines regulären Ausdrucks übereinstimmen.  
  
#### <a name="multiple--condition-examples"></a>Beispiele für mehrere - Bedingungen  
Die folgende Tabelle enthält ein Beispiel für mehrere - Expression-Bedingungen.  
  
|Beschreibung der Bedingung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Diese Regel besitzt eine Bedingung, überprüfen Sie, ob zwei zur Eingabe, Ansprüche, jeweils mit einem festgelegten Anspruchstyp ("http://test/name" und "http://test/email"). Wenn die zwei übereinstimmenden Ansprüche in den Eingabeansprüchen vorhanden sind, kopiert die Regel den Namensanspruch in die Menge der Ausgabeansprüche.|``` c1: [type  == "http://test/name"] && c2: [type == "http://test/email"] => issue (claim  = c1 );```|  
  
#### <a name="regular--condition-examples"></a>Reguläre - Beispiele für die erste Bedingung  
Die folgende Tabelle enthält ein Beispiel für einen regulären, Ausdruck-Bedingung basiert.  
  
|Beschreibung der Bedingung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Diese Regel hat eine Bedingung, die einen regulären Ausdruck verwendet, überprüfen Sie für eine e-Mail-Anspruch auf "@fabrikam.com". Wenn ein übereinstimmender Anspruch in den Eingabeansprüchen gefunden wird, kopiert die Regel den übereinstimmenden Anspruch in den Ausgabeanspruchssatz.|```c: [type  == "http://test/email", value  =~ "^. +@fabrikam.com$" ] => issue (claim  = c );```|  
  
### <a name="issuance-statements"></a>Ausstellungsanweisungen  
Benutzerdefinierte Regeln verarbeitet werden, basierend auf den ausstellungsanweisungen (*Problem* oder *hinzufügen* ), dass Sie in die Anspruchsregeln programmieren. Abhängig vom gewünschten Ergebnis kann entweder die „issue“-Anweisung (Ausgeben) oder die „add“-Anweisung (Hinzufügen) in die Regel geschrieben werden, um den Eingabeanspruchssatz oder den Ausgabeanspruchssatz zu besetzen. Eine benutzerdefinierte Regel, die explizit die „add“-Anweisung verwendet, fügt Anspruchswerte nur in den Eingabeanspruchssatz ein, während eine benutzerdefinierte Regel, die explizit die „issue“-Anweisung verwendet, Anspruchswerte sowohl in den Eingabeanspruchssatz als auch in den Ausgabeanspruchssatz einfügt. Dies kann nützlich sein, wenn ein Anspruchswert nur von darauffolgenden Regeln in den Anspruchsregelsätzen verwendet werden soll.  
  
In der folgenden Abbildung wird beispielsweise der eingehende Anspruch durch das Anspruchsausgabemodul dem Eingabeanspruchssatz hinzugefügt. Wenn die erste benutzerdefinierte Anspruchsregel ausgeführt wird und die Kriterien mindestens eines Domänenbenutzers erfüllt wird, wird die anspruchsausstellungs-Engine verarbeitet die Logik in der Regel mit dem "Add"-Anweisung und der Wert des **Editor** wird dem eingabeanspruchssatz hinzugefügt. Da der Wert von „Editor“ im Eingabeanspruchssatz vorhanden ist, kann Regel 2 die Ausstellungsanweisung ihrer Logik erfolgreich ausführen und den neuen Wert **Hello** erzeugen, der sowohl dem Ausgabeanspruchssatz als auch dem Eingabeanspruchssatz für die nächste Regel in der Regelmenge hinzugefügt wird. Regel 3 kann nun alle Ansprüche im Eingangsanspruchssatz als Eingabe für die Verarbeitung der Logik verwenden.  
  
![AD FS-Rollen](media/adfs2_customrule.gif)  
  
#### <a name="claim-issuance-actions"></a>Anspruchsausstellungsaktionen  
Der Hauptteil der Regel stellt eine Anspruchsausstellungsaktion dar. Die Sprache erkennt zwei Anspruchsausstellungsaktionen:  
  
-   **„issue“-Anweisung:** Die „issue“-Anweisung erstellt einen Anspruch, der sowohl in den Eingabeanspruchssatz als auch in den Ausgabeanspruchssatz kopiert wird. Die folgende Anweisung stellt beispielsweise eine neue Anforderung anhand ihres Eingabeanspruchssatzes aus.  
  
    ```c:[type == "Name"] => issue(type = "Greeting", value = "Hello " + c.value);```  
  
-   **„add“-Anweisung:** Die „add“-Anweisung erstellt eine neue Anforderung, die nur dem Eingabeanspruchssatz hinzugefügt wird. Die folgende Anweisung fügt z. B. dem Eingabeanspruchssatz einen neuen Anspruch hinzu:  
  
    ```c:[type == "Name", value == "domain user"] => add(type = "Role", value = "Editor");``` 
  
Die „issue“-Anweisung definiert, welche Ansprüche durch die Regel ausgegeben werden, wenn die Bedingungen zutreffen. Es gibt zwei Formen der „issue“-Anweisung, die sich durch die Anzahl der Argumente und das Verhalten der Anweisung unterscheiden:  
  
-   **Normal**: Normale „issue“-Anweisungen können Ansprüche ausgeben, wenn die Regel mithilfe von Literalwerten formuliert ist oder die Werte direkt in übereinstimmenden Ansprüchen zu finden sind. Eine normale „issue“-Anweisung besteht aus einem oder beiden der folgenden Formate:  
  
    -   *Anspruchskopie*: Bei der Anspruchskopie wird eine Kopie des vorhandenen Anspruchs in den Ausgabeanspruchssatz kopiert. Diese Form der Ausstellung ist nur in Kombination mit der Ausstellungsanweisung „issue“ sinnvoll. In Kombination mit der Ausstellungsanweisung „add“ hat sie keinerlei Auswirkung.  
  
    -   *Neuer Anspruch*: Dieses Format wird anhand der Werte verschiedener anspruchseigenschaften einen neuen Anspruch erstellt. „Claim.Type“ muss angegeben werden, alle anderen Anspruchseigenschaften sind optional. Die Reihenfolge der Argumente wird in dieser Form ignoriert.  
  
-   **Attributspeicher**: Bei dieser Form werden Ansprüche mit Werten erstellt, die von einem Attributspeicher abgerufen werden. Es ist möglich, mehrere Anspruchstypen erstellen, mit einer einzelnen ausstellungsanweisung, die was bei attributspeichern wichtig ist, die Netzwerk- oder datenträgerkonfigurationsdetails Eingabe-/Ausgabevorgänge (e/a)-Vorgänge während der attributabruf vorgenommen. Daher ist es wünschenswert, die Anzahl der Roundtrips zwischen dem Richtlinienmodul und dem Attributspeicher zu begrenzen. Es ist auch zulässig, für einen Anspruchstyp jeweils mehrere Ansprüche zu erstellen. Wenn der Attributspeicher mehrere Werte für einen Anspruchstyp zurückliefert, erstellt die Ausstellungsanweisung automatisch einen Anspruch für jeden Anspruchswert. Ein Mechanismus des Attributspeichers ersetzt die Platzhalter im Abfrageargument durch die Parameterargumente. Die Platzhalter verwenden dieselbe Syntax wie die .NET "String.Format" ()-Funktion (z. B. {1}, {2}und so weiter). Die Reihenfolge der Argumente für diese Art der Ausstellung ist wichtig, und es muss die in der folgenden Grammatik vorgeschriebene Reihenfolge sein.  
  
Die folgende Tabelle beschreibt einige allgemeine Syntaxkonstruktionen für beide Ausstellungsanweisungen in Anspruchsregeln.  
  
|Ausstellungsanweisungstyp|Beschreibung der Ausstellungsanweisung|Syntaxbeispiel für Ausstellungsanweisung|  
|---------------------------|----------------------------------|-------------------------------------|  
|Normal|Die folgende Regel gibt immer den gleichen Anspruch aus, wenn ein Benutzer den angegebenen Anspruchstyp und den Wert enthält:|```c: [type  == "http://test/employee", value  == "true"] => issue (type = "http://test/role", value = "employee");```|  
|Normal|Die folgende Regel konvertiert einen Anspruchstyp in einen anderen. Beachten Sie, dass der Wert des Anspruchs, der der Bedingung „c“ entspricht, in der Ausstellungsanweisung verwendet wird.|```c: [type  == "http://test/group" ] => issue (type  = "http://test/role", value  = c.Value );```|  
|Attributspeicher|Die folgende Regel verwendet den Wert eines eingehenden Anspruchs, um den Active Directory-Attributspeicher abzufragen:|```c: [Type  == "http://test/name" ] => issue (store  = "Enterprise AD Attribute Store", types  =  ("http://test/email" ), query  = ";mail;{0}", param  = c.Value )```|  
|Attributspeicher|Die folgende Regel verwendet den Wert eines eingehenden Anspruchs auf einen zuvor konfigurierten (SQL = Structured Query Language)-Attributspeichers:|```c: [type  == "http://test/name"] => issue (store  = "Custom SQL store", types  =  ("http://test/email","http://test/displayname" ), query  = "SELECT mail, displayname FROM users WHERE name ={0}", param  = c.value );```|  
  
#### <a name="expressions"></a>Ausdrücke  
Ausdrücke werden auf der rechten Seite sowohl für Anspruchsselektorbeschränkungen als auch für Parameter für Ausstellungsanweisungen verwendet. Es gibt verschiedene Arten von Ausdrücken, die die Sprache unterstützt. Alle Ausdrücke in der Sprache operieren auf Zeichenfolgen, d. h., dass Zeichenfolgen als Eingabe angenommen und als Ausgabe erzeugt werden. Zahlen und andere Datentypen wie beispielsweise Datum/Uhrzeit werden in Ausdrücken nicht unterstützt. Die Sprache unterstützt folgende Arten von Ausdrücken:  
  
-   Zeichenfolgenliteral: Ein Zeichenfolgenwert, getrennt durch das Anführungszeichen (") auf beiden Seiten.  
  
-   Verkettung von Ausdrücken als Zeichenfolgen: Das Ergebnis ist eine Zeichenfolge, die durch Verkettung der linken und rechten Werte erzeugt wird.  
  
-   Funktionsaufruf: Die Funktion wird durch einen Bezeichner identifiziert, und die Parameter als ein Komma übergeben werden: durch Trennzeichen getrennte Liste von Ausdrücken, die in eckige Klammern eingeschlossen ("()").  
  
-   Der Zugriff auf Anspruchseigenschaften erfolgt in der Form: Variablenname PUNKT Eigenschaftenname: Das Ergebnis ist der Wert der betreffenden Anspruchseigenschaft während der laufenden Auswertung. Die Variable muss zunächst an einen Anspruchsselektor gebunden werden, bevor sie in dieser Weise verwendet werden kann. Es ist nicht zulässig, die an einen Anspruchsselektor gebundene Variable in den Beschränkungen für denselben Anspruchsselektor zu verwenden.  
  
Die folgenden Anspruchseigenschaften sind verfügbar:  
  
-   Claim.Type  
  
-   Claim.Value  
  
-   Claim.Issuer  
  
-   Claim.OriginalIssuer  
  
-   Claim.ValueType  
  
-   Claim.Properties\[Eigenschaft\_Namen\] (diese Eigenschaft gibt eine leere Zeichenfolge, wenn die Eigenschaft _name in den Anspruch des Properties-Auflistung nicht gefunden wird. )  
  
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
[Erstellen Sie eine Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel](https://technet.microsoft.com/library/dd807049.aspx)  
  

