---
ms.assetid: 696a29b2-d627-4c9a-a384-9c8aaf50bd23
title: Ermitteln des Typs der zu verwendenden Anspruchsregelvorlage
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 129cd83be4cd8302bd170ba87aad58c50f636006
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815851"
---
# <a name="determine-the-type-of-claim-rule-template-to-use"></a>Ermitteln des Typs der zu verwendenden Anspruchsregelvorlage

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Ein wichtiger Teil beim Entwerfen einer Active Directory Federation Services \(AD FS\) Infrastruktur ist das Bestimmen von Anspruchsregeln – und der entsprechenden anspruchsregelvorlagen können Sie sollten diese erstellen – für jeden Partner im Verbund mit Ihrer Organisation einbezogen wird. Sie können Regeln erstellen, mithilfe von anspruchsregelvorlagen im AD FS-Verwaltungs-Snap-\-in.  
  
Jede Gruppe von Anspruchsregeln, die Sie konfigurieren, kann nur einer Verbundvertrauensstellung zugeordnet werden. Dies bedeutet, dass Sie keinen Regelsatz für eine Vertrauensstellung erstellen und diese für andere Vertrauensstellungen in Ihrem Verbunddienst verwenden können. Stattdessen können Sie Regeln problemlos anhand von Anspruchsregelvorlagen erstellen, um eine gewünschte Gruppe von Ansprüchen schneller zu generieren, die zwischen den einzelnen Verbundpartnern und Ihrer Organisation vereinbart wurden.  
  
Weitere Informationen zu Regeln und Regelvorlagen finden Sie unter [The Role of Claim Rules](The-Role-of-Claim-Rules.md).  
  
Bevor Sie beginnen, die Arten von Anspruchsregelvorlagen zu bestimmen, die verwendet werden sollten, stellen Sie sich die folgenden Fragen:  
  
-   Welche Ansprüche werden von Ihren vertrauenswürdigen Anspruchsanbietern bereitgestellt?  
  
-   Welchen Ansprüchen des jeweiligen Anspruchsanbieters vertrauen Sie?  
  
-   Welche Ansprüche werden von den vertrauenden Seiten angefordert, die diesem Verbunddienst vertrauen?  
  
-   Welche Ansprüche möchten Sie jeder vertrauenden Seite preisgeben?  
  
-   Welche Benutzer sollen Zugriff auf jede vertrauende Seite haben?  
  
Durch die Beantwortung dieser Fragen können Sie einen soliden Anspruchsregelentwurf planen. Außerdem können Sie eine überzeugende Autorisierungs- und Zugriffssteuerungsstrategie besser entwickeln und dem Bereitstellungsteam eine effizientere Einführung ermöglichen.  
  
Im nächsten Abschnitt lernen Sie den Typ von Regelvorlagen kennen, den Sie für Ihre Umgebung basierend auf Ihren Geschäftsanforderungen auswählen müssen.  
  
## <a name="claim-rule-template-types"></a>Typen von Anspruchsregelvorlagen  
Die folgende Tabelle beschreibt alle Typen von anspruchsregelvorlagen, mit denen Sie zum Erstellen von Regeln, die mit der AD FS-Verwaltungs-Snap\-in, und die Vorteile der Verwendung einer Vorlage über ein anderes.  
  
