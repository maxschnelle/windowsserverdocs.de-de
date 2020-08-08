---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: Ansprüche Transformation Regeln Sprache
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c4b35c738e275456929b7f90fec9be605876a4e6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952903"
---
# <a name="claims-transformation-rules-language"></a>Ansprüche Transformation Regeln Sprache

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Gesamtstruktur übergreifende Anspruchs Transformations Funktion ermöglicht es Ihnen, Ansprüche für dynamische Access Control über Gesamtstruktur Grenzen hinweg durch Festlegen von Anspruchs Transformations Richtlinien auf Gesamtstruktur übergreifende Vertrauens Stellungen zu überbrücken. Die primäre Komponente aller Richtlinien sind Regeln, die in der Sprache der Anspruchs Transformationsregeln geschrieben sind. Dieses Thema enthält ausführliche Informationen zu dieser Sprache und enthält Anleitungen zum Erstellen von Anspruchs Transformationsregeln.

Die Windows PowerShell-Cmdlets für Transformations Richtlinien für Gesamtstruktur übergreifende Vertrauens Stellungen haben Optionen zum Festlegen einfacher Richtlinien, die in gängigen Szenarien erforderlich sind. Diese Cmdlets übersetzen die Benutzereingaben in Richtlinien und Regeln in der Sprache der Anspruchs Transformationsregeln und speichern Sie dann im vorgeschriebenen Format in Active Directory. Weitere Informationen zu Cmdlets für die Transformation von Ansprüchen finden Sie in den [AD DS Cmdlets für dynamisches Access Control](https://go.microsoft.com/fwlink/?LinkId=243150).

Abhängig von der Anspruchs Konfiguration und den Anforderungen, die für die Gesamtstruktur übergreifende Vertrauensstellung in Ihren Active Directory Gesamtstrukturen gelten, müssen ihre Anspruchs Transformations Richtlinien möglicherweise komplexer sein als die Richtlinien, die von den Windows PowerShell-Cmdlets für Active Directory unterstützt werden. Um solche Richtlinien effektiv zu verfassen, ist es von entscheidender Bedeutung, die Sprachsyntax und die Semantik der Anspruchs Transformationsregeln zu verstehen. Diese Anspruchs Transformations Regel-Sprache ("die Sprache") in Active Directory ist eine Teilmenge der Sprache, die von [Active Directory-Verbunddienste (AD FS)](https://go.microsoft.com/fwlink/?LinkId=243982) zu ähnlichen Zwecken verwendet wird, und Sie weist eine sehr ähnliche Syntax und Semantik auf. Es sind jedoch weniger Vorgänge zulässig, und zusätzliche Syntax Einschränkungen werden in der Active Directory Version der Sprache platziert.

In diesem Thema wird die Syntax und Semantik der Anspruchs Transformations Regel-Sprache in Active Directory erläutert, und es werden Überlegungen zum Erstellen von Richtlinien erläutert. Sie enthält mehrere Sätze von Beispiel Regeln, um Ihnen den Einstieg zu erleichtern, sowie Beispiele falscher Syntax und der von Ihnen generierten Meldungen, um beim Erstellen der Regeln Fehlermeldungen zu entschlüsseln.

## <a name="tools-for-authoring-claims-transformation-policies"></a>Tools zum Erstellen von Anspruchs Transformations Richtlinien
**Windows PowerShell-Cmdlets für Active Directory**: Dies ist die bevorzugte und empfohlene Methode zum Erstellen und Festlegen von Anspruchs Transformations Richtlinien. Diese Cmdlets bieten Schalter für einfache Richtlinien und überprüfen Regeln, die für komplexere Richtlinien festgelegt sind.

**LDAP**: Anspruchs Transformations Richtlinien können in Active Directory mithilfe von LDAP (Lightweight Directory Access Protocol) bearbeitet werden. Dies wird jedoch nicht empfohlen, da die Richtlinien mehrere komplexe Komponenten aufweisen und die von Ihnen verwendeten Tools die Richtlinie möglicherweise nicht validieren, bevor Sie Sie in Active Directory schreiben. Dies kann später eine beträchtliche Zeit für die Diagnose von Problemen erfordern.

## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory Anspruchs Transformationsregeln-Sprache

### <a name="syntax-overview"></a>Syntaxübersicht
Im folgenden finden Sie eine kurze Übersicht über die Syntax und die Semantik der Sprache:

-   Der Regelsatz der Anspruchs Transformation besteht aus null oder mehr Regeln. Jede Regel verfügt über zwei aktive Teile: **Wählen Sie Bedingungs Liste** und **Regel Aktion**aus. Wenn die **Liste Bedingung auswählen** als true ausgewertet wird, wird die entsprechende Regel Aktion ausgeführt.

-   Die **Auswahl Bedingungs Liste** enthält keine oder mehrere SELECT- **Bedingungen**. Alle SELECT- **Bedingungen** müssen als true ausgewertet werden, damit die **Liste Bedingung auswählen** als true ausgewertet wird.

-   Jede **Select-Bedingung** hat einen Satz von NULL oder mehr **übereinstimmenden Bedingungen**. Alle **übereinstimmenden Bedingungen** müssen als true ausgewertet werden, damit die Select-Bedingung als true ausgewertet wird. Alle diese Bedingungen werden anhand eines einzelnen Anspruchs ausgewertet. Ein Anspruch, der einer **Select-Bedingung** entspricht, kann durch einen **Bezeichner** gekennzeichnet werden und in der **Regel Aktion**darauf verwiesen werden.

-   Jede **übereinstimmende Bedingung** gibt die Bedingung an, mit der der **Typ** oder **Wert** oder **ValueType** eines Anspruchs mithilfe verschiedener Bedingungs **Operatoren** und **Zeichen folgen Literale**übereinstimmen.

    -   Wenn Sie eine abgleichsbedingung für **einen Wert**angeben, müssen Sie auch eine **entsprechende Bedingung** für einen bestimmten **Matching Condition** **ValueType** angeben und umgekehrt. Diese Bedingungen müssen in der-Syntax nebeneinander liegen.

    -   **ValueType** -Übereinstimmungs Bedingungen müssen nur bestimmte **ValueType** -Literale verwenden.

-   Eine **Regel Aktion** kann einen Anspruch kopieren, der mit einem **Bezeichner** gekennzeichnet ist, oder einen Anspruch auf der Grundlage eines Anspruchs, der mit einem Bezeichner und/oder angegebenen Zeichenfolgenliteralen gekennzeichnet ist, ausstellen.

**Beispiel Regel**

Dieses Beispiel zeigt eine Regel, die verwendet werden kann, um den Anspruchstyp zwischen zwei Gesamtstrukturen zu übersetzen, vorausgesetzt, Sie verwenden die gleichen Anspruchs ValueTypes und weisen die gleichen Interpretationen für Anspruchs Werte für diesen Typ auf. Die Regel verfügt über eine übereinstimmende Bedingung und eine Issue-Anweisung, die Zeichen folgen Literale und einen übereinstimmenden Anspruchs Verweis verwendet.

```
C1: [TYPE=="EmployeeType"]
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.

```

### <a name="runtime-operation"></a>Lauf Zeit Vorgang
Es ist wichtig, den Lauf Zeit Vorgang von Anspruchs Transformationen zu verstehen, um die Regeln effektiv zu verfassen. Der Lauf Zeit Vorgang verwendet drei Sätze von Ansprüchen:

1.  **Eingabe Anspruchssatz**: der Eingabe Satz der Ansprüche, die an den Anspruchs Transformations Vorgang übergeben werden.

2.  **Funktionierender Anspruchssatz**: zwischen Ansprüche, die während der Anspruchs Transformation gelesen und geschrieben werden.

3.  **Ausgabe Anspruchssatz**: Ausgabe des Anspruchs Transformations Vorgangs.

Im folgenden finden Sie eine kurze Übersicht über den Vorgang der Transformation für Lauf Zeit Ansprüche:

1.  Die Eingabe Ansprüche für die Transformation von Ansprüchen werden verwendet, um den Arbeits Anspruchssatz zu initialisieren.

    1.  Beim Verarbeiten jeder Regel wird der Arbeits Anspruchssatz für die Eingabe Ansprüche verwendet.

    2.  Die Auswahl Bedingungs Liste in einer Regel wird mit allen möglichen Sätzen von Ansprüchen aus dem Arbeits Anspruchssatz verglichen.

    3.  Jeder Satz übereinstimmender Ansprüche wird verwendet, um die Aktion in dieser Regel auszuführen.

    4.  Das Ausführen einer Regel Aktion führt zu einem Anspruch, der an den Ausgabe Anspruchssatz und den funktionierenden Anspruchssatz angefügt wird. Daher wird die Ausgabe einer Regel als Eingabe für nachfolgende Regeln im Regelsatz verwendet.

2.  Die Regeln im Regelsatz werden in sequenzieller Reihenfolge verarbeitet, beginnend mit der ersten Regel.

3.  Wenn der gesamte Regelsatz verarbeitet wird, wird der Ausgabe Anspruchssatz verarbeitet, um doppelte Ansprüche und andere Sicherheitsprobleme zu entfernen. Die resultierenden Ansprüche sind die Ausgabe des Anspruchs Transformationsprozesses.

Komplexe Anspruchs Transformationen können basierend auf dem vorherigen Laufzeitverhalten geschrieben werden.

**Beispiel: Lauf Zeit Vorgang**

Dieses Beispiel zeigt den Lauf Zeit Vorgang einer Anspruchs Transformation, die zwei Regeln verwendet.

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

### <a name="special-rules-semantics"></a>Semantik für spezielle Regeln
Im folgenden finden Sie eine spezielle Syntax für Regeln:

1.  Leerer Regelsatz = = keine Ausgabe Ansprüche

2.  Leere Auswahl Bedingungs Liste = = jeder Anspruch stimmt mit der Liste der SELECT-Bedingungen überein.

    **Beispiel: leere Auswahl Bedingungs Liste**

    Die folgende Regel gleicht jeden Anspruch im Workingset ab.

    ```
    => Issue (Type = "UserType", Value = "External", ValueType = "string")
    ```

3.  Leere SELECT Match List = = jeder Anspruch stimmt mit der Liste der ausgewählten Bedingungen überein

    **Beispiel: leere übereinstimmende Bedingungen**

    Die folgende Regel gleicht jeden Anspruch im Workingset ab. Dies ist die grundlegende "allow-all"-Regel, wenn Sie allein verwendet wird.

    ```
    C1:[] => Issule (claim = C1);
    ```

## <a name="security-considerations"></a>Sicherheitshinweise
**Ansprüche, die in eine Gesamtstruktur eintreten**

Die Ansprüche, die von Prinzipale vorgelegt werden, die in einer Gesamtstruktur eingehenden werden, müssen gründlich geprüft werden, um sicherzustellen, dass wir nur die richtigen Ansprüche zulassen oder ausstellen. Nicht ordnungsgemäße Ansprüche können die Gesamtstruktur Sicherheit beeinträchtigen, und dies sollte bei der Erstellung von Transformations Richtlinien für Ansprüche, die eine Gesamtstruktur eintreten, eine hohe Priorität haben.

Active Directory verfügt über die folgenden Funktionen, um eine Fehlkonfiguration von Ansprüchen zu verhindern, die in eine Gesamtstruktur eintreten:

-   Wenn für eine Gesamtstruktur-Vertrauensstellung für die Ansprüche, die in eine Gesamtstruktur eintreten, keine Anspruchs Transformations Richtlinie festgelegt ist, werden aus Sicherheits Active Directory Gründen alle Prinzipal Ansprüche gelöscht, die in die Gesamtstruktur eintreten.

-   Wenn die Ausführung des Regelsatzes für Ansprüche, die in eine Gesamtstruktur eintritt, zu Ansprüchen führt, die nicht in der Gesamtstruktur definiert sind, werden die nicht definierten Ansprüche aus den Ausgabe Ansprüchen gelöscht.

**Ansprüche, die eine Gesamtstruktur verlassen**

Ansprüche, die eine Gesamtstruktur verlassen, stellen für die Gesamtstruktur weniger Sicherheitsbedenken dar als die Ansprüche, die in die Gesamtstruktur eintreten. Ansprüche dürfen die Gesamtstruktur unverändert belassen, auch wenn keine entsprechende Anspruchs Transformations Richtlinie vorhanden ist. Es ist auch möglich, Ansprüche auszugeben, die nicht in der Gesamtstruktur als Teil der Transformation von Ansprüchen definiert sind, die die Gesamtstruktur verlassen. Dies dient zum einfachen Einrichten von Gesamtstruktur übergreifenden Vertrauens Stellungen mit Ansprüchen. Ein Administrator kann ermitteln, ob Ansprüche, die in die Gesamtstruktur eintreten, transformiert werden müssen, und die entsprechende Richtlinie einrichten. Beispielsweise könnte ein Administrator eine Richtlinie festlegen, wenn es erforderlich ist, einen Anspruch auszublenden, um die Offenlegung von Informationen zu verhindern.

**Syntax Fehler in Anspruchs Transformationsregeln**

Wenn für eine bestimmte Anspruchs Transformations Richtlinie ein Regelsatz vorliegt, der syntaktisch falsch ist, oder wenn andere Syntax-oder Speicherprobleme vorliegen, wird die Richtlinie als ungültig eingestuft. Dies wird anders behandelt als die zuvor erwähnten Standardbedingungen.

Active Directory kann die Absicht in diesem Fall nicht ermitteln und wechselt in einen ausfallsicheren Modus, in dem keine Ausgabe Ansprüche für diese Vertrauensstellung und Richtung des Durchlaufs generiert werden. Zum Beheben des Problems ist ein Administrator Eingriff erforderlich. Dies kann vorkommen, wenn LDAP zum Bearbeiten der Anspruchs Transformations Richtlinie verwendet wird. Windows PowerShell-Cmdlets für Active Directory Überprüfung durchgeführt werden, um das Schreiben einer Richtlinie mit Syntax Problemen zu verhindern.

## <a name="other-language-considerations"></a>Weitere Überlegungen zur Sprache

1.  Es gibt mehrere Schlüsselwörter oder Sonderzeichen, die in dieser Sprache spezifisch sind (als Terminals bezeichnet). Diese werden in der Tabelle " [sprach Terminals](Claims-Transformation-Rules-Language.md#BKMK_LT) " weiter unten in diesem Thema angezeigt. In den Fehlermeldungen werden die Tags für diese Terminals für die Mehrdeutigkeit verwendet.

2.  Terminals können mitunter als Zeichenfolgenliterale verwendet werden. Diese Verwendung kann jedoch mit der Sprachdefinition in Konflikt stehen oder unbeabsichtigte Folgen haben. Diese Art der Verwendung wird nicht empfohlen.

3.  Von der Regel Aktion können keine Typkonvertierungen für Anspruchs Werte ausgeführt werden, und ein Regelsatz, der eine solche Regel Aktion enthält, wird als ungültig angesehen. Dies führt zu einem Laufzeitfehler, und es werden keine Ausgabe Ansprüche erzeugt.

4.  Wenn eine Regel Aktion auf einen Bezeichner verweist, der nicht im Abschnitt Select Condition List der Regel verwendet wurde, handelt es sich um eine ungültige Verwendung. Dies würde einen Syntax Fehler verursachen.

    **Beispiel: falscher bezeichnerverweis** Die folgende Regel veranschaulicht einen falschen Bezeichner, der in der Regel Aktion verwendet wird.

    ```
    C1:[] => Issue (claim = C2);
    ```

## <a name="sample-transformation-rules"></a>Beispiele für Transformationsregeln

-   **Alle Ansprüche eines bestimmten Typs zulassen**

    Genauer Typ

    ```
    C1:[type=="XYZ"] => Issue (claim = C1);
    ```

    Verwenden von Regex

    ```
    C1: [type =~ "XYZ*"] => Issue (claim = C1);
    ```

-   **Einen bestimmten Anspruchstyp nicht zulassen** Genauer Typ

    ```
    C1:[type != "XYZ"] => Issue (claim=C1);
    ```

    Verwenden von Regex

    ```
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);
    ```

## <a name="examples-of-rules-parser-errors"></a>Beispiele für Regel Parser-Fehler
Anspruchs Transformationsregeln werden von einem benutzerdefinierten Parser analysiert, um auf Syntax Fehler zu überprüfen. Dieser Parser wird von zugehörigen Windows PowerShell-Cmdlets ausgeführt, bevor Regeln in Active Directory gespeichert werden. Alle Fehler beim Parsen der Regeln, einschließlich Syntax Fehlern, werden in der Konsole gedruckt. Domänen Controller führen auch den Parser aus, bevor Sie die Regeln zum Transformieren von Ansprüchen verwenden, und protokollieren Fehler im Ereignisprotokoll (Ereignisprotokoll Nummern hinzufügen).

In diesem Abschnitt werden einige Beispiele für Regeln veranschaulicht, die mit falscher Syntax geschrieben werden, sowie die entsprechenden Syntax Fehler, die vom Parser generiert werden.

1. Beispiel:

   ```
   c1;[]=>Issue(claim=c1);
   ```

   In diesem Beispiel ist ein Semikolon anstelle eines Doppelpunkts falsch verwendet.
   **Fehlermeldung:** 
    *POLICY0002: die Richtlinien Daten konnten nicht analysiert werden.* 
    *Zeilennummer: 1, Spaltennummer: 2, Fehler Token:;. Zeile: ' C1; [] =>Problem (Claim = C1); '.* 
    *Parserfehler: ' POLICY0030: Syntax Fehler, unerwartetes '; ', es wird eine der folgenden voraussichtlich erwartet: ': '. '*

2. Beispiel:

   ```
   c1:[]=>Issue(claim=c2);
   ```

   In diesem Beispiel ist das bezeichnertag in der Copy-Ausstellungs Anweisung nicht definiert.
   **Fehlermeldung**: *POLICY0011: keine Bedingungen in der Anspruchs Regel entsprechen dem Bedingungs Tag, das in der copyissuancestatement: ' C2 ' angegeben ist.*

3. Beispiel:

   ```
   c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)
   ```

   "bool" ist kein Terminal in der Sprache und kein gültiger ValueType. Gültige Terminals sind in der folgenden Fehlermeldung aufgeführt.
   **Fehlermeldung:** 
    *POLICY0002: die Richtlinien Daten konnten nicht analysiert werden.*
   Zeilennummer: 1, Spaltennummer: 39, Fehler Token: "bool". Zeile: ' C1: [Type = = "x1", Value = = "1", ValueType = = "bool"] =>Issue (Claim = C1); ".
   *Parserfehler: ' POLICY0030: Syntax Fehler, unerwartete ' Zeichenfolge ', erwartet wurde eine der folgenden Elemente: ' INT64_TYPE ' ' UINT64_TYPE ' ' STRING_TYPE ' ' BOOLEAN_TYPE ' ' Bezeichner '*

4. Beispiel:

   ```
   c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);
   ```

   Die Ziffer **1** in diesem Beispiel ist kein gültiges Token in der Sprache, und eine solche Verwendung ist in einer übereinstimmenden Bedingung nicht zulässig. Er muss in doppelte Anführungszeichen eingeschlossen werden, um ihn zu einer Zeichenfolge zu machen.
   **Fehlermeldung:** 
    *POLICY0002: die Richtlinien Daten konnten nicht analysiert werden.* 
    *Zeilennummer: 1, Spaltennummer: 23, Fehler Token: 1. Zeile: ' C1: [Type = = ' x1 ', Value = = 1, ValueType = = "bool"] =>Issue (Claim = C1); ".* <em>Parserfehler: ' POLICY0029: unerwartete Eingabe.</em>

5. Beispiel:

   ```
   c1:[type == "x1", value == "1", valuetype == "boolean"] =>

        Issue(type = c1.type, value="0", valuetype == "boolean");
   ```

   In diesem Beispiel wurde ein doppeltes Gleichheitszeichen (= =) anstelle eines einzelnen Gleichheitszeichens (=) verwendet.
   **Fehlermeldung:** 
    *POLICY0002: die Richtlinien Daten konnten nicht analysiert werden.* 
    *Zeilennummer: 1, Spaltennummer: 91, Fehler Token: = =. Zeile: ' C1: [Type = = ' x1 ', value = = ' 1 ',* 
    *ValueType = = ' Boolean '] =>Issue (Type = C1. Type, Value = "0", ValueType = = "Boolean"); ".* 
    *Parserfehler: ' POLICY0030: Syntax Fehler, unerwartetes ' = = ', erwartet wurde eines der folgenden Elemente: ' = '*

6. Beispiel:

   ```
   c1:[type=="x1", value=="boolean", valuetype=="string"] =>

         Issue(type=c1.type, value=c1.value, valuetype = "string");
   ```

   Dieses Beispiel ist syntaktisch und semantisch korrekt. Die Verwendung von "Boolean" als Zeichen folgen Wert ist jedoch an Verwirrung gebunden und sollte vermieden werden. Wie bereits erwähnt, sollten die Verwendung von sprach Terminals als Anspruchs Werte nach Möglichkeit vermieden werden.

## <a name="language-terminals"></a><a name="BKMK_LT"></a>Sprach Terminals
In der folgenden Tabelle sind die kompletten Terminal Zeichenfolgen und die zugehörigen sprach Terminals aufgelistet, die in der Anspruchs Transformations-Regel Sprache verwendet werden. In diesen Definitionen werden UTF-16-Zeichen folgen ohne Beachtung der Groß-und

|String|Terminal|
|----------|------------|
|"=>"|Bein|
|";"|Semikolon|
|":"|Doppelpunkt|
|","|Komma|
|"."|Gewinn|
|"["|O_SQ_BRACKET|
|"]"|C_SQ_BRACKET|
|"("|O_BRACKET|
|")"|C_BRACKET|
|"=="|EQ|
|"!="|NEQ|
|"=~"|REGEXP_MATCH|
|"!~"|REGEXP_NOT_MATCH|
|"="|Einräumen|
|"&&"|UND|
|betrifft|PROBLEM|
|Sorte|TYPE|
|Wert|VALUE|
|ValueType|VALUE_TYPE|
|erheben|Erheben|
|"[_A-za-z] [_a-zA-Z0-9] *"|IDENTIFIER|
|" \\ " [^ \\ "\n] * \\ " "|STRING|
|UInt64|UINT64_TYPE|
|Int64|INT64_TYPE|
|„String“|STRING_TYPE|
|booleschen|BOOLEAN_TYPE|

## <a name="language-syntax"></a>Sprachsyntax
Die folgende Sprache für Anspruchs Transformationsregeln wird in ABNF-Form angegeben. In dieser Definition werden die in der vorherigen Tabelle angegebenen Terminals zusätzlich zu den hier definierten ABNF-Produktionen verwendet. Die Regeln müssen in UTF-16 codiert werden, und die Zeichen folgen Vergleiche müssen bei der Groß-/Kleinschreibung nicht beachtet werden.

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



