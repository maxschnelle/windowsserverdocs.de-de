---
ms.assetid: 696a29b2-d627-4c9a-a384-9c8aaf50bd23
title: Bestimmen Sie die Art der Anspruchsregelvorlage verwenden
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 129cd83be4cd8302bd170ba87aad58c50f636006
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="determine-the-type-of-claim-rule-template-to-use"></a>Bestimmen Sie die Art der Anspruchsregelvorlage verwenden

>Gilt für: Windows Server 2016, Windows Server2012 R2

Ein wichtiger Teil beim Entwerfen einer Infrastruktur für Active Directory Federation Services \(AD FS\) ist das Bestimmen von Anspruchsregeln – und der entsprechenden anspruchsregelvorlagen, sollten Sie zu ihrer Erstellung verwenden – für jeden Partner, die im Verbund mit Ihrer Organisation einbezogen werden. Sie können Regeln mithilfe von anspruchsregelvorlagen in AD FS-Verwaltungs-Snap-In erstellen.  
  
Jede Gruppe von Anspruchsregeln, die Sie konfigurieren, kann nur einer verbundvertrauensstellung zugeordnet werden. Dies bedeutet, dass Sie keinen Satz von Regeln für eine Vertrauensstellung erstellen und für andere Vertrauensstellungen in Ihrem Verbunddienst zu verwenden. Stattdessen können Sie leicht Regeln von anspruchsregelvorlagen erstellen Regelvorlagen können Sie schnell eine bestimmte Gruppe von Ansprüchen zu erstellen, die zwischen den einzelnen Verbundpartnern und Ihrer Organisation vereinbart sind.  
  
Weitere Informationen zu Regeln und Regelvorlagen finden Sie unter [The Role of Claim Rules](The-Role-of-Claim-Rules.md).  
  
Bevor Sie beginnen, welche Arten von anspruchsregelvorlagen, die Sie verwenden sollten, berücksichtigen Sie die folgenden Fragen:  
  
-   Welche Ansprüche werden von Ihren vertrauenswürdigen Anspruchsanbietern bereitgestellt?  
  
-   Welche Ansprüche vertrauen Sie von jedem Anspruchsanbieter?  
  
-   Welche Ansprüche von den vertrauenden Seiten erforderlich sind, die diesem Verbunddienst vertrauen?  
  
-   Welche Ansprüche Sie auf jede vertrauende Seite preisgeben sind?  
  
-   Welche Benutzer Zugriff auf jede vertrauende Seite haben sollen?  
  
Diese Fragen beantwortet werden Hilfe Sie einen soliden planen Regel Design anfordern. Es wird auch erstellen eine reibungslose Autorisierung und entwickeln und dem Bereitstellungsteam effizienter während der Einführung.  
  
Im nächsten Abschnitt, die Sie für Ihre Umgebung basierend auf Ihr Unternehmen die Art der Regelvorlagen erfahren auswählen muss.  
  
## <a name="claim-rule-template-types"></a>Regel Vorlage Anspruchstypen  
Die folgende Tabelle enthält alle Typen von anspruchsregelvorlagen, die Sie zum Erstellen von Regeln, die mit AD FS-Verwaltungs-Snap-In verwenden können, und geben Sie die Vorteile der Verwendung einer Vorlage über ein anderes.  
  
