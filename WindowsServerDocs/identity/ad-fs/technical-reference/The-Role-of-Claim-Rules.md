---
ms.assetid: 65e474b5-3076-4ba3-809d-a09160f7c2bd
title: Die Rolle von Anspruchsregeln
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e47dbecdeee620d3a237ad8d8c41a550d3ef069c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-claim-rules"></a>Die Rolle von Anspruchsregeln
Die allgemeine Funktion des Verbunddiensts in Active Directory Federation Services \(AD FS\) ist ein Token ausstellen, die eine Gruppe von Ansprüchen enthält. Die Entscheidung, welche Ansprüche AD FS akzeptiert und anschließend ausgegeben unterliegt Anspruchsregeln.  
  
## <a name="what-are-claim-rules"></a>Was sind Anspruchsregeln?  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die nehmen einen oder mehrere eingehende Ansprüche Bedingungen anwendet \ (wenn x dann Y\) und erstellen Sie einen oder mehrere ausgehende Ansprüche, die auf Grundlage der Bedingung-Parameter. Weitere Informationen zu eingehenden und ausgehenden Ansprüchen finden Sie unter [The Role of Claims ](The-Role-of-Claims.md).  
  
Anspruchsregeln werden verwendet, wenn Sie benötigen, um Geschäftslogik zu implementieren, die den anspruchsverlauf in der anspruchspipeline gesteuert werden. Während die anspruchspipeline um ein eher logisches Konzept des ist angeblich der zur Implementierung-zu-Ende-Prozess für den anspruchsverlauf handelt, Anspruchsregeln ein tatsächliches administratives Element handelt, das Sie verwenden können, um den Fluss der anspruchsverlauf im anspruchsausstellungsprozess anpassen.  
  
Weitere Informationen zur anspruchspipeline finden Sie unter [The Role of the Claims Engine ](The-Role-of-the-Claims-Engine.md).  
  
Anspruchsregeln bieten folgende Vorteile:  
  
-   Bereitstellen eines Mechanismus für Administratoren ausführen Zeit Geschäftslogik für vertrauende Ansprüche von Anspruchsanbietern anwenden  
  
-   Bereitstellen eines Mechanismus für Administratoren definieren, welche Ansprüche für vertrauende Seiten ausgegeben werden  
  
-   Bereitstellen von aussagekräftigen und detaillierten Claims\-basierte Autorisierungsfunktionen für Administratoren, die Zugriff zulassen oder Verweigern des Zugriffs auf bestimmte Benutzer möchten  
  
### <a name="how-claim-rules-are-processed"></a>Verarbeiten von Anspruchsregeln  
Anspruchsregeln werden verarbeitet, über die Pipeline mithilfe der *anspruchsmodul *. Das anspruchsmodul ist eine logische Komponente des Verbunddiensts, die den Satz von eingehenden Ansprüche von einem Benutzer untersucht, und klicken Sie dann abhängig von der Logik in jeder Regel, erzeugt einen ausgabeanspruchssatz von Ansprüchen.  
  
Regel, die Ansprüche zusammen, die-Modul und der Anspruch auf eine bestimmte Vertrauensstellung zugeordnete Regeln zu ermitteln, ob die eingehenden Ansprüche weitergegeben werden, um eine bestimmte Bedingung Kriterien gefiltert oder werden in einen vollständig neuen Satz von Ansprüchen transformiert werden, bevor sie durch den Verbunddienst als ausgehende Ansprüche ausgestellt werden.  
  
Weitere Informationen zu diesem Prozess finden Sie unter [The Role of the Claims Engine ](The-Role-of-the-Claims-Engine.md).  
  
## <a name="what-are-claim-rule-templates"></a>Was sind anspruchsregelvorlagen?  
AD FS enthält einen vordefinierten Satz von anspruchsregelvorlagen Vorlagen, die entwickelt wurden, können Sie ganz einfach auswählen und erstellen die am besten geeigneten Anspruchsregeln für Ihre spezifischen Anforderungen Ihres Unternehmens. Anspruchsregelvorlagen Sie werden beim Erstellen der Anspruch Regel nur Vorlagen verwendet werden.  
  
In der AD FS-Verwaltungs-Snap-In können Regeln nur erstellt werden, mithilfe von anspruchsregelvorlagen wurde. Nachdem Sie das Snap-In zum verwenden eine anspruchsregelvorlage auswählen, die erforderlichen Daten für die Regellogik und auf die Konfigurationsdatenbank speichern, werden \ (von diesem Punkt Forward\) gemäß der Benutzeroberfläche als Anspruchsregel.  
  
### <a name="how-claim-rule-templates-work"></a>Wie von anspruchsregelvorlagen  
Auf den ersten Blick erscheinen anspruchsregelvorlagen nur Eingabeformulare, die durch das Snap-In zum Sammeln von Daten und prozessspezifischer Logik für eingehende Ansprüche bereitgestellt werden. Fordern Sie jedoch ausführlichere Ebene speichern anspruchsregelvorlagen die erforderlichen Anspruch Framework für die Sie die grundlegende Logik zum Erstellen einer Regel ohne tiefgehende wissen, die Sprache erforderlich machen.  
  
