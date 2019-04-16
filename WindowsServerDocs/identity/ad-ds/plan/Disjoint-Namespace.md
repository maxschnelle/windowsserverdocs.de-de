---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: "Nicht zusammenhängenden Namespace"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac231dbfbaaeafa39199e29a1744d84d5cec23e8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="disjoint-namespace"></a>Nicht zusammenhängenden Namespace

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Ein separater Namespace tritt auf, wenn ein oder mehrere Computer ein primäres Suffix des Domain Name Service (DNS), das nicht mit den DNS-Namen der Active Directory-Domäne übereinstimmt, von denen die Computer angehören. Ein Mitgliedscomputer, ein primäres DNS-Suffix des corp.fabrikam.com in einer Active Directory-Domäne mit dem Namen na.corp.fabrikam.com wird z.B. einen separaten Namespace verwendet.  
  
Ein separaten Namespace ist schwieriger zu verwalten, verwalten und behandeln als einen zusammenhängenden Namespace. In einen zusammenhängenden Namespace entspricht das primäre DNS-Suffix der Active Directory-Domänennamen. Netzwerkanwendungen, die geschrieben werden, um wird davon ausgegangen, dass die Active Directory-Namespace das primäre DNS-Suffix für alle Domänenmitgliedscomputer entspricht funktionieren nicht ordnungsgemäß in einem separaten Namespace.  
  
## <a name="support-for-disjoint-namespaces"></a>Unterstützung für separaten Namespaces  
Domänenmitgliedscomputer, einschließlich Domänencontrollern, können in einem separaten Namespace fungieren. Domänenmitgliedscomputer können registrieren, dem Host (A)-Ressourceneintrag und IP-Version 6 (IPv6) (AAAA)-Ressourceneintrag in einem separaten DNS-Namespace hosten. Wenn Domänenmitgliedscomputer Ressourceneinträge auf diese Weise registrieren, können Sie weiterhin Domänencontroller global und standortspezifische Dienste (SRV)-Ressourceneinträge in DNS-Zone zu registrieren, die in den Active Directory-Domänennamen identisch ist.  
  
Nehmen wir beispielsweise an, dass ein Domänencontroller für Active Directory-Domäne mit dem Namen na.corp.fabrikam.com, das primäres DNS-Suffix corp.fabrikam.com verwendet in der DNS-Zone corp.fabrikam.com Host (A) und IPv6-Host (AAAA) registriert. Der Domänencontroller weiterhin registriert Ressourceneinträge für globale und standortspezifische Dienste (SRV) in der _msdcs. na.corp.fabrikam.com und na.corp.fabrikam.com DNS-Zonen, wodurch Dienstsuche möglich ist.  
  
> [!IMPORTANT]  
> Auch Windows-Betriebssystemen einen separaten Namespace unterstützt, funktionieren Clientanwendungen, die davon ausgehen, dass das primäre DNS-Suffix identisch mit dem Active Directory-Domänensuffix ist geschrieben werden möglicherweise nicht in einer solchen Umgebung. Aus diesem Grund sollten Sie testen alle Anwendungen und ihre jeweiligen Betriebssysteme sorgfältig vor der Bereitstellung von eines separaten Namespaces.  
  
Ein separaten Namespace sollte funktionieren (und wird unterstützt) in den folgenden Situationen:  
  
-   Wenn einen einzelnen DNS-Namespace, der auch bekannt als eine DNS-Zone ist verwendet eine Gesamtstruktur mit mehreren Active Directory-Domänen  
  
    Ein Beispiel hierfür ist ein Unternehmen, das verwendet Regionaldomänen mit Namen wie na.corp.fabrikam.com, sa.corp.fabrikam.com und asia.corp.fabrikam.com und einen DNS-Namespace, z.B. corp.fabrikam.com.  
  
-   Wenn eine einzelne Active Directory-Domäne in separate DNS-Namespaces unterteilt wird  
  
    Ein Beispiel hierfür ist ein Unternehmen mit Active Directory-Domäne des corp.contoso.com, die DNS-Zonen wie hr.corp.contoso.com, production.corp.contoso.com und it.corp.contoso.com verwendet.  
  
Ein separaten Namespace funktioniert nicht ordnungsgemäß (und wird nicht unterstützt) in den folgenden Situationen:  
  
-   Einen separaten Suffix von Domänenmitgliedern verwendet entspricht einen Active Directory-Domänennamen in dieser oder einer anderen Gesamtstruktur. Dadurch wird die Kerberos-Namensuffix Routing unterbrochen.  
  
-   Das Gleiche separaten Suffix wird in einer anderen Gesamtstruktur verwendet. Dies verhindert, dass diese Suffixe eindeutig zwischen Gesamtstrukturen Routing.  
  
