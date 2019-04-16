---
title: Die Rolle der Anspruchsregelsprache
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: dda9d148-d72f-4bff-aa2a-f2249fa47e4c
ms.technology: identity-adfs
ms.openlocfilehash: 206da33d33cbded0450db29615dc74eb1161cbce
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-the-claim-rule-language"></a>Die Rolle der Anspruchsregelsprache
Die Active Directory-Verbunddienste (AD FS), die Ansprüche fungiert als administrativer Baustein für das Verhalten von eingehenden und ausgehenden Ansprüchen, während das anspruchsmodul als Verarbeitungsmodul für die Logik der anspruchsregelsprache fungiert, die die benutzerdefinierte Regel definiert. Weitere Informationen dazu, wie alle Regeln durch das anspruchsmodul verarbeitet werden, finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  
## <a name="creating-custom-claim-rules-using-the-claim-rule-language"></a>Erstellen benutzerdefinierter Anspruchsregeln mithilfe der anspruchsregelsprache  
AD FS bietet Administratoren die Möglichkeit, benutzerdefinierte Regeln zu definieren, die sie verwenden können, um das Verhalten von Identitätsansprüchen mithilfe der anspruchsregelsprache bestimmen. Können der Syntaxbeispiele für den Anspruch in diesem Thema eine benutzerdefinierte Regel erstellen, die listet hinzugefügt, gelöscht, und ändert die Ansprüche gemäß den Bedürfnissen Ihrer Organisation. Sie können benutzerdefinierte Regeln erstellen, geben Sie in der Syntax der anspruchsregelsprache in die **Senden von Ansprüchen, die mit einem benutzerdefinierten Anspruch** Regelvorlage.  
  
Regeln werden durch Semikolons voneinander getrennt.  
  
Weitere Informationen zur Verwendung benutzerdefinierter Regeln finden Sie unter [verwenden eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
## <a name="using-claim-rule-templates-to-learn-about-the-claim-rule-language-syntax"></a>Verwenden von anspruchsregelvorlagen Informationen zu Syntax der anspruchsregelsprache  
AD FS bietet auch eine Reihe vordefinierter Regelvorlagen für das ausgeben und von Ansprüchen, Anspruchsregeln Annahme Vorlagen, die Sie verwenden können, um allgemeine zu implementieren. In der **Anspruchsregeln bearbeiten** im Dialogfeld für eine bestimmte Vertrauensstellung, können Sie eine vordefinierte Regel erstellen – und Anzeigen der Syntax anspruchsregelsprache, aus denen die Regel besteht – indem Sie auf die **Regelsprache anzeigen** Registerkarte für diese Regel. Mithilfe der Informationen in diesem Abschnittund der **Regelsprache anzeigen** Hilfestellung, wie Sie Ihre eigenen benutzerdefinierten Regeln zu erstellen.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelvorlagen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md).  
  
## <a name="understanding-the-components-of-the-claim-rule-language"></a>Grundlegendes zu den Komponenten der anspruchsregelsprache  
Die anspruchsregelsprache besteht aus den folgenden Komponenten, getrennt durch die "= >" Operator:  
  
-   Eine Bedingung  
  
-   Eine ausstellungsanweisung  
  
### <a name="conditions"></a>Bedingungen  
Sie können die Bedingungen in einer Regel verwenden, Eingabeansprüche zu überprüfen und festzustellen, ob die ausstellungsanweisung der Regel ausgeführt werden soll. Eine Bedingung stellt einen logischen Ausdruck, der bewertet werden muss zum Ausführen der Hauptteil der Regel auf true. Wenn dieser Teil fehlt, wird eine logische "Wahr" zurückgegeben wird davon ausgegangen, dass; Das heißt, wird der Hauptteil der Regel immer ausgeführt. Der Bedingungsteil enthält eine Liste der Bedingungen, die zusammen mit dem logischen und -Operator kombiniert werden ("& &"). Alle Bedingungen in der Liste ausgewertet werden müssen, um für den Bedingungsteil ausgewertet werden auf "true". Die Bedingung kann entweder ein anspruchsselektoroperator oder ein zusammengesetzter Funktionsaufruf sein. Diese beiden Möglichkeiten schließen sich gegenseitig aus, was bedeutet, dass die Selektoren Anspruch und Aggregatfunktionen können nicht in einen Bedingungsteil derselben Regel kombiniert werden.  
  
