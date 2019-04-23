---
ms.assetid: 65e474b5-3076-4ba3-809d-a09160f7c2bd
title: Rolle von Anspruchsregeln
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e47dbecdeee620d3a237ad8d8c41a550d3ef069c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860781"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-claim-rules"></a>Rolle von Anspruchsregeln
Die allgemeine Funktion des Verbunddiensts in Active Directory-Verbunddienste \(AD FS\) besteht darin, ein Token ausstellen, die einen Satz von Ansprüchen enthält. Die Entscheidung, welche Ansprüche, die AD FS akzeptiert und gibt dann unterliegt Anspruchsregeln.  
  
## <a name="what-are-claim-rules"></a>Was sind Anspruchsregeln?  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die nehmen eine oder mehrere eingehende Ansprüche Bedingungen anwendet \(If x, dann y\) und erzeugen Sie eine oder mehrere ausgehende Ansprüche, die Grundlage der Bedingungsparameter. Weitere Informationen zu ein- und ausgehende Ansprüche, finden Sie unter [The Role of Claims](The-Role-of-Claims.md).  
  
Anspruchsregeln werden verwendet, um Geschäftslogik zu implementieren, die den Anspruchsverlauf in der Anspruchspipeline steuert. Während der anspruchspipeline mehr ein logisches Konzept des Endes\-zu\-Ende des Prozesses für anspruchsverlaufs, beanspruchen Sie die Regeln sind ein tatsächliches administratives Element, mit denen Sie den anspruchsverlauf im anspruchsausstellungsprozess anpassen können.  
  
Weitere Informationen zur anspruchspipeline finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md).  
  
Anspruchsregeln bieten folgende Vorteile:  
  
-   Bieten einen Mechanismus für Administratoren ausführen anwenden\-Zeit Geschäftslogik für vertrauende Ansprüche von Anspruchsanbietern  
  
-   Bereitstellen eines Mechanismus, mit dem Administratoren definieren können, welche Ansprüche für vertrauende Seiten ausgegeben werden  
  
-   Bereitstellen von aussagekräftigen und detaillierten Ansprüche\-Autorisierungsfunktionen für Administratoren, die Zugriff zulassen oder Verweigern des Zugriffs auf bestimmte Benutzer möchten basierend  
  
### <a name="how-claim-rules-are-processed"></a>Verarbeiten von Anspruchsregeln  
Anspruchsregeln werden mithilfe des *Anspruchsmoduls* über die Anspruchspipline verarbeitet. Das Anspruchsmodul ist eine logische Komponente des Verbunddiensts, die den Satz der von einem Benutzer gesendeten eingehenden Ansprüche untersucht und anschließend in Abhängigkeit von der Logik in jeder Regel einen Ausgabeanspruchssatz erzeugt.  
  
Das Anspruchsregelmodul und der Anspruchsregelsatz bestimmen in Verbindung mit einer angegebenen Verbundvertrauensstellung, ob eingehende Ansprüche unverändert weitergereicht, anhand der Kriterien einer bestimmten Bedingung gefiltert oder in einen vollständig neuen Satz von Ansprüchen transformiert werden, bevor sie durch den Verbunddienst als ausgehende Ansprüche ausgegeben werden.  
  
Weitere Informationen zu diesem Prozess finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md).  
  
## <a name="what-are-claim-rule-templates"></a>Was sind Anspruchsregelvorlagen?  
Einen vordefinierten Satz von anspruchsregelvorlagen, mit denen Sie auf einfache Weise auswählen, und erstellen die am besten geeigneten Anspruchsregeln für Ihre spezifischen Anforderungen Ihres Unternehmens, umfasst AD FS. Anspruchsregelvorlagen werden nur beim Erstellungsprozess für die Anspruchsregel verwendet.  
  
Im AD FS-Verwaltungs-Snap-\-in Regeln können nur erstellt werden mit anspruchsregelvorlagen. Nachdem Sie mithilfe der angedockten\-in einer anspruchsregelvorlage auswählen, geben Sie die erforderlichen Daten für die Regellogik, und speichern Sie sie mit der Konfigurationsdatenbank, sie werden \(ab diesem Punkt\) in der Benutzeroberfläche als Anspruchsregel bezeichnet.  
  
### <a name="how-claim-rule-templates-work"></a>Funktionsweise von Anspruchsregelvorlagen  
Auf den ersten Blick Anspruch Regelvorlagen erscheinen nur durch das Snap-in bereitgestellte Eingabeformulare\-in zum Sammeln von Daten und prozessspezifischer Logik für eingehende Ansprüche. Bei genauerer Betrachtung speichern Anspruchsregelvorlagen jedoch das erforderliche Framework für die Anspruchsregelsprache, das die Basislogik bereitstellt, die Ihnen das schnelle Erstellen einer Regel ohne tiefgehende Kenntnis der Sprache ermöglicht.  
  