-   Bei einer Domäne Mitglied-Zertifizierungsstelle (CA) qualifizierte serveränderungen ist es vollständig Domänennamen (FQDN), damit er nicht mehr verwendet die gleiche primäre DNS-Suffix, das von den Domänencontrollern der Domäne an, der der CA-Server angehört, verwendet wird. In diesem Fall müssen Sie Probleme, die Überprüfung von Zertifikaten möglicherweise den CA-Server ausgestellt werden, je nachdem, welche DNS-Namen in den Zertifikatsperrlisten-Verteilungspunkte verwendet werden. Aber wenn Sie einen Zertifizierungsstellenserver in einem stabilen zusammenhanglosen Namespace platzieren, ordnungsgemäß funktioniert und wird unterstützt.  
  
## <a name="considerations-for-disjoint-namespaces"></a>Überlegungen für zusammenhanglosen Namespaces  
Folgendes helfen Ihnen die Entscheidung, ob Sie einen separaten Namespace verwendet werden soll.  
  
### <a name="application-compatibility"></a>Die Anwendungskompatibilität  
Wie bereits erwähnt kann ein separaten Namespace Probleme für alle Anwendungen und Dienste, die davon ausgehen, dass ein primäres DNS-Suffix des Computers mit dem Namen des Domänennamens identisch ist, deren Mitglied ist, geschrieben werden. Bevor Sie einen separaten Namespace bereitstellen, müssen Sie Anwendungen für Kompatibilitätsprobleme überprüfen. Werden Sie darüber hinaus sicher, dass Sie die Kompatibilität aller Anwendungen zu überprüfen, die Sie verwenden, wenn Sie Ihre Analyse durchzuführen. Dazu gehören Anwendungen von Microsoft und von anderen Softwareentwicklern.  
  
### <a name="advantages-of-disjoint-namespaces"></a>Vorteile von zusammenhanglosen Namespaces  
Mit einem separaten Namespace können die folgenden Vorteile:  
  
-   Da das primäre DNS-Suffix eines Computers verschiedene Informationen anzeigen kann, können Sie den DNS-Namespace aus den Active Directory-Domänennamen separat verwalten.  
  
-   Sie können den DNS-Namespace, die basierend auf Unternehmensstruktur oder geografischen Standort trennen. Beispielsweise können Sie den Namespace basierend auf den Unternehmensnamen Einheit oder physischen Speicherort, z.B. Kontinent, Land/Region oder Erstellung trennen.  
  
### <a name="disadvantages-of-disjoint-namespaces"></a>Nachteile der zusammenhanglosen Namespaces  
Mit einem separaten Namespace können die folgenden Nachteile:  
  
-   Sie müssen erstellen und Verwalten von separaten DNS-Zonen für jede Active Directory-Domäne in der Gesamtstruktur mit Computern, die Mitglieder, die einen nicht zusammenhängenden Namespace verwenden. (Das heißt, benötigt es eine zusätzliche, komplexere Konfiguration.)  
  
-   Führen Sie die manuelle Schrittezum Ändern und Verwalten von Active Directory-Attribut, das Mitglieder der Domäne angegeben, das primäre DNS-Suffixe verwenden kann.  
  
