---
ms.assetid: 65e474b5-3076-4ba3-809d-a09160f7c2bd
title: Rolle von Anspruchsregeln
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 410e9ce5fbde7d84cbb4efbbde3515d0af537180
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937887"
---
# <a name="the-role-of-claim-rules"></a>Rolle von Anspruchsregeln
Die Gesamtfunktion der Verbunddienst in Active Directory-Verbunddienste (AD FS) \( AD FS \) besteht darin, ein Token auszugeben, das einen Satz von Ansprüchen enthält. Die Entscheidung bezüglich der Ansprüche, die AD FS akzeptiert und dann Probleme behandelt, unterliegt den Anspruchs Regeln.

## <a name="what-are-claim-rules"></a>Was sind Anspruchsregeln?
Eine Anspruchs Regel stellt eine Instanz der Geschäftslogik dar, die einen oder mehrere eingehende Ansprüche annimmt, Bedingungen auf Sie anwendet, \( Wenn x und y ist, \) und einen oder mehrere ausgehende Ansprüche basierend auf den Bedingungs Parametern erzeugt. Weitere Informationen zu eingehenden und ausgehenden Ansprüchen finden Sie [unter die Rolle von Ansprüchen](The-Role-of-Claims.md).

Anspruchsregeln werden verwendet, um Geschäftslogik zu implementieren, die den Anspruchsverlauf in der Anspruchspipeline steuert. Obwohl es sich bei der Anspruchs Pipeline um ein eher logisches Konzept des End- \- to- \- End-Prozesses für den Fluss von Ansprüchen handelt, sind Anspruchs Regeln ein tatsächliches administratives Element, mit dem Sie den Anspruchs Verlauf durch den Anspruchs Ausstellungs Prozess anpassen können.

Weitere Informationen zur Anspruchs Pipeline finden Sie [unter The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).

Anspruchsregeln bieten folgende Vorteile:

-   Stellen Sie einen Mechanismus bereit, mit dem Administratoren Lauf \- Zeit Geschäftslogik auf vertrauende Ansprüche von Anspruchs Anbietern anwenden können.

-   Bereitstellen eines Mechanismus, mit dem Administratoren definieren können, welche Ansprüche für vertrauende Seiten ausgegeben werden

-   Bereitstellen von umfassenden und detaillierten Anspruchs \- basierten Autorisierungs Funktionen für Administratoren, die den Zugriff für bestimmte Benutzer zulassen oder verweigern möchten

### <a name="how-claim-rules-are-processed"></a>Verarbeiten von Anspruchsregeln
Anspruchsregeln werden mithilfe der *Anspruchs-Engine* über die Anspruchspipline verarbeitet. Die Anspruchs-Engine ist eine logische Komponente des Verbunddiensts, die den Satz der von einem Benutzer gesendeten eingehenden Ansprüche untersucht und anschließend in Abhängigkeit von der Logik in jeder Regel einen Ausgabeanspruchssatz erzeugt.

Die Anspruchs Regel-Engine und der Satz von Anspruchs Regeln, die einer bestimmten Verbund Vertrauensstellung zugeordnet sind, bestimmen zusammen, ob eingehende Ansprüche unverändert übergeben werden sollen, gefiltert nach den Kriterien einer bestimmten Bedingung oder werden in einen völlig neuen Satz von Ansprüchen transformiert, bevor Sie von ihrer Verbunddienst als ausgehende Ansprüche ausgegeben werden.

Weitere Informationen zu diesem Prozess finden Sie [unter The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).

## <a name="what-are-claim-rule-templates"></a>Was sind Anspruchsregelvorlagen?
AD FS enthält einen vordefinierten Satz von Anspruchs Regel Vorlagen, die Ihnen helfen sollen, die am besten geeigneten Anspruchs Regeln für Ihre bestimmte geschäftliche Anforderungen auszuwählen und zu erstellen. Anspruchsregelvorlagen werden nur beim Erstellungsprozess für die Anspruchsregel verwendet.

Im Snap-in "AD FS-Verwaltung" \- können Regeln nur mithilfe von Anspruchs Regel Vorlagen erstellt werden. Nachdem Sie mit dem Snap- \- in eine Anspruchs Regel Vorlage ausgewählt haben, geben Sie die erforderlichen Daten für die Regellogik ein, und speichern Sie Sie in der Konfigurations Datenbank. Sie wird \( ab diesem Punkt \) in der Benutzeroberfläche als Anspruchs Regel bezeichnet.

### <a name="how-claim-rule-templates-work"></a>Funktionsweise von Anspruchsregelvorlagen
Auf den ersten Blick erscheinen Anspruchs Regel Vorlagen nur als Eingabeformulare, die vom Snap-in bereitgestellt werden, \- um Daten zu sammeln und bestimmte Logik für eingehende Ansprüche zu verarbeiten. Bei genauerer Betrachtung speichern Anspruchsregelvorlagen jedoch das erforderliche Framework für die Anspruchsregelsprache, das die Basislogik bereitstellt, die Ihnen das schnelle Erstellen einer Regel ohne tiefgehende Kenntnis der Sprache ermöglicht.

