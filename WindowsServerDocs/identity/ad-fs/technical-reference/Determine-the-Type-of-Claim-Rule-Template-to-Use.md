---
ms.assetid: 696a29b2-d627-4c9a-a384-9c8aaf50bd23
title: Ermitteln des Typs der zu verwendenden Anspruchsregelvorlage
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: eaf0e9fca9b24eb4e67caa4237efe044937d5831
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407408"
---
# <a name="determine-the-type-of-claim-rule-template-to-use"></a>Ermitteln des Typs der zu verwendenden Anspruchsregelvorlage


Ein wichtiger Bestandteil des Entwurfs einer Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Infrastruktur ist die Bestimmung des kompletten Satzes von Anspruchs Regeln – und der entsprechenden Anspruchs Regel Vorlagen, die Sie verwenden sollten, um Sie zu erstellen – für jeden Partner, der beteiligen Sie sich an einem Verbund mit Ihrer Organisation. Sie erstellen Regeln mithilfe von Anspruchs Regel Vorlagen im AD FS Verwaltungs-Snap @ no__t-0in.  
  
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
In der folgenden Tabelle werden alle Typen von Anspruchs Regel Vorlagen beschrieben, die Sie zum Erstellen von Regeln mithilfe des Snap-Ins "AD FS-Verwaltung" und "no__t-0in" verwenden können, sowie die Vorteile der Verwendung eines Vorlagen Typs für einen anderen.  
  
|Regelvorlagentyp|Beschreibung|Vorteile|Nachteile|  
|----------------------|---------------|--------------|-----------------|  
|Durchlauf oder Filtern eines eingehenden Anspruchs|Dient zum Erstellen einer Regel, die alle Anspruchswerte für einen ausgewählten Anspruchstyp weiterleitet oder Ansprüche basierend auf Anspruchswerten filtert, sodass nur bestimmte Anspruchswerte für einen ausgewählten Anspruchstyp weitergeleitet werden.<br /><br />Weitere Informationen finden Sie unter [Verwendung einer Pass-Through or Filter Claim Rule](When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md).|-Kann verwendet werden, um bestimmte Ansprüche auszuwählen, die akzeptiert oder unverändert ausgestellt werden sollen.|-Anspruchstyp und-Wert können nicht geändert werden.|  
|Eingehenden Anspruch transformieren|Dient zum Erstellen einer Regel, die einen eingehenden Anspruch auswählen und ihn einem anderen Anspruchstyp zuordnen kann. Außerdem kann der Anspruchswert einem neuen Anspruchswert zugeordnet werden.<br /><br />Weitere Informationen finden Sie unter [wann Use a Transform Claim Rule](When-to-Use-a-Transform-Claim-Rule.md).|-Kann verwendet werden, um Anspruchs Typen oder-Werte zu normalisieren.<br />-Kann ein e @ no__t-0mail-Suffix eines eingehenden Anspruchs ersetzen|-Komplexere Zeichen folgen Ersetzungen erfordern eine benutzerdefinierte Regel.|  
|LDAP-Attribute als Ansprüche senden|Dient zum Erstellen einer Regel, die Attribute in einem LDAP-Attributspeicher zum Senden als Ansprüche an die vertrauende Seite auswählt.<br /><br />Weitere Informationen finden Sie unter [wann verwenden Sie eine Send LDAP Attributes as Claims Rule](When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md).|-Kann Ansprüche aus beliebigen AD DS @ no__t-0ad LDS-Attribut Speicher aufrufen<br />: Mehrere Ansprüche können mithilfe einer einzigen Regel ausgegeben werden.|-Leistung – aufgrund der Konto Suche langsam<br />-Kann keinen benutzerdefinierten LDAP-Filter für Abfragen verwenden.|  
|Gruppenmitgliedschaft als Anspruch senden|Wird verwendet, um eine Regel zu erstellen, die einen angegebenen Anspruchstyp und -wert senden kann, wenn ein Benutzer Mitglied einer Active Directory-Sicherheitsgruppe ist. Wenn diese Regel verwendet wird, wird nur ein einzelner Anspruch auf Grundlage der ausgewählten Gruppe gesendet.<br /><br />Weitere Informationen finden Sie unter [verwenden ein Senden der Gruppenmitgliedschaft als Anspruchsregel](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md).|-Schnelle Leistung beim Ausstellen von Gruppen Ansprüchen – keine Konto Suche|-Der Benutzer muss Mitglied einer lokalen Active Directory Gruppe sein.|  
|Senden von Ansprüchen mit benutzerdefinierter Regel|Wird verwendet, um eine benutzerdefinierte Regel zu erstellen, die mehr erweiterte Optionen als eine Standardregelvorlage bietet. Sie schreiben benutzerdefinierte Regeln mit der AD FS Anspruchs Regel Sprache.<br /><br />Weitere Informationen finden Sie unter [verwenden Sie eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).|-Kann verwendet werden, um Ansprüche aus einem SQL-Attribut Speicher zu beziehen.<br />-Kann verwendet werden, um einen benutzerdefinierten LDAP-Filter anzugeben.<br />-Kann verwendet werden, um eine PPID auszugeben.<br />-Kann mit einem benutzerdefinierten Attribut Speicher verwendet werden.<br />-Kann verwendet werden, um nur dem Eingangs Anspruchssatz Ansprüche hinzuzufügen.<br />-Kann verwendet werden, um Ansprüche basierend auf mehr als einem eingehenden Anspruch zu senden.|-Es ist schwieriger, \- zu konfigurieren, da möglicherweise eine Anlaufzeit erforderlich ist, um zunächst Kenntnis der Anspruchs Regel Sprache zu erhalten.|  
|Benutzer auf der Grundlage eines eingehenden Anspruchs zulassen oder verweigern|Wird verwendet, um eine Regel zu erstellen, die Benutzern den Zugriff auf die vertrauende Seite auf Grundlage von Typ und Wert eines eingehenden Anspruchs gewährt oder zu verweigert.<br /><br />Weitere Informationen finden Sie unter [wann Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md).|-Vereinfacht den Autorisierungs Prozess|: Erfordert, dass nur ein Anspruchstyp und ein Anspruchs Wert angegeben werden.<br />: Unterstützt keinen Musterabgleich für Anspruchs Werte.|  
|Alle Benutzer zulassen|Wird verwendet, um eine Regel erstellen, die allen Benutzern den Zugriff auf die vertrauende Seite ermöglicht.<br /><br />Weitere Informationen finden Sie unter [wann Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md).|-Einfach zu konfigurieren|-Weniger sicher als die Verwendung der Vorlage "Benutzer auf Basis eines eingehenden Anspruchs zulassen oder verweigern"|  
  

