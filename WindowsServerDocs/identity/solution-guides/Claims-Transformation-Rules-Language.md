---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: Sprache zum Schreiben von Regeln für die Transformation von Ansprüchen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a1f5c724d041a9f64c3b2697a8b5acd17a2a7bd9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445810"
---
# <a name="claims-transformation-rules-language"></a>Sprache zum Schreiben von Regeln für die Transformation von Ansprüchen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die gesamtstrukturübergreifende Ansprüche Transformation können Sie Bridge für die dynamische Zugriffssteuerung über Gesamtstrukturgrenzen hinweg, Ansprüche durch Festlegen von Transformationsrichtlinien für die für gesamtstrukturübergreifende Vertrauensstellungen für Ansprüche. Die primäre Komponente aller Richtlinien ist, die in Ansprüche Transformation Regeln Sprache geschrieben werden. Dieses Thema enthält Details zu dieser Sprache und enthält Anleitungen zum Erstellen von anspruchstransformationsregeln.  
  
Die Windows PowerShell-Cmdlets für die Transformation für Richtlinien für die gesamtstrukturübergreifende Vertrauensstellungen Optionen einfache Richtlinien festlegen, die sind in gängigen Szenarien müssen. Diese Cmdlets die Benutzereingabe Richtlinien und Regeln in der Ansprüche Transformation Regeln Sprache übersetzt, und klicken Sie dann in das vorgeschriebene Format in Active Directory speichern. Weitere Informationen zu den Cmdlets für die Transformation von Ansprüchen finden Sie unter den [AD DS-Cmdlets für die dynamische Zugriffssteuerung](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
Abhängig von der Konfiguration der Ansprüche und die Anforderungen für die gesamtstrukturübergreifende Vertrauensstellung in Ihrer Active Directory-Gesamtstrukturen platziert Ihre Ansprüche Transformationsrichtlinien möglicherweise komplexer als die Richtlinien, die von der Windows PowerShell-Cmdlets für Active unterstützt werden Das Verzeichnis. Um effektiv solcher Richtlinien zu erstellen, ist es wichtig, die Ansprüche Transformation Regeln Sprachsyntax und Semantik zu verstehen. Diese Ansprüche Transformation Regeln Sprache ("die Sprache") in Active Directory ist eine Teilmenge der Programmiersprache, mit dem [Active Directory Federation Services](https://go.microsoft.com/fwlink/?LinkId=243982) für ähnliche Zwecke, und es hat eine sehr ähnliche Syntax und Semantik verwendet. Allerdings stehen weniger Vorgänge zulässig, und zusätzliche Syntax Einschränkungen sind in der Active Directory-Version der Sprache.  
  
In diesem Thema wird kurz erläutert, die Syntax und Semantik der Ansprüche Transformation Regeln Sprache in Active Directory und Überlegungen beim Erstellen von Richtlinien vorgenommen werden. Es bietet mehrere Sätze von Beispielregeln können Sie sofort loslegen und Beispiele für falsche Syntax und die Nachrichten, die sie generieren, mit denen Sie die Fehlermeldungen zu entschlüsseln, wenn Sie die Regeln erstellen, die aus.  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>Tools zum Erstellen von Ansprüche-Transformationsrichtlinien  
**Windows PowerShell-Cmdlets für Active Directory**: Dies ist die bevorzugte und empfohlene Möglichkeit, zu erstellen und Ansprüche Transformationsrichtlinien. Diese Cmdlets Switches für einfache Richtlinien bereitstellen, und überprüfen die Regeln, die für eine komplexere Richtlinien festgelegt werden.  
  
**LDAP**: Richtlinien für die Transformation von Ansprüchen können in Active Directory über Lightweight Directory Access Protocol (LDAP) bearbeitet werden. Dies ist jedoch nicht empfohlen, da die Richtlinien mehrere komplexe Komponenten wurden und die Tools, mit denen Sie die Richtlinie vor dem Schreiben es in Active Directory können nicht überprüft werden. Dies erfordert möglicherweise anschließend viel Zeit, um Probleme zu diagnostizieren.  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory-Ansprüche Transformation Regeln Sprache  
  
### <a name="syntax-overview"></a>Übersicht über die Syntax  
Hier ist eine kurze Übersicht über die Syntax und Semantik der Sprache:  
  
-   Die Menge der Ausgabeansprüche Transformation Regel besteht aus null oder mehr Regeln. Jede Regel verfügt über zwei aktive Teilen: **Wählen Sie die Liste der Bedingungen** und **Regelaktion**. Wenn die **Select-Liste von Bedingung** zu TRUE ausgewertet, die entsprechende Regelaktion ausgeführt wird.  
  
-   **Wählen Sie die Liste der Bedingungen** verfügt über 0 (null) oder mehr **Bedingungen wählen**. Alle der **Bedingungen auswählen** für "true" ergeben muss die **Select-Liste von Bedingung** zu "true" ausgewertet werden soll.  
  
-   Jede **Bedingung auswählen** verfügt über einen Satz von NULL oder mehr **Bedingungen für die Übereinstimmung**. Alle der **Bedingungen für die Übereinstimmung** muss für die Bedingung wählen Sie auf "true" ergibt "true" ausgewertet. Alle diese Bedingungen werden für ein einzelner Anspruch ausgewertet. Einen Anspruch, eine **Bedingung auswählen** können gekennzeichnet werden, indem ein **Bezeichner** bezeichnet, in der **Regelaktion**.  
  
-   Jede **Bedingung übereinstimmenden** gibt die Bedingung entsprechend der **Typ** oder **Wert** oder **ValueType** des Anspruchs mit verschiedenen  **Operatoren für die erste Bedingung** und **Zeichenfolgenliterale**.  
  
    -   Bei Angabe einer **Bedingung übereinstimmenden** für eine **Wert**, müssen Sie auch angeben eine **Bedingung übereinstimmenden** für einen bestimmten **ValueType** und umgekehrt. Diese Bedingungen müssen nebeneinander in der Syntax sein.  
  
    -   **ValueType** übereinstimmungsbedingungen muss bestimmte verwenden **ValueType** nur Literale.  
  
-   Ein **Regelaktion** können kopieren, einen Anspruch, der mit gekennzeichnet ist ein **Bezeichner** oder geben Sie einen Anspruch, basierend auf einen Anspruch, der mit einer ID gekennzeichnet ist, und/oder Zeichenfolgenliterale angegeben.  
  
**Beispielregel**  
  
Dieses Beispiel zeigt eine Regel, die verwendet werden kann, um die Ansprüche Typ zwischen zwei Gesamtstrukturen zu übersetzen, vorausgesetzt, sie dieselben Ansprüche Werttypen verwenden und die gleichen Interpretationen für die forderungs-Werte für diesen Typ. Die Regel verfügt über eine entsprechende Bedingung und eine Problem-Anweisung, die Zeichenfolgenliterale und einem übereinstimmenden Ansprüche-Verweis verwendet.  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>Runtime-Vorgang  
Es ist wichtig zu verstehen, die Runtime-Vorgang von Transformationen von Ansprüchen zum effektiven Regeln zu erstellen. Die Runtime-Vorgang verwendet drei Sätze von Ansprüchen:  
  
1.  **Satz von Ansprüchen Eingabe**: Der Eingabe Satz von Ansprüchen, die für den Betrieb der Ansprüche Transformation angegeben werden.  
  
2.  **Verwenden die Menge der Ausgabeansprüche**: Intermediate Ansprüche, die aus gelesen und geschrieben während die Transformation von Ansprüchen.  
  
3.  **Ausgabe von Ansprüchen Satz**: Die Ausgabe des Vorgangs Transformation Ansprüche.  
  
Hier ist eine kurze Übersicht über die Common Language Runtime Ansprüche Datentransformation:  
  
1.  Eingabeansprüche für die Transformation von Ansprüchen werden verwendet, um das Workingset-Ansprüche zu initialisieren.  
  
    1.  Bei der Verarbeitung jeder Regel wird das Workingset-Ansprüche für den Eingabeansprüchen verwendet.  
  
    2.  Die Auswahlliste für die Bedingung in einer Regel ist mit allen möglichen Sätze von Ansprüchen, aus dem Arbeitssatz der Ansprüche verglichen.  
  
    3.  Jeder Satz übereinstimmender Ansprüche dient zum Ausführen der Aktion in dieser Regel.  
  
    4.  Die Ausführung einer Regel Aktionsergebnisse in einen Anspruch, der mit der Ausgabe angefügt wird beansprucht, Gruppe und die Menge der Ausgabeansprüche arbeiten. Daher ist die Ausgabe von einer Regel für die nachfolgenden Regeln im Regelsatz als Eingabe verwendet.  
  
2.  Die Regeln im Regelsatz werden in sequenzieller Reihenfolge, beginnend mit der ersten Regel verarbeitet.  
  
3.  Wenn der gesamte Regelsatz verarbeitet wird, wird die Menge der Ausgabeansprüche verarbeitet, um doppelte Ansprüche zu entfernen und für andere Sicherheitsrisiken. Die resultierenden Ansprüchen handelt es sich um die Ausgabe einer Transformation Ansprüche.  
  
Es ist möglich, Schreiben komplexer Anspruchstransformationen auf die Laufzeit das vorherige Verhalten basieren.  
  
**Beispiel: Runtime-Vorgang**  
  
Dieses Beispiel zeigt den Runtime-Vorgang, der eine Transformation von Ansprüchen, die zwei Regeln verwendet.  
  
```  
  
     C1:[Type=="EmpType", Value=="FullTime",ValueType=="string"] =>  
                Issue(Type=="EmployeeType", Value=="FullTime",ValueType=="string");  
     [Type=="EmployeeType"] =>   
               Issue(Type=="AccessType", Value=="Privileged", ValueType=="string");  
Input claims and Initial Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"),(Value="Marketing"),(ValueType="String")}  
After Processing Rule 1:  
 Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"), (Value="Marketing"),(ValueType="String")}  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
Output Context:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  
After Processing Rule 2:  
Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"),(Value="Marketing"),(ValueType="String")}  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
Output Context:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
  
Final Output:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
  
```  
  
### <a name="special-rules-semantics"></a>Spezielle Regeln-Semantik  
Im folgenden finden spezielle Syntax für die Regeln:  
  
1.  Leere Regelsatz keine Ausgabeansprüche ==  
  
2.  Leere Select-Liste von Bedingung == alle Anspruch entspricht der Liste der Bedingungen auswählen  
  
    **Beispiel: Leere Option Bedingungsliste**  
  
    Die folgende Regel entspricht jeden Anspruch in das Workingset.  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  Wählen Sie übereinstimmende Liste leer == jeder Anspruch entspricht der Liste der Bedingungen auswählen  
  
    **Beispiel: Bedingungen für die leere Übereinstimmung**  
  
    Die folgende Regel entspricht jeden Anspruch in das Workingset. Dies ist die grundlegende "Allow-All"-Regel, wenn es allein verwendet wird.  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>Sicherheitsüberlegungen  
**Ansprüche, die eine Gesamtstruktur eingeben**  
  
Die bereitgestellten von Prinzipalen, die in einer Gesamtstruktur eingehenden Ansprüche müssen sorgfältig überprüft werden muss, um sicherzustellen, dass wir zulassen, oder geben Sie nur die Richtigkeit der Ansprüche. Nicht ordnungsgemäße Ansprüche können der Gesamtstruktur die Sicherheit beeinträchtigen, und Dies dürfte eine wichtige Rolle beim Erstellen von Transformationsrichtlinien für die für Ansprüche, die eine Gesamtstruktur eingeben.  
  
Active Directory verfügt über die folgenden Funktionen aus, um zu verhindern, dass die Fehlkonfiguration von Ansprüchen, die eine Gesamtstruktur eingeben:  
  
-   Wenn eine Gesamtstruktur-Vertrauensstellung ist keine Ansprüche Transformation Richtliniensatz für die Ansprüche, die eine Gesamtstruktur, für die Sicherheit zu erhöhen, geben Sie löscht Active Directory die principal Ansprüche, die die Gesamtstruktur eingeben.  
  
-   Wenn den Regelsatz auf Ansprüchen ausgeführt, der eine Gesamtstruktur-Ergebnisse in Ansprüchen eingibt, die nicht in der Gesamtstruktur definiert sind, werden die nicht definierten Ansprüche aus die Ausgabeansprüche gelöscht.  
  
**Ansprüche, die verlassen eine Gesamtstruktur**  
  
Ansprüche, die verlassen eine Gesamtstruktur vorhanden, weniger Sicherheit wichtig ist für die Gesamtstruktur als die Ansprüche, die die Gesamtstruktur eingeben. Ansprüche können die Gesamtstruktur wie der lassen – ist, auch wenn keine entsprechenden Ansprüche transformationsrichtlinie vorhanden. Es ist auch möglich, die Ansprüche ausgeben, die nicht, in der Gesamtstruktur als Teil definiert sind der Transformation von Ansprüchen, die von der Gesamtstruktur zu lassen. Dies ist ganz einfach einrichten gesamtstrukturübergreifende Vertrauensstellungen mit Ansprüchen. Ein Administrator kann bestimmen, ob Ansprüche, die die Gesamtstruktur eingeben müssen, transformiert und die entsprechende Richtlinie einrichten werden. Beispielsweise kann ein Administrator eine Richtlinie festlegen, wenn besteht die Notwendigkeit, einen Anspruch, um die Offenlegung von Informationen ausblenden.  
  
**Syntaxfehler im Transformationsregeln für Ansprüche**  
  
Wenn eine bestimmte Ansprüche Transformation-Richtlinie verfügt über einen Regelsatz, der syntaktisch falsch ist, oder wenn andere Probleme Syntax oder Speicher vorliegen, die Richtlinie ist ungültig. Dies ist anders als die oben genannten standardbedingungen behandelt.  
  
Active Directory kann nicht das Ziel in diesem Fall ermitteln und wechselt in den ein Abgesicherter Modus, wodurch keine Ausgabeansprüche generiert werden, auf diese Vertrauensstellung und die Richtung des Durchlaufs. Eingreifen des Administrators ist erforderlich, um das Problem zu beheben. Dies kann passieren, wenn LDAP verwendet wird, um die Ansprüche Transformation-Richtlinie zu bearbeiten. Windows PowerShell-Cmdlets für Active Directory haben Validierung, um zu verhindern, schreiben eine Richtlinie mit Syntaxfehler.  
  
## <a name="other-language-considerations"></a>Andere sprachbezogene Aspekte  
  
1.  Es gibt mehrere Schlüsselwörter oder Zeichen an, die in dieser Sprache (bezeichnet als Terminals) besonders sind. Diese werden angezeigt, der [Sprache Terminals](Claims-Transformation-Rules-Language.md#BKMK_LT) Tabelle weiter unten in diesem Thema. Die Fehlermeldungen werden die Tags für diese Terminals für Mehrdeutigkeit verwenden.  
  
2.  Terminale können manchmal als Zeichenfolgenliterale verwendet werden. Jedoch solche Nutzung zu Konflikten mit der Sprachdefinition oder haben möglicherweise unerwartete Ergebnisse liefern. Diese Art von Auslastung wird nicht empfohlen.  
  
3.  Die Regelaktion kann ausführen, typkonvertierungen Anspruchswerte und ein Regelsatz, der eine solche Regelaktion enthält, wird als ungültig angesehen. Dies würde dazu führen, dass einen Laufzeitfehler, und es werden keine Ausgabeansprüche generiert.  
  
4.  Wenn eine Regelaktion auf einen Bezeichner, die nicht in der Select-Liste von Bedingung Teil der Regel verwendet wurde verweist, ist es eine ungültige Verwendung. Dies würde dazu führen, dass ein Syntaxfehler aufgetreten.  
  
    **Beispiel: Falscher Verweis für Bezeichner**  
    Die folgende Regel zeigt nicht den korrekten Bezeichner, die in einer Regelaktion verwendet.  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>Beispiel-Transformationsregeln  
  
-   **Alle Ansprüche eines bestimmten Typs zu ermöglichen**  
  
    Exakten Typ  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    Mithilfe von Regex  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **Verweigert einen bestimmten Anspruchstyp**  
    Exakten Typ  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    Mithilfe von Regex  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>Beispiele für Regeln Parser-Fehler  
Transformationsregeln für Ansprüche werden durch einen benutzerdefinierten Parser überprüft auf Syntaxfehler analysiert. Dieser Parser wird von zugehörigen Windows PowerShell-Cmdlets ausgeführt, bevor Regeln in Active Directory gespeichert. Fehler bei der Analyse Syntaxfehler, einschließlich der Regeln werden in der Konsole ausgegeben. Domänencontroller den Parser auch vor der Verwendung von Regeln zum Transformieren von Ansprüchen ausgeführt, und sie Fehler im Ereignisprotokoll protokollieren (Hinzufügen von Ereignisprotokoll Zahlen).  
  
In diesem Abschnitt sind einige Beispiele für Regeln, die Fehler mit falscher Syntax und die entsprechende Syntax geschrieben werden, die vom Parser generiert werden.  
  
1. Beispiel:  
  
   ```  
   c1;[]=>Issue(claim=c1);  
   ```  
  
   In diesem Beispiel hat ein falsch verwendeter Semikolon anstelle von einem Doppelpunkt.   
   **Fehlermeldung:**  
   *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
   *Zeilennummer: 1, Spaltennummer: 2, fehlertoken:;. Line: 'c1;[]=>Issue(claim=c1);'.*  
   *Fehler im Parser: "POLICY0030: Syntaxfehler: Unerwartetes ';', erwartet eine der folgenden: ":". "*  
  
2. Beispiel:  
  
   ```  
   c1:[]=>Issue(claim=c2);  
   ```  
  
   In diesem Beispiel ist das Tag "Bezeichner" in der ausstellungsanweisung kopieren nicht definiert.   
   **Fehlermeldung**:   
   *POLICY0011: Keine Bedingungen in der Anspruchsregel mit dem die Bedingungstag, die in der CopyIssuanceStatement angegeben: "c2".*  
  
3. Beispiel:  
  
   ```  
   c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
   ```  
  
   "Bool" ist nicht mit einem Terminal aus, in der Sprache, und es ist dabei nicht um eine gültige ValueType. Gültige Terminals werden in der folgenden Fehlermeldung aufgeführt.   
   **Fehlermeldung:**  
   *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
   Zeilennummer: 1, Spaltennummer: 39, fehlertoken: "Bool". Line: 'c1:[type=="x1", value=="1",valuetype=="bool"]=>Issue(claim=c1);'.   
   *Fehler im Parser: "POLICY0030: Syntaxfehler: Unerwartetes 'STRING', erwartet eine der folgenden: 'INT64_TYPE' 'UINT64_TYPE' 'STRING_TYPE' 'BOOLEAN_TYPE' 'IDENTIFIER'*  
  
4. Beispiel:  
  
   ```  
   c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
   ```  
  
   Die Zahl **1** in diesem Beispiel ist kein gültiges Token in der Sprache, und die Nutzung ist in einer übereinstimmungsbedingung nicht zulässig. Er muss in doppelte Anführungszeichen ein, um es zu eine Zeichenfolge machen eingeschlossen werden.   
   **Fehlermeldung:**  
   *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
   *Zeilennummer: 1, Spaltennummer: 23 fehlertoken: 1. Line: 'c1:[type=="x1", value==1, valuetype=="bool"]=>Issue(claim=c1);'.* <em>Parser error: "POLICY0029: Unerwartete Eingabe.</em>  
  
5. Beispiel:  
  
   ```  
   c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
        Issue(type = c1.type, value="0", valuetype == "boolean");  
   ```  
  
   Dieses Beispiel verwendet ein doppeltes Gleichheitszeichen (==), anstatt ein einzelnes Gleichheitszeichen (=).   
   **Fehlermeldung:**  
   *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
   *Zeilennummer: 1, Spaltennummer: 91, fehlertoken: ==. Line: 'c1:[type=="x1", value=="1",*  
   *valuetype=="boolean"]=>Issue(type=c1.type, value="0", valuetype=="boolean");'.*  
   *Fehler im Parser: "POLICY0030: Syntaxfehler, unerwartetes "==", eine der folgenden erwartet: '='*  
  
6. Beispiel:  
  
   ```  
   c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
         Issue(type=c1.type, value=c1.value, valuetype = "string");  
   ```  
  
   In diesem Beispiel ist syntaktisch und semantisch richtig. Verwenden jedoch "Boolean" auf, wie Sie ein Zeichenfolgenwert an für Verwirrung sorgen, gebunden ist, und sollte vermieden werden. Wie bereits erwähnt, mithilfe der Sprache Terminals wie Ansprüche Werte sollten möglichst vermieden werden.  
  
## <a name="BKMK_LT"></a>Language-terminals  
Die folgende Tabelle enthält den vollständigen Satz von Terminaldienste-Zeichenfolgen und die zugeordnete Sprache-Terminals, die in der Ansprüche Transformation Regeln Sprache verwendet werden. Diese Definitionen werden Groß-/Kleinschreibung UTF-16-Zeichenfolgen verwenden.  
  
|Zeichenfolge|Terminaldienste|  
|----------|------------|  
|"=>"|IMPLIZIEREN|  
|";"|DURCH SEMIKOLONS|  
|":"|DOPPELPUNKT|  
|","|COMMA|  
|"."|PUNKT|  
|"["|O_SQ_BRACKET|  
|"]"|C_SQ_BRACKET|  
|"("|O_BRACKET|  
|")"|C_BRACKET|  
|"=="|EQ|  
|"!="|NEQ|  
|"=~"|REGEXP_MATCH|  
|"!~"|REGEXP_NOT_MATCH|  
|"="|WEISEN SIE|  
|"&&"|AND|  
|"Issue"|PROBLEM|  
|"Type"|TYPE|  
|"Value"|WERT|  
|"Valuetype"|VALUE_TYPE|  
|"claim"|ANSPRUCH|  
|"[_A-Za-z][_A-Za-z0-9]*"|BEZEICHNER|  
|"\\" [^\\"\n]*\\" "|ZEICHENFOLGE|  
|"uint64"|UINT64_TYPE|  
|"int64"|INT64_TYPE|  
|"string"|STRING_TYPE|  
|"boolean"|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>Sprachsyntax  
Die folgenden Ansprüche Transformation Regeln Sprache wird in ABNF Formular angegeben. Diese Definition verwendet die Terminals, die in der vorherigen Tabelle zusätzlich zu den hier definierten ABNF Produktionen angegeben werden. Die Regeln in UTF-16 codiert werden müssen, und der Vergleich von Zeichenfolgen müssen Groß-/Kleinschreibung behandelt werden.  
  
```  
Rule_set        = ;/*Empty*/  
             / Rules  
Rules         = Rule  
             / Rule Rules  
Rule          = Rule_body  
Rule_body       = (Conditions IMPLY Rule_action SEMICOLON)  
Conditions       = ;/*Empty*/  
             / Sel_condition_list  
Sel_condition_list   = Sel_condition  
             / (Sel_condition_list AND Sel_condition)  
Sel_condition     = Sel_condition_body  
             / (IDENTIFIER COLON Sel_condition_body)  
Sel_condition_body   = O_SQ_BRACKET Opt_cond_list C_SQ_BRACKET  
Opt_cond_list     = /*Empty*/  
             / Cond_list  
Cond_list       = Cond  
             / (Cond_list COMMA Cond)  
Cond          = Value_cond  
             / Type_cond  
Type_cond       = TYPE Cond_oper Literal_expr  
Value_cond       = (Val_cond COMMA Val_type_cond)  
             /(Val_type_cond COMMA Val_cond)  
Val_cond        = VALUE Cond_oper Literal_expr  
Val_type_cond     = VALUE_TYPE Cond_oper Value_type_literal  
claim_prop       = TYPE  
             / VALUE  
Cond_oper       = EQ  
             / NEQ  
             / REGEXP_MATCH  
             / REGEXP_NOT_MATCH  
Literal_expr      = Literal  
             / Value_type_literal  
  
Expr          = Literal  
             / Value_type_expr  
             / (IDENTIFIER DOT claim_prop)  
Value_type_expr    = Value_type_literal  
             /(IDENTIFIER DOT VALUE_TYPE)  
Value_type_literal   = INT64_TYPE  
             / UINT64_TYPE  
             / STRING_TYPE  
             / BOOLEAN_TYPE  
Literal        = STRING  
Rule_action      = ISSUE O_BRACKET Issue_params C_BRACKET  
Issue_params      = claim_copy  
             / claim_new  
claim_copy       = CLAIM ASSIGN IDENTIFIER  
claim_new       = claim_prop_assign_list  
claim_prop_assign_list = (claim_value_assign COMMA claim_type_assign)  
             /(claim_type_assign COMMA claim_value_assign)  
claim_value_assign   = (claim_val_assign COMMA claim_val_type_assign)  
             /(claim_val_type_assign COMMA claim_val_assign)  
claim_val_assign    = VALUE ASSIGN Expr  
claim_val_type_assign = VALUE_TYPE ASSIGN Value_type_expr  
Claim_type_assign   = TYPE ASSIGN Expr  
  
```  
  