Jede Vorlage, die in der Benutzeroberfläche der Benutzeroberfläche bereitgestellt wird \( \) , stellt eine vorab aufgefüllte Syntax der Anspruchs Regel Sprache dar, die auf den am häufigsten erforderlichen administrativen Aufgaben basiert. Es gibt jedoch eine Vorlage, die eine Ausnahme bildet. Diese Vorlage wird als benutzerdefinierte Regelvorlage bezeichnet. Sie enthält keine vordefinierte Syntax. Stattdessen müssen Sie die Syntax für die Anspruchsregel mithilfe der Anspruchsregelsprache direkt im Textkörper des Anspruchsregel-Vorlagenformulars erstellen.

Weitere Informationen zur Verwendung der Syntax der Anspruchs Regel Sprache finden Sie in der [Rolle der Anspruchs Regel Sprache](The-Role-of-the-Claim-Rule-Language.md) im AD FS Bereitstellungs Handbuch.

> [!TIP]
> Sie können die einer Regel zugeordnete Anspruchsregelsprache jederzeit anzeigen, indem Sie in den Eigenschaften einer Anspruchsregel auf die Schaltfläche **Regelsprache anzeigen** klicken.

### <a name="how-to-create-a-claim-rule"></a>Erstellen einer Anspruchsregel
Anspruchsregeln werden separat für jede Verbund-Vertrauensstellungsbeziehung innerhalb des Verbunddiensts erstellt und werden nicht von mehreren Vertrauensstellungen gemeinsam verwendet. Sie können entweder eine Regel auf Basis einer Anspruchsregelvorlage erstellen, eine Regel mithilfe der Anspruchsregelsprache von Grund auf neu erstellen oder eine Regel mithilfe von Windows PowerShell anpassen.

Diese unterschiedlichen Optionen bieten Ihnen die Flexibilität, die geeignete Methode für ein bestimmtes Szenario auszuwählen. Weitere Informationen zum Erstellen einer Anspruchs Regel finden Sie unter Konfigurieren von [Anspruchs Regeln](../deployment/configuring-claim-rules.md) im AD fsdeployment Guide.

#### <a name="using-claim-rule-templates"></a>Verwenden von Anspruchsregelvorlagen
Anspruchsregelvorlagen werden nur beim Erstellungsprozess für die Anspruchsregel verwendet. Mit den folgenden Vorlagen können Sie eine Anspruchsregel erstellen:

-   Eingehenden Anspruch weiterleiten oder filtern

-   Transformieren eines eingehenden Anspruchs

-   LDAP-Attribute als Ansprüche senden

-   Gruppenmitgliedschaft als Anspruch senden

-   Senden von Ansprüchen mit benutzerdefinierter Regel

-   Benutzer auf der Grundlage eines eingehenden Anspruchs zulassen oder verweigern

-   Alle Benutzer zulassen

Weitere Informationen zu den einzelnen Anspruchs Regel Vorlagen finden [Sie unter Bestimmen der zu verwendenden Anspruchs Regel Vorlage](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).

#### <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache
Für Geschäftsregeln, die über den Rahmen einer Standard-Anspruchsregelvorlage hinausgehen, können Sie eine benutzerdefinierte Regelvorlage verwenden, um mithilfe der Anspruchsregelsprache eine Reihe komplexer Logikbedingungen auszudrücken. Weitere Informationen zum Verwenden einer benutzerdefinierten Regel finden Sie unter [Verwenden einer benutzerdefinierten Anspruchs Regel](When-to-Use-a-Custom-Claim-Rule.md).

#### <a name="using-windowspowershell"></a>Verwenden von Windows PowerShell
Sie können auch das Cmdlet-Objekt adfsclaimruleset mit Windows PowerShell verwenden, um Regeln in AD FS zu erstellen oder zu verwalten. Weitere Informationen zur Verwendung von Windows PowerShell mit diesem Cmdlet finden Sie unter [AD FS Administration with Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).

## <a name="what-is-a-claim-rule-set"></a>Was ist ein Anspruchsregelsatz?
Wie in der folgenden Abbildung dargestellt, ist ein Anspruchsregelsatz eine Gruppierung von einer oder mehreren Regeln für eine angegebene Verbundvertrauensstellung, die definiert, wie Ansprüche durch die Anspruchsregel-Engine verarbeitet werden. Bei Empfang eines eingehenden Anspruchs durch den Verbunddienst wendet die Anspruchsregel-Engine die Logik an, die durch den entsprechenden Anspruchsregelsatz angegeben wird. Das Endergebnis der Logik aller Regeln im Satz bestimmt, wie die Ansprüche für eine bestimmte Vertrauensstellung in ihrer Gesamtheit ausgegeben werden.

![Rollen AD FS](media/adfs2_claimruleset.gif)