Bedingungen sind in Regeln optional. Beispielsweise besitzt die folgende Regel keine Bedingung:  
  
```  
=> issue(type = "http://test/role", value = "employee");  
```  
  
Es gibt drei Arten von Bedingungen:  
  
-   Einzelbedingung – Dies ist die einfachste Form einer Bedingung. Nur ein Ausdruck wird geprüft; beispielsweise Windows account Name = Domänenbenutzer.  
  
-   Mehrfachbedingung – dieser Bedingungstyp erfordert zusätzliche Überprüfungen, um mehrere Ausdrücke im Hauptteil Regel; verarbeiten. beispielsweise Windows account Name = Domänenbenutzer und Group = Contosopurchasers.  
  
> [!NOTE]  
> Eine weitere Bedingung vorhanden, aber es ist eine Teilmenge von einzelbedingungen und mehrfachbedingungen. Es wird als Bedingung regulärer Ausdruck (Regex) bezeichnet. Hiermit wird einen Eingabeausdruck und des Ausdrucks mit einem bestimmten Muster entsprechen. Ein Beispiel, wie es ist, kann verwendet werden wird unten gezeigt.  
  
Die folgenden Beispiele zeigen einige Syntaxformen, die auf die Bedingungstypen basieren, Sie verwenden können, um benutzerdefinierte Regeln zu erstellen.  
  
#### <a name="single--condition-examples"></a>Single - Bedingung Beispiele  
Single - Ausdruck Bedingungen in der folgenden Tabelle beschrieben werden. Sie werden erstellt, um einfach überprüfen, ein Anspruch mit einem festgelegten Anspruchstyp oder ein Anspruch mit einem festgelegten Anspruchstyp und einem Anspruchswert.  
  
|Beschreibung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Mit dieser Regel wird ein Eingabeanspruch mit einem festgelegten Anspruchstyp ("http://Test/name") suchen. Wenn ein übereinstimmender Anspruch in den Eingabeansprüchen vorhanden ist, kopiert die Regel den passenden Anspruch bzw. die Ansprüche für die Menge der Ausgabeansprüche.|``` c: [type == "http://test/name"] => issue(claim = c );```|  
|Mit dieser Regel wird ein Eingabeanspruch mit einem festgelegten Anspruchstyp ("http://Test/name") suchen und einem Anspruchswert ("Terry"). Wenn ein übereinstimmender Anspruch in den Eingabeansprüchen vorhanden ist, kopiert die Regel den passenden Anspruch bzw. die Ansprüche für die Menge der Ausgabeansprüche.|``` c: [type == "http://test/name", value == "Terry"] => issue(claim = c);```|  
  
Mehr - werden komplexe Bedingungen angezeigt im nächsten Abschnitt, beispielsweise Bedingungen, überprüfen Sie für mehrere Ansprüche Bedingungen den Aussteller eines Anspruchs überprüft und Bedingungen nach Werten gesucht, die mit einem Muster eines regulären Ausdrucks übereinstimmen.  
  
#### <a name="multiple--condition-examples"></a>Beispiele für mehrere - Bedingung  
Die folgende Tabelle enthält ein Beispiel für mehrere - Ausdruck Bedingungen.  
  
|Beschreibung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Mit dieser Regel wird ein prüfen, ob zwei jeweils mit einem festgelegten Anspruchstyp ("http://Test/name" und "http://Test/email"). Wenn die zwei übereinstimmenden Ansprüche in den Eingabeansprüchen vorhanden sind, kopiert die Regel den Namensanspruch die Menge der Ausgabeansprüche.|``` c1: [type  == "http://test/name"] && c2: [type == "http://test/email"] => issue (claim  = c1 );```|  
  
#### <a name="regular--condition-examples"></a>Reguläre - Bedingung Beispiele  
Die folgende Tabelle enthält ein Beispiel für eine, RA-Bedingung basiert.  
  
