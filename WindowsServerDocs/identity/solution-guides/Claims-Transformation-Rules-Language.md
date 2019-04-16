---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: "Ansprüche Transformation Regeln Sprache"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4a6b378bc4aef180ebedd260008febaa2f2a76ae
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="claims-transformation-rules-language"></a>Ansprüche Transformation Regeln Sprache

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die gesamtstrukturübergreifende Ansprüche Transformation Feature können Sie die Brücke für die dynamische Zugriffssteuerung gesamtstrukturübergreifend Ansprüche durch Festlegen von Ansprüche Transformation Richtlinien für gesamtstrukturübergreifende Vertrauensstellung. Die primäre Komponente aller Richtlinien werden Regeln, die in Ansprüche Transformation Regeln Sprache geschrieben sind. Dieses Thema enthält ausführliche Informationen zu dieser Sprache und bietet eine Anleitung zum Erstellen von Regeln für die Transformation von Ansprüchen.  
  
Windows PowerShell-Cmdlets für die Transformation von Richtlinien auf gesamtstrukturübergreifende Vertrauensstellungen Optionen einfache Richtlinien festlegen, die gemeinsam Szenarien erforderlich sind. Diese Cmdlets die Benutzereingabe in Richtlinien und Regeln in der Ansprüche Transformation Regeln Sprache übersetzen, und klicken Sie dann in das vorgeschriebene Format in Active Directory gespeichert. Weitere Informationen zu Cmdlets für die Transformation von Ansprüchen finden Sie unter der [AD DS-Cmdlets für die dynamische Zugriffssteuerung](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
Je nach der Konfiguration von Ansprüchen und die Anforderungen für die gesamtstrukturübergreifende Vertrauensstellung in Ihrer Active Directory-Gesamtstrukturen platziert möglicherweise Ihre Ansprüche Transformation Richtlinien komplexer als die Richtlinien, die von Windows PowerShell-Cmdlets für Active Directory unterstützt werden. Um solche Richtlinien effektiv zu erstellen, ist es wichtig zu verstehen, die Ansprüche Transformation Regeln Sprachsyntax und Semantik. Diese Ansprüche Transformation Regeln Sprache ("die Sprache") in Active Directory ist eine Teilmenge der Sprache, mit dem [Active Directory Federation Services](https://go.microsoft.com/fwlink/?LinkId=243982) für ähnliche Zwecke, und es hat eine sehr ähnliche Syntax und Semantik. Allerdings gibt es weniger Vorgänge zulässig sind, und zusätzliche Syntax Einschränkungen befinden sich in der Active Directory-Version der Sprache.  
  
In diesem Thema wird kurz erläutert, die Syntax und Semantik der Ansprüche Transformation Regeln Sprache in Active Directory und Überlegungen beim Erstellen von Richtlinien getroffen werden. Es enthält mehrere Sätze von Beispielregeln, um Ihnen den Einstieg und Beispiele für Ungültige Syntax und die Nachrichten, die sie generieren können Sie die Fehlermeldungen zu entschlüsseln, wenn Sie die Regeln erstellen.  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>Tools zum Erstellen von Richtlinien für Ansprüche transformation  
**Windows PowerShell-Cmdlets für Active Directory**: Dies ist die bevorzugte und empfohlene Möglichkeit zum Erstellen und Ansprüche Transformation Richtlinien festlegen. Diese Cmdlets Switches für einfache Richtlinien bereitstellen, und überprüfen Sie die Regeln, die für komplexere Richtlinien festgelegt werden.  
  
**LDAP**: Ansprüche Transformation Richtlinien in Active Directory über Lightweight Directory Access Protocol (LDAP) bearbeitet werden können. Dies ist jedoch nicht empfohlen, da die Richtlinien mehrere komplexe Komponenten, und die Tools, mit denen die Richtlinie vor dem Schreiben in Active Directory können nicht überprüft werden. Dies erfordert möglicherweise später viel Zeit zur Diagnose von Problemen.  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory-Ansprüche Transformation Regeln Sprache  
  
### <a name="syntax-overview"></a>Syntax (Übersicht)  
Nachfolgend finden Sie eine kurze Übersicht über die Syntax und Semantik der Sprache:  
  
-   Ansprüche Transformation Regelsatz besteht aus null oder mehr Regeln. Jede Regel besteht aus zwei aktive Teilen: **Bedingungsliste wählen** und **Regelaktion**. Wenn die **Bedingungsliste wählen** "Wahr" ergibt, wird die entsprechende Regelaktion ausgeführt.  
  
-   **Wählen Sie die Liste der Bedingungen** ist NULL oder mehr **auswählen Bedingungen**. Alle der **wählen Bedingungen** für "true" ergeben muss die **Bedingungsliste auswählen** zu TRUE ausgewertet wird.  
  
-   Jede **Bedingung auswählen** hat eine Reihe von NULL oder mehr **übereinstimmenden Bedingungen**. Alle der **übereinstimmenden Bedingungen** für die Bedingung auswählen, wird "Wahr" ergibt "true" ergeben muss. Alle diese Bedingungen sind ein einzelner Anspruch ausgewertet. Einen Anspruch, der entspricht einer **Bedingung auswählen** gekennzeichnet sein können, indem Sie eine **Bezeichner** und gemäß der **Regelaktion**.  
  
-   Jede **Bedingung übereinstimmenden** gibt die Bedingung entsprechend der **Typ** oder **Wert** oder **ValueType** eines Anspruchs mit verschiedenen **Bedingungsoperatoren** und **Zeichenfolgenliterale**.  
  
    -   Bei der Angabe einer **übereinstimmende Bedingung** für eine **Wert**, müssen Sie auch angeben eine **übereinstimmende Bedingung** für einen bestimmten **ValueType** und umgekehrt. Diese Bedingung muss nebeneinander in der Syntax.  
  
    -   **ValueType** übereinstimmenden Bedingungen muss bestimmte verwenden **ValueType** nur Literale.  
  
-   Ein **Regelaktion** können einen Anspruch, der mit markiert ist, kopieren Sie eine **Bezeichner** oder einem Anspruch basierend auf eine Anforderung, die mit einer Kennung markiert ist, bzw. angegebenen Zeichenfolgenliterale ausstellt.  
  
**Beispielregel**  
  
Dieses Beispiel zeigt eine Regel, die die Ansprüche Typ zwischen zwei Gesamtstrukturen, übersetzen, vorausgesetzt, sie die gleichen Ansprüche Werttypen verwenden und verfügen über die gleichen Interpretationen für Ansprüche Werte für diesen Typ verwendet werden kann. Die Regel verfügt über eine Bedingung und eine Problem-Anweisung, die Zeichenfolgenliterale und eine übereinstimmende Ansprüche Referenz verwendet.  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>Runtime-Vorgang  
Es ist wichtig zu verstehen, die Runtime-Vorgang Anspruchstransformationen effektiv die Regeln zu erstellen. Die Runtime-Vorgang verwendet drei Gruppen von Ansprüchen:  
  
1.  **Eingabe Ansprüche Set**: die Eingabe Satz von Ansprüchen, die für den Betrieb der Ansprüche Transformation angegeben werden.  
  
2.  **Funktioniert Ansprüche Set**: Zwischenzertifizierungsstellen Ansprüche, die von gelesen und geschrieben während die Transformation von Ansprüchen.  
  
3.  **Set-Ausgabe Ansprüche**: Ausgabe des Vorgangs Transformation von Ansprüchen.  
  
Hier ist eine kurze Übersicht über die Common Language Runtime Ansprüche Transformation Operation:  
  
1.  Eingabeansprüche für die Transformation von Ansprüchen wird Workingsets Ansprüche zu initialisieren.  
  
    1.  Bei der Verarbeitung von jeder Regel wird Workingsets Ansprüche für den Eingabeansprüchen verwendet.  
  
    2.  Die Bedingung Auswahlliste in einer Regel wird mit alle möglichen Sätze von Ansprüchen aus den Arbeitsseiten Ansprüche verglichen.  
  
    3.  Jeden Satz übereinstimmender Ansprüche dient zum Ausführen der Aktion in der Regel.  
  
    4.  Die Ausführung einer Regel Aktionsergebnisse in einem Anspruch, Ansprüche der an die Ausgabe angefügt wird, und die Arbeit Ansprüche. Daher wird die Ausgabe einer Regel als Eingabe für die nachfolgenden Regeln im Regelsatz verwendet.  
  
2.  In sequenzieller Reihenfolge beginnend mit der ersten Regel werden die Regeln im Regelsatz verarbeitet.  
  
3.  Wenn der gesamte Regelsatz verarbeitet wird, wird die Menge der Ausgabeansprüche verarbeitet, um doppelte Ansprüche zu entfernen und für andere Sicherheitsrisiken. Die resultierende Ansprüche sind die Ausgabe einer Transformation von Ansprüchen.  
  
Es ist möglich, Schreiben Sie komplexe Anspruchstransformationen auf das vorherige Verhalten von Runtime basieren.  
  
**Beispiel:-Runtime-Vorgang**  
  
Dieses Beispiel zeigt die Runtime-Vorgang von einer Transformation von Ansprüchen, die zwei Regeln verwendet.  
  
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
  
### <a name="special-rules-semantics"></a>Spezielle Regeln Semantik  
Im folgenden finden spezielle Syntax für Regeln:  
  
1.  Leeren Regelsatz == keine Ausgabe Ansprüche  
  
2.  Bedingungsliste leeren == jeder Anspruch entspricht der Liste der Bedingung auswählen  
  
    **Beispiel: Leere wählen Bedingungsliste**  
  
    Die folgende Regel entspricht jedes Anspruchs in den Arbeitsseiten.  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  Leeren übereinstimmenden Liste wählen == jedes Anspruchs entspricht der Liste der Bedingung auswählen  
  
    **Beispiel: Leere übereinstimmenden Bedingungen**  
  
    Die folgende Regel entspricht jedes Anspruchs in den Arbeitsseiten. Dies ist die grundlegende "Allow All"-Regel, wenn es allein verwendet wird.  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>Überlegungen zur Sicherheit  
**Ansprüche, die eine Gesamtstruktur eingeben**  
  
Die von Prinzipalen, die in einer Gesamtstruktur eingehenden Ansprüche müssen gründlich überprüft werden, um sicherzustellen, dass wir gewähren oder nur die richtige Ansprüche ausgeben. Falsche Ansprüche die Gesamtstruktur-Sicherheit gefährden können sollte, und dies eine Rolle spielt beim Erstellen von Richtlinien der Transformation für Ansprüche, die eine Gesamtstruktur eingeben.  
  
Active Directory bietet die folgenden Features Fehlkonfiguration von Ansprüchen zu verhindern, die eine Gesamtstruktur eingeben:  
  
-   Wenn eine Gesamtstruktur-Vertrauensstellung ist keine Ansprüche Transformation Richtlinie für die Ansprüche, die eine Gesamtstruktur, für die Sicherheit zu erhöhen, geben Sie löscht Active Directory die Dienstprinzipalnamen Ansprüche, die die Gesamtstruktur eingeben.  
  
-   Wenn die Regel auf Ansprüche ausgeführt, die eine Gesamtstruktur Ergebnisse Ansprüche eingibt, die nicht in der Gesamtstruktur definiert sind, werden die undefined Ansprüche aus die Ausgabe Ansprüche gelöscht.  
  
**Ansprüche, die verlassen eine Gesamtstruktur**  
  
Ansprüche, die verlassen eine Gesamtstruktur stellen eine geringere Sicherheitsbedenken für die Gesamtstruktur als die Ansprüche, die die Gesamtstruktur eingeben. Ansprüche können die Gesamtstruktur als lassen – selbst wenn keine entsprechenden Ansprüche Transformation Richtlinie vorhanden ist. Es ist auch möglich, Ansprüche ausgeben, die nicht in der Gesamtstruktur als Teil der Transformation von Ansprüchen, die die Gesamtstruktur lassen definiert sind. Dies ist auf einfache Weise gesamtstrukturübergreifende Vertrauensstellung mit Ansprüchen erstellen. Ein Administrator kann erkennen, ob Ansprüche, die die Gesamtstruktur eingeben müssen transformiert werden, und richten Sie die entsprechende Richtlinie. Beispielsweise kann ein Administrator eine Richtlinie festlegen, wenn zum Ausblenden von Ansprüchen zum Verhindern der informationsoffenlegung von müssen.  
  
**Syntaxfehler in Ansprüche Transformationsregeln**  
  
Wenn eine bestimmte Ansprüche Transformation Richtlinie hat einen Satz von Regeln, der Syntax falsch ist oder wenn andere Syntax oder Speicher Probleme vorliegen, die Richtlinie ist ungültig. Dies ist anders als die standardbedingungen, die bereits erwähnten behandelt.  
  
Active Directory ist nicht in diesem Fall ermittelt die Absicht und wechselt in ein Abgesicherter Modus, wo keine Ansprüche Ausgabe erzeugt auf diese Vertrauensstellung + Richtung des Durchlaufs. Ein Eingreifen des Administrators ist erforderlich, um dieses Problem zu beheben. Dies kann passieren, wenn LDAP verwendet wird, um die Ansprüche Transformation Richtlinie bearbeiten. Windows PowerShell-Cmdlets für Active Directory verfügen über Überprüfung um zu verhindern, dass eine Richtlinie hinsichtlich Syntax schreiben.  
  
## <a name="other-language-considerations"></a>Weitere Aspekte der Sprache  
  
1.  Es gibt mehrere Schlüssel Worte oder Zeichen, die in dieser Sprache (als Terminals bezeichnet) sind. Diese werden angezeigt, dem [Sprache Terminals](Claims-Transformation-Rules-Language.md#BKMK_LT) Tabelle weiter unten in diesem Thema. Die Fehlermeldungen verwenden Sie die Tags für diese Terminals zur Klärung.  
  
2.  Terminals können manchmal als Zeichenfolgenliterale verwendet werden. Jedoch eine solche Verwendung im Konflikt mit der Sprachdefinition oder haben möglicherweise unerwartete Ergebnisse. Diese Art der Verwendung von wird nicht empfohlen.  
  
3.  Die Aktion kann keine typkonvertierungen führen Sie auf Anspruchswerte und ein Regelsatz, der eine solche Regelaktion enthält ist ungültig. In diesem Fall einen Laufzeitfehler und keine Ansprüche Ausgabe erzeugt werden.  
  
4.  Wenn eine Aktion für einen Bezeichner, die nicht in der Liste der Bedingung auswählen Teil der Regel verwendet wurde bezieht, handelt es sich um eine ungültige Verwendung. Dies würde dazu führen, dass einen Fehler.  
  
    **Beispiel: Falsche ID-Verweis**  
    Die folgende Regel zeigt nicht den korrekten Bezeichner in Aktion verwendet.  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>Beispiel für die Transformationsregeln  
  
-   **Alle Ansprüche eines bestimmten Typs zulassen**  
  
    Genaue Typ  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    Verwendung von Regex  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **Verbieten Sie einen bestimmten Anspruchstyp**  
    Genaue Typ  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    Verwendung von Regex  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>Beispiele für Fehlermeldungen Regeln  
Ansprüche Transformationsregeln werden durch einen benutzerdefinierten Parser überprüft auf Syntaxfehler analysiert. Dieser Parser wird von zugehörigen Windows PowerShell-Cmdlets ausgeführt, bevor Regeln in Active Directory gespeichert. Fehler bei der Analyse der Regeln einschließlich Syntaxfehler enthält, werden auf der Konsole ausgegeben. Domänencontroller den Parser auch vor der Verwendung von der Regeln für die Transformation von Ansprüchen ausführen, und sie Fehler im Ereignisprotokoll protokollieren (Ereignisprotokoll Zahlen hinzufügen).  
  
In diesem Abschnitt werden einige Beispiele für Regeln, die Fehler mit falscher Syntax und die entsprechende Syntax geschrieben werden, die vom Parser generiert werden.  
  
1.  Beispiel:  
  
    ```  
    c1;[]=>Issue(claim=c1);  
    ```  
  
    In diesem Beispiel hat ein falsch verwendeten Semikolon anstelle von einem Doppelpunkt.   
    **Fehlermeldung:**  
    *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
    *Zeilennummer: 1, Spaltennummer: 2, Fehler Token:;. Zeile: ' c1; [] = > Issue(claim=c1);'.*  
    *Analysefehler: "POLICY0030: Syntaxfehler, unerwartete '; erwartet einen der folgenden: ':'.'*  
  
2.  Beispiel:  
  
    ```  
    c1:[]=>Issue(claim=c2);  
    ```  
  
    In diesem Beispiel ist das ID-Tag in der ausstellungsanweisung Kopie nicht definiert.   
    **Fehlermeldung**:   
    *POLICY0011: Keine Bedingung in der Anspruchsregel entsprechen dem Kennzeichen Bedingung in der CopyIssuanceStatement: 'c2'.*  
  
3.  Beispiel:  
  
    ```  
    c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
    ```  
  
    "Bool" ist nicht mit einem Terminalserver in der Sprache, und es ist keinem gültigen ValueType. Gültige Terminals sind in der folgenden Fehlermeldung aufgeführt.   
    **Fehlermeldung:**  
    *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
    Zeilennummer: 1, Spaltennummer: 39, Fehler Token: "Bool". Zeile: ' c1: [Typ == "X1," Wert "1" Valuetype == "Bool" ==] = > Issue(claim=c1);'.   
    *Analysefehler: "POLICY0030: Syntaxfehler, unerwartete 'STRING', erwartet einen der folgenden: 'INT64_TYPE' 'UINT64_TYPE' 'STRING_TYPE' 'BOOLEAN_TYPE'"BEZEICHNER"*  
  
4.  Beispiel:  
  
    ```  
    c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
    ```  
  
    Die Zahl **1** in diesem Beispiel ist kein gültiges Token in der Sprache, und diese Verwendung ist in einer Bedingung nicht zulässig. Er muss in doppelten Anführungszeichen, es stellen Sie eine Zeichenfolge eingeschlossen werden.   
    **Fehlermeldung:**  
    *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
    *Zeilennummer: 1, Spaltennummer: 23, Fehler Token: 1. Zeile: ' c1: [Typ == "X1," Wert == 1 "," Valuetype == "Bool"] = > Issue(claim=c1);'. * *-Analysefehler: "POLICY0029: Unerwarteter Eingaben.*  
  
5.  Beispiel:  
  
    ```  
    c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
         Issue(type = c1.type, value="0", valuetype == "boolean");  
    ```  
  
    In diesem Beispiel wird ein doppelter Gleichheitszeichen (==) anstelle von ein Gleichheitszeichen (=) verwendet.   
    **Fehlermeldung:**  
    *POLICY0002: Richtliniendaten konnte nicht analysiert werden.*  
    *Zeilennummer: 1, Spaltennummer: 91, Fehler Token: ==. Zeile: ' c1: [Typ == "X1," Wert "1", ==*  
    *ValueType "Boolean" ==] = > Problem (type=c1.type, Wert = "0" Valuetype "Boolean" ==);'.*  
    *Analysefehler: "POLICY0030: Syntaxfehler, unerwartete"==", eines der folgenden erwartet: '='*  
  
6.  Beispiel:  
  
    ```  
    c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
          Issue(type=c1.type, value=c1.value, valuetype = "string");  
    ```  
  
    In diesem Beispiel ist die Syntax und Semantik richtig. Allerdings mithilfe von "Boolean" ein Zeichenfolgenwert, Verwechslungen gebunden ist, und sollte vermieden werden. Wie bereits erwähnt, Sprache Terminals verwenden, wie Ansprüche Werte möglichst vermieden werden sollten.  
  
## <a name="BKMK_LT"></a>Sprache terminals  
Die folgende Tabelle enthält den vollständigen Satz von Terminaldienste-Zeichenfolgen und das zugehörige Language-Anschlüsse, die in der Ansprüche Transformation Regeln Sprache verwendet werden. Diese Definitionen verwenden Groß-und Kleinschreibung UTF-16-Zeichenfolgen.  
  
|Zeichenfolge|Terminaldienste|  
|----------|------------|  
|"=>"|IMPLIZIEREN|  
|";"|DURCH SEMIKOLONS|  
|":"|DOPPELPUNKT|  
|","|DURCH TRENNZEICHEN|  
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
|"&&"|UND|  
|"Issue"|PROBLEM|  
|"Geben Sie"|TYP|  
|"Value"|WERT|  
|"Valuetype"|WERTTYP|  
|"Forderung"|ANSPRUCHS|  
|"[_A-Za-z][_A-Za-z0-9]*"|BEZEICHNER|  
|"\\"[^\\"\n]*\\""|ZEICHENFOLGE|  
|"uint64"|UINT64_TYPE|  
|"int64"|INT64_TYPE|  
|"String"|STRING_TYPE|  
|"boolean"|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>Die syntax  
Die folgenden Ansprüche Transformation Regeln Sprache wird in Form von ABNF angegeben. Diese Definition verwendet die Anschlüsse, die in der obigen Tabelle zusätzlich zu der hier festgelegten ABNF-Produktionen angegeben werden. Die Regeln müssen in UTF-16-codiert sein, und das Vergleichen von Zeichenfolgen als Groß-/Kleinschreibung behandelt werden müssen.  
  
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
  