-   Um die Namensauflösung zu optimieren, müssen Sie manuelle Schrittezum Ändern und Verwalten von Gruppenrichtlinien zum Konfigurieren von Computern, die Mitglieder mit anderen primären DNS-Suffixe ausführen.  
  
    > [!NOTE]  
    > Dieser Nachteil Offset von Auflösen von Namen mit einfacher Bezeichnung kann Windows Internet Name Service (WINS) verwendet werden. Weitere Informationen zu WINS finden Sie unter der WINS-Technical Reference ([https://go.microsoft.com/fwlink/?LinkId=102303](https://go.microsoft.com/fwlink/?LinkId=102303)).  
  
-   Wenn Ihre Umgebung mehrere primäre DNS-Suffixe erforderlich sind, müssen Sie die DNS-Suffix-Suchreihenfolge für alle von Active Directory-Domänen in der Gesamtstruktur entsprechend konfigurieren.  
  
    Die DNS-Suffix-Suchreihenfolge festlegen möchten, können Sie Group Policy Objects oder Dienstparameter Dynamic Host Configuration-Protokoll (DHCP) Server verwenden. Sie können auch die Registrierung ändern.  
  
-   Sie müssen sorgfältig alle Anwendungen auf Kompatibilitätsprobleme testen.  
  
Weitere Informationen zu den Schritten, die Sie ergreifen können um diese Nachteile zu beheben, finden Sie unter Erstellen einer separaten Namespace ([https://go.microsoft.com/fwlink/?LinkId=106638](https://go.microsoft.com/fwlink/?LinkId=106638)).  
  
### <a name="planning-a-namespace-transition"></a>Planen einen Namespace Übergang  
Bevor Sie einen Namespace ändern, überprüfen Sie die folgenden Aspekte, die für Übergänge aus zusammenhängenden Namespaces zusammenhanglosen Namespaces (oder umgekehrt) gelten:  
  
-   Manuell konfigurierte möglicherweise Dienstprinzipalnamen (SPN) nicht mehr DNS-Namen nach einer Namespaceänderung übereinstimmen. Dies kann zu Authentifizierungsfehlern führen.  
  
    Weitere Informationen finden Sie unter Service Anmeldungen Fehler aufgrund falsch Set SPNs ([https://go.microsoft.com/fwlink/?LinkId=102304](https://go.microsoft.com/fwlink/?LinkId=102304)).  
  
    -   Wenn Sie Windows Server2003-basierten Computern mithilfe der eingeschränkten Delegierung verwenden, können diese Computer zusätzliche Konfiguration so ändern Sie den Dienstprinzipalnamen (SPN) erforderlich. Weitere Informationen finden Sie in der Microsoft Knowledge Base-Artikel 936628 ([https://go.microsoft.com/fwlink/?LinkId=102306](https://go.microsoft.com/fwlink/?LinkId=102306)).  
  
    -   Wenn Sie Berechtigungen zum Ändern der Dienstprinzipalnamen (SPN), um Administratoren untergeordnete delegieren möchten, finden Sie unter Delegieren von Berechtigungen zum Ändern von Dienstprinzipalnamen (SPN) ([https://go.microsoft.com/fwlink/?LinkId=106639](https://go.microsoft.com/fwlink/?LinkId=106639)).  
  
-   Wenn Sie über Secure Sockets Layer (SSL) (bekannt als LDAPS) mit einer Zertifizierungsstelle in einer Bereitstellung Lightweight Directory Access Protocol (LDAP), die Domänencontroller verfügt, die in einem separaten Namespace konfiguriert sind verwenden, müssen Sie die entsprechenden Active Directory-Domänennamen und das primäre DNS-Suffix verwenden, wenn Sie die Zertifikate LDAPS konfigurieren.  
  
    Weitere Informationen zu Domain Controller-Zertifikatanforderungen finden Sie im Artikel 321051 in der Microsoft Knowledge Base ([https://go.microsoft.com/fwlink/?LinkId=102307](https://go.microsoft.com/fwlink/?LinkId=102307)).  
  
    > [!NOTE]  
    > Domänencontroller, die Verwendung von Zertifikaten für LDAPS müssen Sie ihre Zertifikate erneut bereitstellen. Wenn Sie dies tun, können Domänencontroller kein entsprechendes Zertifikat auswählen, bis sie neu gestartet werden. Weitere Informationen zur LDAPS Authentifizierung und eine entsprechende Update für Windows Server2003 finden Sie in der Microsoft Knowledge Base-Artikel 932834 ([https://go.microsoft.com/fwlink/?LinkId=102308](https://go.microsoft.com/fwlink/?LinkId=102308)).  
  
### <a name="planning-for-disjoint-namespace-deployments"></a>Planen von separaten Namespace-Bereitstellungen  
Wenn Sie Computer in einer Umgebung bereitstellen, die über einen separaten Namespace verfügt, führen Sie die folgenden Vorsichtsmaßnahmen:  
  
1.  Benachrichtigen Sie alle Softwarehersteller, mit denen Sie Geschäfte, die sie testen und einen separaten Namespace unterstützen müssen. Bitten Sie sie überprüfen, ob ihre Anwendungen unterstützen sie in Umgebungen, die nicht zusammenhängenden Namespace verwenden.  
  
2.  Testen Sie alle Versionen von Betriebssystemen und Anwendungen in zusammenhanglosen Lab. Wenn Sie dies tun, beachten Sie folgende Empfehlungen:  
  
    1.  Beheben Sie alle Probleme mit Software, bevor Sie die Software in Ihrer Umgebung bereitstellen.  
  
    2.  Wenn möglich, Teilnahme am Beta-Tests von Betriebssystemen und Anwendungen, die Sie in separaten Namespaces bereitstellen möchten.  
  
3.  Stellen Sie sicher, dass Administratoren und Helpdeskmitarbeiter separaten Namespace und dessen Auswirkungen kennen.  
  
4.  Erstellen Sie einen Plan, der Sie für den Übergang von einem separaten Namespace zu einem zusammenhängenden Namespace, bei Bedarf ermöglicht.  
  
5.  Werben Sie die Bedeutung der zusammenhanglosen Namespaceunterstützung für Betriebssystem und App-Anbieter.  
  