|Beschreibung|Syntaxbeispiel der Bedingung|  
|-------------------------|----------------------------|  
|Diese Regel ist eine Bedingung, die einen regulären Ausdruck zum Suchen nach verwendet eines E-Mail-Anspruch auf die Endung "@fabrikam.com". Wenn ein übereinstimmender Anspruch in den Eingabeansprüchen gefunden wird, kopiert die Regel den übereinstimmenden Anspruch in die Menge der Ausgabeansprüche.|```c: [type  == "http://test/email", value  =~ "^. +@fabrikam.com$" ] => issue (claim  = c );```|  
  
### <a name="issuance-statements"></a>"Issue"-Anweisungen  
Benutzerdefinierte Regeln verarbeitet werden, basierend auf den ausstellungsanweisungen (*Problem* oder *hinzufügen* ), dass Sie in der Anspruchsregel programmieren. Abhängig vom gewünschten Ergebnis kann entweder die "Issue"-Anweisung oder das Hinzufügen von Anweisung geschrieben werden kann, in der Regel zum Auffüllen der eingangsanspruchssatz oder den ausgabeanspruchssatz zu besetzen. Eine benutzerdefinierte Regel, die explizit die "Add"-Anweisung verwendet, fügt Anspruchswerte Werte nur in den eingabeanspruchssatz, während eine benutzerdefinierte Regel, die die "Issue"-Anweisung verwendet, Anspruchswerte Werte in den ein-als auch in der Ausgabe einfügt. Dies kann nützlich sein, wenn ein Anspruchswert nur von darauf folgenden Regeln in der Gruppe von Anspruchsregeln verwendet werden soll.  
  
Beispielsweise wird in der folgenden Abbildungeingehenden Anspruchs durch das anspruchsausgabemodul eingangsanspruchssatz hinzugefügt. Wenn die erste benutzerdefinierte Anspruchsregel ausgeführt wird und die Kriterien der Domänenbenutzer erfüllt ist, das anspruchsausstellungsmodul verarbeitet die Logik in der Regel mit dem "Add"-Anweisung und der Wert der **Editor** wird dem eingabeanspruchssatz hinzugefügt. Da der Wert des Editors in den eingabeanspruchssatz vorhanden ist, Regel 2 können erfolgreich verarbeitet die "Issue"-Anweisung in seiner Logik und generieren Sie einen neuen Wert des **Hello**, die beide die Ausgabe hinzugefügt wird als auch auf dem eingabeanspruchssatz für die Verwendung durch die nächste Regel in der Regel festgelegt. Regel 3 kann nun alle Werte verwenden, die im eingangsanspruchssatz als Eingabe für die Verarbeitung der Logik vorhanden sind.  
  
![AD FS-Rollen](media/adfs2_customrule.gif)  
  
#### <a name="claim-issuance-actions"></a>Anspruchsausstellungsaktionen  
Der Hauptteil der Regel stellt eine anspruchsausstellungsaktion dar. Es gibt zwei Anspruch Ausstellung Aktionen, die die Sprache erkennt:  
  
-   **Anweisung:** die "Issue"-Anweisung erstellt einen Anspruch, Eingabe und Ausgabe den ausgabeanspruchssatz. Die folgende Anweisung stellt beispielsweise eine neue Anforderung anhand ihres eingabeanspruchssatzes:  
  
    ```c:[type == "Name"] => issue(type = "Greeting", value = "Hello " + c.value);```  
  
-   **Fügen Sie Anweisung hinzu:** die "Add"-Anweisung erstellt eine neue Anforderung, die nur dem eingabeanspruchssatz hinzugefügt wird. Die folgende Anweisung fügt z.B. einen neuen Anspruch in den eingangsanspruchssatz:  
  
    ```c:[type == "Name", value == "domain user"] => add(type = "Role", value = "Editor");``` 
  
Die ausstellungsanweisung der Regel definiert, welche Ansprüche werden durch die Regel ausgegeben werden, wenn die Bedingungen zutreffen. Es gibt zwei Arten der ausstellungsanweisungen in Bezug auf Argumente und das Verhalten der Anweisung unterscheiden:  
  