Jede Vorlage, die in der Benutzeroberfläche bereitgestellt wird \(UI\) eine vorab aufgefüllte Anspruchsregel-Sprachsyntax, basierend auf den am häufigsten erforderlichen administrativen Aufgaben darstellt. Es gibt jedoch eine Vorlage, die eine Ausnahme bildet. Diese Vorlage wird als benutzerdefinierte Regelvorlage bezeichnet. Sie enthält keine vordefinierte Syntax. Stattdessen müssen Sie die Syntax für die Anspruchsregel mithilfe der Anspruchsregelsprache direkt im Textkörper des Anspruchsregel-Vorlagenformulars erstellen.  
  
Weitere Informationen zur Verwendung der Syntax der anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md) in AD FS-Bereitstellungshandbuch.  
  
> [!TIP]  
> Sie können die einer Regel zugeordnete Anspruchsregelsprache jederzeit anzeigen, indem Sie in den Eigenschaften einer Anspruchsregel auf die Schaltfläche **Regelsprache anzeigen** klicken.  
  
### <a name="how-to-create-a-claim-rule"></a>Erstellen einer Anspruchsregel  
Anspruchsregeln werden separat für jede Verbund-Vertrauensstellungsbeziehung innerhalb des Verbunddiensts erstellt und werden nicht von mehreren Vertrauensstellungen gemeinsam verwendet. Sie können entweder eine Regel auf Basis einer Anspruchsregelvorlage erstellen, eine Regel mithilfe der Anspruchsregelsprache von Grund auf neu erstellen oder eine Regel mithilfe von Windows PowerShell anpassen.  
  