Jede Vorlage, die in der Benutzeroberfläche bereitgestellt wird, stellt \(UI\) eine vordefinierte Syntax anspruchsregelsprache, basierend auf der am häufigsten erforderlichen administrativen Aufgaben. Gibt es eine Regelvorlage jedoch, die eine Ausnahme. Diese Vorlage wird als benutzerdefinierte Regelvorlage bezeichnet. Mit dieser Vorlage wird enthält keine vordefinierte Syntax. Stattdessen müssen Sie die Syntax der anspruchsregelsprache im Hauptteil der Anspruch Vorlagenformular mithilfe der Syntax der anspruchsregelsprache direkt erstellen.  
  
Weitere Informationen zur Verwendung der Syntax der anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md) in AD FS-Bereitstellungshandbuch.  
  
> [!TIP]  
> Sie können anzeigen, die anspruchsregelsprache einer Regel zugeordnete jederzeit durch Klicken auf die **Regelsprache anzeigen** auf die Eigenschaften einer Anspruchsregel auf die Schaltfläche.  
  
### <a name="how-to-create-a-claim-rule"></a>Vorgehensweise beim Erstellen einer Anspruchsregel  
Anspruchsregeln werden separat für jede Verbund-vertrauensstellungsbeziehung innerhalb des Verbunddiensts erstellt und sind nicht mehreren Vertrauensstellungen gemeinsam verwendet. Sie können entweder eine Regel aus einer anspruchsregelvorlage erstellen, von Grund auf neu starten, erstellen Sie die Regel mithilfe der anspruchsregelsprache oder mithilfe von Windows PowerShell eine Regel anpassen.  
  