-   **Normal**: normale "Issue"-Anweisungen können Ansprüche ausgeben, mithilfe von Literalwerten in der Regel oder die Werte von Ansprüche, die den Suchkriterien übereinstimmen. Eine normale ausstellungsanweisung besteht aus einer oder beide der folgenden Formate:  
  
    -   *Anspruchskopie*: der anspruchskopie wird eine Kopie des vorhandenen Anspruchs in den ausgabeanspruchssatz kopiert. Diese Form der Ausstellung ist nur sinnvoll, wenn sie mit der ausstellungsanweisung "Issue gemeinsam". Wenn sie mit der ausstellungsanweisung "hinzufügen" kombiniert wird, verfügt es nicht wirksam.  
  
    -   *Neuer Anspruch*: Dies anspruchseigenschaften einen neuen Anspruch angegebenen Werte verschiedener formatieren. Claim.Type muss angegeben werden. Alle anderen anspruchseigenschaften sind optional. Die Reihenfolge der Argumente für diese Art wird ignoriert.  
  
-   **Attributspeicher**– dieses Formulars erstellt Ansprüche mit Werten, die aus einem Attributspeicher abgerufen werden. Es ist möglich, erstellen Sie mehrere Anspruchstypen mithilfe einer einzelnen ausstellungsanweisung, die bei attributspeichern wichtig ist, die Netzwerk- oder Eingabe/Ausgabe (E/A) Vorgänge während des Aufrufs Attribut zu machen. Daher ist es wünschenswert sein, die Anzahl von Roundtrips zwischen dem Richtlinienmodul und dem Attributspeicher zu begrenzen. Es ist auch zulässig, mehrere Ansprüche für einen Anspruchstyp zu erstellen. Wenn der Attributspeicher mehrere Werte für einen Anspruchstyp zurückgibt, erstellt die ausstellungsanweisung automatisch einen Anspruch für jeden Anspruchswert. Eine Attribut Store-Implementierung verwendet die Parameterargumente Platzhalter im Abfrageargument durch Werte ersetzen, die in Parameterargumente bereitgestellt werden. Die Platzhalter verwenden dieselbe Syntax wie die Funktion .NET String.Format (z.B. {1}, {2}, usw.). Die Reihenfolge der Argumente für diese Art der Ausstellung ist wichtig, und es muss die in der folgenden Grammatik vorgeschriebene Reihenfolge sein.  
  
Die folgende Tabelle beschreibt einige allgemeine Syntaxkonstruktionen für beide ausstellungsanweisungen in Anspruchsregeln.  
  
|Ausstellungsanweisungstyp|Beschreibung der ausstellungsanweisung|Syntaxbeispiel für ausstellungsanweisung|  
|---------------------------|----------------------------------|-------------------------------------|  
|– Normal|Die folgende Regel gibt immer den gleichen Anspruch aus, wenn ein Benutzer den angegebenen Anspruchstyp und -Wert verfügt:|```c: [type  == "http://test/employee", value  == "true"] => issue (type = "http://test/role", value = "employee");```|  
|– Normal|Die folgende Regel konvertiert einen Anspruchstyp in einen anderen. Beachten Sie, dass der Wert des Anspruchs, der der Bedingung "c" entspricht in der ausstellungsanweisung verwendet wird.|```c: [type  == "http://test/group" ] => issue (type  = "http://test/role", value  = c.Value );```|  
|Attributspeicher|Die folgende Regel verwendet den Wert eines eingehenden Anspruchs, den Active Directory-Attributspeicher abzufragen:|```c: [Type  == "http://test/name" ] => issue (store  = "Enterprise AD Attribute Store", types  =  ("http://test/email" ), query  = ";mail;{0}", param  = c.Value )```|  
|Attributspeicher|Die folgende Regel verwendet den Wert eines eingehenden Anspruchs, um eine zuvor konfigurierte Structured Query Language (SQL)-Attributspeichers:|```c: [type  == "http://test/name"] => issue (store  = "Custom SQL store", types  =  ("http://test/email","http://test/displayname" ), query  = "SELECT mail, displayname FROM users WHERE name ={0}", param  = c.value );```|  
  