Diese unterschiedlichen Optionen bieten Ihnen die Flexibilität, die geeignete Methode für ein bestimmtes Szenario auszuwählen. Weitere Informationen über das Erstellen einer Anspruchsregel finden Sie unter [Konfigurieren von Anspruchsregeln](https://technet.microsoft.com/library/ee913571.aspx) im AD FSDeployment Guide.  
  
#### <a name="using-claim-rule-templates"></a>Verwenden von Anspruchsregelvorlagen  
Anspruchsregelvorlagen werden nur beim Erstellungsprozess für die Anspruchsregel verwendet. Mit den folgenden Vorlagen können Sie eine Anspruchsregel erstellen:  
  
-   Durchlauf oder Filtern eines eingehenden Anspruchs  
  
-   Eingehenden Anspruch transformieren  
  
-   LDAP-Attribute als Ansprüche senden  
  
-   Gruppenmitgliedschaft als Anspruch senden  
  
-   Senden von Ansprüchen mit benutzerdefinierter Regel  
  
-   Benutzer auf der Grundlage eines eingehenden Anspruchs zulassen oder verweigern  
  
-   Alle Benutzer zulassen  
  
Weitere Informationen, die einzelnen anspruchsregelvorlagen, finden Sie unter [bestimmt der Typ des Anspruchs Regelvorlage verwenden](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).  
  
#### <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Für Geschäftsregeln, die über den Rahmen einer Standard-Anspruchsregelvorlage hinausgehen, können Sie eine benutzerdefinierte Regelvorlage verwenden, um mithilfe der Anspruchsregelsprache eine Reihe komplexer Logikbedingungen auszudrücken. Weitere Informationen zur Verwendung einer benutzerdefinierten Regelsatzes finden Sie unter [verwenden Sie eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
#### <a name="using-windowspowershell"></a>Verwenden von Windows PowerShell  
Sie können auch die Cmdlet-Objekt ADFSClaimRuleSet mit Windows PowerShell zum Erstellen oder Verwalten von Regeln in AD FS. Weitere Informationen darüber, wie Sie Windows PowerShell mit diesem Cmdlet verwenden können, finden Sie unter [AD FS-Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
## <a name="what-is-a-claim-rule-set"></a>Was ist ein Anspruchsregelsatz?  
Wie in der folgenden Abbildung dargestellt, ist ein Anspruchsregelsatz eine Gruppierung von einer oder mehreren Regeln für eine angegebene Verbundvertrauensstellung, die definiert, wie Ansprüche durch das Anspruchsregelmodul verarbeitet werden. Bei Empfang eines eingehenden Anspruchs durch den Verbunddienst wendet das Anspruchsregelmodul die Logik an, die durch den entsprechenden Anspruchsregelsatz angegeben wird. Das Endergebnis der Logik aller Regeln im Satz bestimmt, wie die Ansprüche für eine bestimmte Vertrauensstellung in ihrer Gesamtheit ausgegeben werden.  
  
![AD FS-Rollen](media/adfs2_claimruleset.gif)  
  
Anspruchsregeln werden vom Anspruchsmodul innerhalb eines bestimmten Regelsatzes chronologisch verarbeitet. Diese Reihenfolge ist wichtig, da die Ausgabe einer Regel als Eingabe für die nächste Regel im Satz verwendet werden kann.  
  
## <a name="what-are-claim-rule-set-types"></a>Was sind Anspruchsregelsatz-Typen?  
Ein Anspruchsregelsatz-Typ ist ein logisches Segment einer Verbundvertrauensstellung, die kategorisch angibt, ob der der Vertrauensstellung zugeordnete Anspruchsregelsatz für die Ausstellung, Autorisierung oder Akzeptanz von Ansprüchen verwendet wird. Jeder Verbundvertrauensstellung können in Abhängigkeit vom Typ der verwendeten Vertrauensstellung ein oder mehrere Anspruchsregelsatz-Typen zugeordnet werden.  
  
Die folgende Tabelle beschreibt die verschiedenen Anspruchsregelsatz-Typen und erläutert deren Beziehung zu entweder einer Anspruchsanbieter-Vertrauensstellung oder einer Vertrauensstellung der vertrauenden Seite.  
  
|Anspruchsregelsatz-Typ|Beschreibung|Verwendung|  
|-----------------------|---------------|-----------|  
|Akzeptanztransformations-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine bestimmte Anspruchsanbieter-Vertrauensstellung verwenden, um die eingehenden Ansprüche, die von der Organisation des Anspruchsanbieters akzeptiert werden, sowie die ausgehenden Ansprüche anzugeben, die an die Vertrauensstellung der vertrauenden Seite gesendet werden.<br /><br />Die eingehenden Ansprüche, die als Quelle für diesen Regelsatz verwendet werden, sind die Ansprüche, die von dem in der Anspruchsanbieterorganisation angegebenen Ausstellungstransformations-Regelsatz ausgegeben werden.<br /><br />Standardmäßig enthält der Vertrauensstellungsknoten des Anspruchsanbieters eine Anspruchsanbieter-Vertrauensstellung mit dem Namen **Active Directory**, die verwendet wird, um den Quellattributspeicher für den Akzeptanztransformations-Regelsatz darzustellen. Mit diesem Vertrauensstellungsobjekt wird die Verbindung von Ihrem Verbunddienst zu einer Active Directory-Datenbank in Ihrem Netzwerk dargestellt. Diese Standardvertrauensstellung verarbeitet Ansprüche für Benutzer, die von Active Directory authentifiziert wurden, und kann nicht gelöscht werden.|Anspruchsanbieter-Vertrauensstellungen|  
|Ausstellungstransformations-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Ansprüche anzugeben, die für die vertrauende Seite ausgegeben werden.<br /><br />Die eingehenden Ansprüche, die als Quelle für diesen Regelsatz verwendet werden, sind zunächst die Ansprüche, die von den Ausstellungstransformationsregeln ausgegeben werden.|Vertrauensstellungen der vertrauenden Seite|  
|Ausstellungsautorisierungs-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Benutzer anzugeben, die zum Empfang eines Tokens für die vertrauende Seite berechtigt sind.<br /><br />Diese Regeln bestimmen, ob ein Benutzer Ansprüche für eine vertrauende Seite empfangen und damit auf die vertrauende Seite zugreifen kann.<br /><br />Wenn Sie keine Ausstellungsautorisierungsregel angeben, wird der Zugriff allen Benutzern standardmäßig verweigert.|Vertrauensstellungen der vertrauenden Seite|  
|Delegationsautorisierungs-Regelsatz|Ein Anspruchsregelsatz, den Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Benutzer anzugeben, die als Stellvertreter für andere Benutzer der vertrauenden Seite agieren dürfen.<br /><br />Diese Regeln bestimmen, ob die anfordernde Person zur Annahme der Identität eines Benutzers berechtigt ist, wobei die anfordernde Person im an die vertrauende Seite gesendeten Token trotzdem identifiziert wird.<br /><br />Wenn Sie keine Ausstellungsautorisierungsregel angeben, können Benutzer standardmäßig nicht als Stellvertreter agieren.|Vertrauensstellungen der vertrauenden Seite|  
|Autorisierungsregelsatz für den Identitätswechsel|Ein Anspruchsregelsatz, den Sie mit Windows PowerShell konfigurieren, um zu bestimmen, ob ein Benutzer vollständig die Identität eines anderen Benutzers der vertrauenden Seite annehmen kann.<br /><br />Diese Regeln bestimmen, ob die anfordernde Person zur Annahme der Identität eines Benutzers berechtigt ist, ohne dass die anfordernde Person im an die vertrauende Seite gesendeten Token identifiziert wird.<br /><br />Die Annahme der Identität eines anderen Benutzers in dieser Weise ist eine sehr leistungsstarke Funktion, da die vertrauende Seite nicht weiß, dass ein anderer die Identität des Benutzers angenommen hat.|Vertrauensstellung der vertrauenden Seite|  
  
Weitere Informationen zum auswählen die geeigneten Anspruchsregeln für die Verwendung in Ihrer Organisation finden Sie unter [bestimmt der Typ des Anspruchs Regelvorlage verwenden](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).  
  