|Regelvorlagentyp|Beschreibung|Vorteile|Nachteile|  
|----------------------|---------------|--------------|-----------------|  
|Weiterleiten oder Filtern eines eingehenden Anspruchs|Verwendet, um eine Regel erstellen, die alle Anspruchswerte für einen ausgewählten Anspruchstyp weiterleiten oder Filtern von Ansprüchen basierend auf anspruchswerten, sodass nur bestimmte Anspruchswerte für einen ausgewählten Anspruchstyp weitergeleitet werden.<br /><br />Weitere Informationen finden Sie unter [verwenden einen Pass-Through or Filter Claim Rule](When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md).|-Werden kann, wählen Sie bestimmte Ansprüche akzeptiert oder ausgestellt werden unverändert|-Anspruch, Typ und Wert geändert werden können|  
|Transformieren eines eingehenden Anspruchs|Verwendet, um eine Regel erstellen, die können einen eingehenden Anspruch auswählen und einem anderen Anspruchstyp zuordnen oder der Anspruchswert einem neuen Anspruchswert zugeordnet.<br /><br />Weitere Informationen finden Sie unter [a Transform Claim Rule verwenden](When-to-Use-a-Transform-Claim-Rule.md).|-Kann verwendet werden, um Anspruchstypen oder -Werte zu normalisieren.<br />-Eine E\ E-Mail-Suffix eines eingehenden Anspruchs kann ersetzt werden.|-Komplexere zeichenfolgenersetzungen erfordern eine benutzerdefinierte Regel|  
|LDAP-Attributen als Ansprüche senden|Verwendet, um eine Regel erstellen, die Attribute aus einem LDAP-Attributspeicher zum Senden als Ansprüche an die vertrauende Seite auswählen.<br /><br />Weitere Informationen finden Sie unter [a Send LDAP Attributes as Claims Rule verwenden](When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md).|-Ansprüche aus jeder AD DS\/AD LDS-Attributspeichers können beziehen werden.<br />-Mehrere Ansprüche können mithilfe einer einzigen Regel ausgestellt werden|-Langsame Leistung als Folge der kontosuche<br />-Einen benutzerdefinierte LDAP-Filter kann nicht für Abfragen verwenden werden.|  
|Senden der Gruppenmitgliedschaft als Anspruch|Verwendet, um eine Regel erstellen, die einen angegebenen Anspruchstyp und -Wert senden kann, wenn ein Benutzer Mitglied einer Active Directory-Sicherheitsgruppe ist. Nur ein einzelner Anspruch wird mit dieser Regel, basierend auf der ausgewählten Gruppe gesendet.<br /><br />Weitere Informationen finden Sie unter [ein Senden der Gruppenmitgliedschaft als Anspruchsregel Verwendung](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md).|-Schnelle Leistung für das Ausstellen von Gruppenansprüchen, keine kontosuche.|-Benutzer muss ein Mitglied einer lokalen Active Directory-Gruppe sein.|  
|Senden von Ansprüchen mit benutzerdefinierter Regel|Verwendet, um eine benutzerdefinierte Regel erstellen, die mehr erweiterte Optionen als eine standardregelvorlage bereitstellt. Sie schreiben benutzerdefinierte Regeln mit der AD FS regelsprache geltend machen.<br /><br />Weitere Informationen finden Sie unter [verwenden eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).|-Können verwendet werden, um Ansprüche aus einem SQL-Attributspeicher beziehen<br />-Kann verwendet werden, um einen benutzerdefinierten LDAP-Filter anzugeben<br />-Kann verwendet werden, um eine PPID auszustellen.<br />-Kann mit einem benutzerdefinierten Attributspeicher verwendet werden<br />-Kann verwendet werden, um nur dem eingangsanspruchssatz Ansprüche hinzuzufügen.<br />-Kann verwendet werden, um Ansprüche basierend auf mehr als einem eingehenden Anspruch senden|-Schwieriger konfigurieren \-einige Zeit möglicherweise werden erforderlich um anfänglich Kenntnisse in der anspruchsregelsprache zu erhalten|  
|Zulassen oder Verweigern von Benutzern anhand eines eingehenden Anspruchs|Erstellen Sie eine Regel, die zulassen oder Verweigern des Zugriffs von Benutzern auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs wird verwendet.<br /><br />Weitere Informationen finden Sie unter [Wann sollte eine Autorisierungsanspruchsregel verwendet](When-to-Use-an-Authorization-Claim-Rule.md).|-Vereinfacht den Autorisierungsprozess|– Erfordert, dass nur ein Anspruchstyp und -Wert Anspruch angegeben werden<br />-Für den Mustervergleich für Anspruchswerte wird nicht unterstützt werden.|  
|Alle Benutzer zulassen|Verwendet, um eine Regel erstellen, die allen Benutzern Zugriff auf die vertrauende Seite ermöglicht.<br /><br />Weitere Informationen finden Sie unter [Wann sollte eine Autorisierungsanspruchsregel verwendet](When-to-Use-an-Authorization-Claim-Rule.md).|– Einfach zu konfigurieren.|-Weniger sicher als die zulassen oder verweigern Benutzer basierend auf einer Vorlage eingehenden Anspruchs|  
  