#### <a name="expressions"></a>Ausdrücke  
Ausdrücke werden auf der rechten Seite für die Ansprüche Selektor Einschränkungen und Ausstellung Anweisungsparameter verwendet. Es gibt verschiedene Arten von Ausdrücken, die die Sprache unterstützt. Alle Ausdrücke in der Sprache basieren auf Zeichenfolge, d.h., dass sie akzeptieren von Zeichenfolgen als Eingabe und Zeichenfolgen. Zahlen oder andere Datentypen wie beispielsweise Datum/Uhrzeit werden in Ausdrücken werden nicht unterstützt. Im folgenden sind die Arten von Ausdrücken, die die Sprache unterstützt:  
  
-   Zeichenfolgenliteral: Zeichenfolge, die von Anführungszeichen ('') auf beiden Seiten begrenzt.  
  
-   Verkettung von Ausdrücken als: das Ergebnis ist eine Zeichenfolge, die durch Verkettung der linken und rechten Werte erzeugt wird.  
  
-   Funktionsaufruf: die Funktion wird durch einen Bezeichner identifiziert, und die Parameter werden als ein Komma übergeben-durch Trennzeichen getrennte Liste von Ausdrücken, die in Klammern gesetzt ("()").  
  
-   Zugriff auf anspruchseigenschaften in Form einer Variablenname Punkt Eigenschaftenname: das Ergebnis der Wert der betreffenden anspruchseigenschaft. Die Variable muss zunächst an einen anspruchsselektor gebunden werden, bevor sie auf diese Weise verwendet werden kann. Es ist nicht zulässig, die Variable zu verwenden, die an einen anspruchsselektor in den Beschränkungen für die gleiche anspruchsselektor gebunden ist.  
  
Die folgenden anspruchseigenschaften sind verfügbar:  
  
-   Claim.Type  
  
-   Claim.Value  
  
-   Claim.Issuer  
  
-   Claim.OriginalIssuer  
  
-   Claim.ValueType  
  
-   Claim.Properties\[property\_name\] (diese Eigenschaft gibt eine leere Zeichenfolge, wenn die Eigenschaft dann zur Name in des Anspruchs gefunden werden kann. )  
  
Die RegexReplace-Funktion können Sie innerhalb eines Ausdrucks aufrufen. Diese Funktion übernimmt einen Eingabeausdruck und vergleicht ihn mit dem angegebenen Muster. Wenn das Muster übereinstimmt, wird die Ausgabe der Übereinstimmung durch den Ersatzwert ersetzt.  
  
#### <a name="exists-functions"></a>Funktionen vorhanden  
Die Exists-Funktion kann in einer Bedingung, ob ein Anspruch bewerten, entspricht die Bedingung in der Eingabe vorhanden eingabeanspruchssatz verwendet werden. Wenn übereinstimmende Ansprüche vorhanden ist, wird die ausstellungsanweisung nur einmal aufgerufen. Im folgenden Beispiel wird der Anspruch "Origin" genau einmal ausgegeben, wenn mindestens ein Anspruch in den eingabeanspruchssatz ein, die den Aussteller "MSFT" festgelegt ist, unabhängig davon, wie viele der Ansprüche der Aussteller legen Sie auf "MSFT". Mit dieser Funktion wird verhindert, dass doppelte Ansprüche ausgestellt werden.  
  
```  
exists([issuer == "MSFT"])  
   => issue(type = "origin", value = "Microsoft");  
```  
  
## <a name="rule-body"></a>Der Hauptteil Regel  
Der Hauptteil der Regel kann nur eine einzelne ausgabeanweisung enthalten. Wenn Bedingungen verwendet werden, ohne die Exists-Funktion zu verwenden, wird der Hauptteil der Regel einmal für jedes Mal ausgeführt, die der Bedingungsteil übereinstimmt.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Erstellen einer Regel zum Senden von Ansprüchen mit benutzerdefinierter Regel](https://technet.microsoft.com/library/dd807049.aspx)  
  