Alle diese Optionen zusammen verwendet werden, um Ihnen die Flexibilität, die geeignete Methode für ein bestimmtes Szenario bieten. Weitere Informationen zur Vorgehensweise beim Erstellen einer Anspruchsregel finden Sie unter [Anspruchsregeln konfigurieren](https://technet.microsoft.com/library/ee913571.aspx) im AD FSDeployment Bereitstellungshandbuch.  
  
#### <a name="using-claim-rule-templates"></a>Verwenden von anspruchsregelvorlagen  
Anspruchsregelvorlagen Sie werden beim Erstellen der Anspruch Regel nur Vorlagen verwendet werden. Sie können eine der folgenden Vorlagen verwenden, um eine Anspruchsregel erstellen:  
  
-   Weiterleiten oder Filtern eines eingehenden Anspruchs  
  
-   Transformieren eines eingehenden Anspruchs  
  
-   LDAP-Attributen als Ansprüche senden  
  
-   Senden der Gruppenmitgliedschaft als Anspruch  
  
-   Senden von Ansprüchen mit benutzerdefinierter Regel  
  
-   Zulassen oder Verweigern von Benutzern anhand eines eingehenden Anspruchs  
  
-   Alle Benutzer zulassen  
  
Für Weitere Informationen zu einzelnen anspruchsregelvorlagen finden Sie unter [bestimmen Sie den Typ der Anspruch Regelvorlage verwenden](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).  
  
#### <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
Für Geschäftsregeln, die außerhalb des Bereichs des Standard-anspruchsregelvorlage sind, können Sie eine benutzerdefinierte Regelvorlage auf eine Reihe komplexer logikbedingungen mithilfe der anspruchsregelsprache Express. Weitere Informationen zur Verwendung einer benutzerdefinierten Regel finden Sie unter [verwenden eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
#### <a name="using-windows-powershell"></a>Mithilfe von WindowsPowerShell  
Sie können auch das Cmdlet-Objekt ADFSClaimRuleSet mit Windows PowerShell verwenden, erstellen oder Verwalten von Regeln in AD FS. Weitere Informationen darüber, wie Sie Windows PowerShell mit diesem Cmdlet verwenden können, finden Sie unter [AD FS-Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
## <a name="what-is-a-claim-rule-set"></a>Was ist ein anspruchsregelsatz?  
Wie in der folgenden Abbildunggezeigt, ist ein anspruchsregelsatz eine Gruppierung von einer oder mehreren Regeln für eine angegebene verbundvertrauensstellung, die definieren, wie Ansprüche durch das anspruchsregelmodul verarbeitet werden. Beim Empfang eines eingehenden Anspruchs durch den Verbunddienst wendet das anspruchsregelmodul die Logik, die durch den entsprechenden anspruchsregelsatz angegeben. Es ist das Endergebnis der Logik aller Regeln in der Gruppe, die bestimmt, wie Ansprüche für eine bestimmte Vertrauensstellung in ihrer Gesamtheit ausgegeben werden.  
  
![AD FS-Rollen](media/adfs2_claimruleset.gif)  
  
Anspruchsregeln werden vom anspruchsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Diese Reihenfolge ist wichtig, da die Ausgabe einer Regel als Eingabe für die nächste Regel im Satz verwendet werden kann.  
  
## <a name="what-are-claim-rule-set-types"></a>Was sind anspruchsregelsatz festlegen?  
Ein anspruchsregelsatz-Typ ist ein logisches Segment einer verbundvertrauensstellung, die kategorisch angibt, ob der der Vertrauensstellung zugeordnete anspruchsregelsatz für Ansprüche Ausstellung, Autorisierung oder Akzeptanz verwendet wird. Jeder verbundvertrauensstellung kann eine oder mehrere anspruchsregelsatz-Typen zugeordnet, je nach den Typ der Vertrauensstellung, die verwendet wird.  
  
In der folgende Tabelle werden die verschiedenen Typen von anspruchsregelsätzen beschrieben und erläutert deren Beziehung zu entweder einer Anspruchsanbieter-Vertrauensstellung oder Vertrauensstellung der vertrauenden Seite.  
  
|Anspruchsregelsatz-Typ|Beschreibung|Auf verwendet|  
|-----------------------|---------------|-----------|  
|Akzeptanztransformations-Regelsatz|Eine Reihe von Anspruchsregeln, mit denen Sie auf eine bestimmte Anspruchsanbieter-Vertrauensstellung angeben, die eingehenden Ansprüche, die von der Organisation des Anspruchsanbieters akzeptiert werden und die ausgehenden Ansprüche, die an die Vertrauensstellung der vertrauenden Seite gesendet werden.<br /><br />Die eingehenden Ansprüche, die verwendet werden, um diesen Regelsatz source werden die Ansprüche, die von der ausstellungstransformations-Regelsatz gemäß der Angabe in der Organisation des Anspruchsanbieters ausgegeben werden.<br /><br />Standardmäßig die Ansprüche enthält einer Anspruch Anspruchsanbieter-Vertrauensstellung mit dem Namen **Active Directory** dem verwendet, um den quellattributspeicher für den akzeptanztransformations-Regelsatz darzustellen. Dieses Vertrauensstellungsobjekt wird verwendet, um die Verbindung von Ihrem Verbunddienst in einer Active Directory-Datenbank in Ihrem Netzwerk darzustellen. Diese Standardeinstellung Vertrauensstellung ist, was verarbeitet Ansprüche für Benutzer, die von Active Directory authentifiziert wurden, und kann nicht gelöscht werden.|Anspruchsanbieter-Vertrauensstellungen|  
|Ausstellungstransformations-Regelsatz|Eine Reihe von Anspruchsregeln, die Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Ansprüche anzugeben, die auf die vertrauende Seite ausgegeben wird.<br /><br />Die eingehenden Ansprüche, die verwendet werden, um diesen Regelsatz source werden die Ansprüche, die Ausgabe der akzeptanztransformationsregeln sind.|Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen|  
|Ausstellungsautorisierungs-Regelsatz|Eine Reihe von Anspruchsregeln, die Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Benutzer anzugeben, die ein Token für die vertrauende Seite empfangen dürfen.<br /><br />Diese Regeln bestimmen, ob ein Benutzer Ansprüche für eine vertrauende Seite und somit den Zugriff auf die vertrauende Seite empfangen kann.<br /><br />Wenn Sie keine ausstellungsautorisierungsregel angeben, werden alle Benutzer Zugriff standardmäßig verweigert.|Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen|  
|Delegationsautorisierungs-Regelsatz|Eine Reihe von Anspruchsregeln, die Sie für eine Vertrauensstellung der vertrauenden Seite verwenden, um die Benutzer anzugeben, die als Stellvertreter für andere Benutzer auf die vertrauende Seite agieren dürfen.<br /><br />Diese Regeln bestimmen, ob die anfordernde Person zur Annahme der Identität eines Benutzers trotzdem identifiziert die anfordernde Person im Token, das auf die vertrauende Seite gesendet wird zulässig ist.<br /><br />Wenn Sie keine ausstellungsautorisierungsregel angeben, können keine Benutzer standardmäßig als Stellvertreter agieren.|Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen|  
|Identitätswechsel-Regelsatz|Eine Reihe von Anspruch, können Regeln, die Sie konfigurieren mithilfe von Windows PowerShell um zu ermitteln, ob ein Benutzer vollständig, die Identität eines anderen Benutzers auf die vertrauende Seite annehmen.<br /><br />Diese Regeln bestimmen, ob die anfordernde Person zur Annahme der Identität eines Benutzers ohne die Identität der anfordernden Person im Token, das auf die vertrauende Seite gesendet wird zulässig ist.<br /><br />Identität eines anderen Benutzers auf diese Weise ist eine sehr leistungsstarke Funktion, da die vertrauende Seite nicht weiß, dass der Benutzer angenommen wird.|Vertrauensstellung einer vertrauenden Seite|  
  
Weitere Informationen zum auswählen die geeigneten Anspruchsregeln für die Verwendung in Ihrer Organisation finden Sie unter [bestimmen Sie den Typ der Anspruch Regelvorlage verwenden](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).  
  