|Regelvorlagentyp|Beschreibung|Vorteile|Nachteile|  
|----------------------|---------------|--------------|-----------------|  
|Durchlauf oder Filtern eines eingehenden Anspruchs|Dient zum Erstellen einer Regel, die alle Anspruchswerte für einen ausgewählten Anspruchstyp weiterleitet oder Ansprüche basierend auf Anspruchswerten filtert, sodass nur bestimmte Anspruchswerte für einen ausgewählten Anspruchstyp weitergeleitet werden.<br /><br />Weitere Informationen finden Sie unter [When to Use a Pass Through or Filter Claim Rule](When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md).|– Sie können verwendet werden, um Wählen Sie bestimmte Ansprüche akzeptiert oder ausgegeben werden unverändert|-Anspruch, dass der Typ und Wert nicht geändert werden kann|  
|Eingehenden Anspruch transformieren|Dient zum Erstellen einer Regel, die einen eingehenden Anspruch auswählen und ihn einem anderen Anspruchstyp zuordnen kann. Außerdem kann der Anspruchswert einem neuen Anspruchswert zugeordnet werden.<br /><br />Weitere Informationen finden Sie unter [When to Use a Transform Claim Rule](When-to-Use-a-Transform-Claim-Rule.md).|– Sie können verwendet werden, um Anspruchstypen oder-Werte zu normalisieren<br />– Sie können einen e ersetzen\-e-Mail-Suffix eines eingehenden Anspruchs|-Eine komplexere zeichenfolgenersetzungen erfordern eine benutzerdefinierte Regel|  
|LDAP-Attribute als Ansprüche senden|Dient zum Erstellen einer Regel, die Attribute in einem LDAP-Attributspeicher zum Senden als Ansprüche an die vertrauende Seite auswählt.<br /><br />Weitere Informationen finden Sie unter [When to Use a Send LDAP Attributes as Claims Rule](When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md).|– Sie können die Ansprüche aus AD DS-Instanzen source\/AD LDS-attributspeichern<br />-Mehrere Ansprüche können mithilfe einer einzigen Regel ausgestellt werden|-Langsame Leistung als Folge der kontosuche<br />-Einen benutzerdefinierten LDAP-Filter kann nicht für Abfragen verwendet werden.|  
|Gruppenmitgliedschaft als Anspruch senden|Wird verwendet, um eine Regel zu erstellen, die einen angegebenen Anspruchstyp und -wert senden kann, wenn ein Benutzer Mitglied einer Active Directory-Sicherheitsgruppe ist. Wenn diese Regel verwendet wird, wird nur ein einzelner Anspruch auf Grundlage der ausgewählten Gruppe gesendet.<br /><br />Weitere Informationen finden Sie unter [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md).|– Schnelle Leistung für das Ausstellen von Gruppenansprüchen, keine kontosuche.|-Benutzer muss Mitglied einer lokalen Active Directory-Gruppe sein.|  
|Senden von Ansprüchen mit benutzerdefinierter Regel|Wird verwendet, um eine benutzerdefinierte Regel zu erstellen, die mehr erweiterte Optionen als eine Standardregelvorlage bietet. Sie schreiben benutzerdefinierte Regeln mit dem AD FS regelsprache Anspruch.<br /><br />Weitere Informationen finden Sie unter [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md).|– Sie können verwendet werden, um die Ansprüche aus einem SQL-Attributspeicher beziehen<br />– Sie können zum Angeben eines benutzerdefinierten LDAP-Filters verwendet werden<br />– Sie können verwendet werden, um eine PPID auszustellen.<br />– Sie können mit einem benutzerdefinierten Attributspeicher verwendet werden<br />– Sie können verwendet werden, um nur dem eingangsanspruchssatz Ansprüche hinzuzufügen<br />– Sie können zum Senden von Ansprüchen basierend auf mehr als einem eingehenden Anspruch verwendet werden|– Dieser Typ ist schwieriger zu konfigurieren \- zunächst Kenntnisse der anspruchsregelsprache erhalten möglicherweise einige Vorbereitungszeit erforderlich|  
|Benutzer auf der Grundlage eines eingehenden Anspruchs zulassen oder verweigern|Wird verwendet, um eine Regel zu erstellen, die Benutzern den Zugriff auf die vertrauende Seite auf Grundlage von Typ und Wert eines eingehenden Anspruchs gewährt oder zu verweigert.<br /><br />Weitere Informationen finden Sie unter [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md).|-Vereinfacht den Autorisierungsprozess|– Erfordert, dass nur ein Anspruchstyp und einem Anspruchswert angegeben werden<br />-Mustervergleich für Anspruchswerte wird nicht unterstützt werden.|  
|Alle Benutzer zulassen|Wird verwendet, um eine Regel erstellen, die allen Benutzern den Zugriff auf die vertrauende Seite ermöglicht.<br /><br />Weitere Informationen finden Sie unter [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md).|-Einfache konfigurieren|-Weniger sicher als das zulassen oder verweigern Benutzer basierend auf einer Vorlage des eingehenden Anspruchs|  
  