Anspruchsregeln werden von der Anspruchs-Engine innerhalb eines bestimmten Regelsatzes chronologisch verarbeitet. Diese Reihenfolge ist wichtig, da die Ausgabe einer Regel als Eingabe für die nächste Regel im Satz verwendet werden kann.

## <a name="what-are-claim-rule-set-types"></a>Was sind Anspruchsregelsatz-Typen?
Ein Anspruchsregelsatz-Typ ist ein logisches Segment einer Verbundvertrauensstellung, die kategorisch angibt, ob der der Vertrauensstellung zugeordnete Anspruchsregelsatz für die Ausstellung, Autorisierung oder Akzeptanz von Ansprüchen verwendet wird. Jeder Verbundvertrauensstellung können in Abhängigkeit vom Typ der verwendeten Vertrauensstellung ein oder mehrere Anspruchsregelsatz-Typen zugeordnet werden.

Die folgende Tabelle beschreibt die verschiedenen Anspruchsregelsatz-Typen und erläutert deren Beziehung zu entweder einer Anspruchsanbieter-Vertrauensstellung oder einer Vertrauensstellung der vertrauenden Seite.

|Anspruchsregelsatz-Typ|BESCHREIBUNG|Verwendung|
|-----------------------|---------------|-----------|
|Akzeptanztransformations-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine bestimmte Anspruchsanbieter-Vertrauensstellung verwenden, um die eingehenden Ansprüche, die von der Organisation des Anspruchsanbieters akzeptiert werden, sowie die ausgehenden Ansprüche anzugeben, die an die Vertrauensstellung der vertrauenden Seite gesendet werden.<p>Die eingehenden Ansprüche, die als Quelle für diesen Regelsatz verwendet werden, sind die Ansprüche, die von dem in der Anspruchsanbieterorganisation angegebenen Ausstellungstransformations-Regelsatz ausgegeben werden.<p>Standardmäßig enthält der Vertrauensstellungsknoten des Anspruchsanbieters eine Anspruchsanbieter-Vertrauensstellung mit dem Namen **Active Directory**, die verwendet wird, um den Quellattributspeicher für den Akzeptanztransformations-Regelsatz darzustellen. Mit diesem Vertrauensstellungsobjekt wird die Verbindung von Ihrem Verbunddienst zu einer Active Directory-Datenbank in Ihrem Netzwerk dargestellt. Diese Standardvertrauensstellung verarbeitet Ansprüche für Benutzer, die von Active Directory authentifiziert wurden, und kann nicht gelöscht werden.|Anspruchsanbieter-Vertrauensstellungen|
|Ausstellungstransformations-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Ansprüche anzugeben, die für die vertrauende Seite ausgegeben werden.<p>Die eingehenden Ansprüche, die als Quelle für diesen Regelsatz verwendet werden, sind zunächst die Ansprüche, die von den Ausstellungstransformationsregeln ausgegeben werden.|Vertrauensstellungen der vertrauenden Seite|
|Ausstellungsautorisierungs-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Benutzer anzugeben, die zum Empfang eines Tokens für die vertrauende Seite berechtigt sind.<p>Diese Regeln bestimmen, ob ein Benutzer Ansprüche für eine vertrauende Seite empfangen und damit auf die vertrauende Seite zugreifen kann.<p>Wenn Sie keine Ausstellungsautorisierungsregel angeben, wird der Zugriff allen Benutzern standardmäßig verweigert.|Vertrauensstellungen der vertrauenden Seite|
|Delegationsautorisierungs-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Benutzer anzugeben, die als Stellvertreter für andere Benutzer der vertrauenden Seite agieren dürfen.<p>Diese Regeln bestimmen, ob die anfordernde Person zur Annahme der Identität eines Benutzers berechtigt ist, wobei die anfordernde Person im an die vertrauende Seite gesendeten Token trotzdem identifiziert wird.<p>Wenn Sie keine Autorisierungs Autorisierungs Regel angeben, können Benutzer standardmäßig nicht als Delegaten fungieren.|Vertrauensstellungen der vertrauenden Seite|
|Autorisierungsregelsatz für den Identitätswechsel|Ein Anspruchsregelsatz, den Sie mit Windows PowerShell konfigurieren, um zu bestimmen, ob ein Benutzer vollständig die Identität eines anderen Benutzers der vertrauenden Seite annehmen kann.<p>Diese Regeln bestimmen, ob die anfordernde Person zur Annahme der Identität eines Benutzers berechtigt ist, ohne dass die anfordernde Person im an die vertrauende Seite gesendeten Token identifiziert wird.<p>Die Annahme der Identität eines anderen Benutzers in dieser Weise ist eine sehr leistungsstarke Funktion, da die vertrauende Seite nicht weiß, dass ein anderer die Identität des Benutzers angenommen hat.|Vertrauensstellung der vertrauenden Seite|

Weitere Informationen zum Auswählen der geeigneten Anspruchs Regeln für Ihre Organisation finden Sie unter [bestimmen der zu verwendenden Anspruchs Regel Vorlage](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).
