---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: Zusammenhangloser Namespace
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0a2e911e889343b05a515c94e615d3648289f2df
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883571"
---
# <a name="disjoint-namespace"></a>Zusammenhangloser Namespace

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein zusammenhangloser Namespace tritt auf, wenn eine oder mehrere Domänenmitgliedscomputer ein primäres Suffix des Domain Name Service (DNS), das nicht mit den DNS-Namen des Active Directory-Domäne übereinstimmt, von denen die Computer angehören. Beispielsweise verwendet ein Mitgliedscomputer, ein primäres DNS-Suffix "corp.Fabrikam.com" in einer Active Directory-Domäne, die mit der Bezeichnung "na.corp.Fabrikam.com" einen zusammenhanglosen Namespace.  
  
Ein zusammenhangloser Namespace ist schwieriger zu verwalten, Verwaltung und Problembehandlung als einen zusammenhängenden Namespace. In einem zusammenhängenden Namespace entspricht das primäre DNS-Suffix der Active Directory-Domänennamen an. Anwendungen, die geschrieben werden, davon ausgehen, dass die Active Directory-Namespace mit das primäre DNS-Suffix für alle Domänenmitgliedscomputer identisch ist funktionieren nicht ordnungsgemäß in einem zusammenhanglosen Namespace.  
  
## <a name="support-for-disjoint-namespaces"></a>Unterstützung für nicht zusammenhängende namespaces  
Domänenmitgliedscomputer, einschließlich Domänencontrollern, können in einem zusammenhanglosen Namespace fungieren. Domänenmitgliedscomputer können registrieren, dem Host (A)-Ressourceneintrag und IP-Version 6 (IPv6) hosten (AAAA)-Ressourcendatensatz in einem zusammenhanglosen DNS-Namespace. Wenn Domänenmitgliedscomputer ihre Ressourceneinträge auf diese Weise registrieren, können Sie weiterhin Domänencontroller globale und standortspezifische Dienstidentifizierungs-Ressourceneinträge in der DNS-Zone zu registrieren, die in den Active Directory-Domänennamen identisch ist.  
  
Nehmen wir beispielsweise an, dass ein Domänencontroller für Active Directory-Domäne mit dem Namen Bezeichnung "na.corp.Fabrikam.com", die eine primäre DNS-"corp.Fabrikam.com Suffix" in der DNS-Zone "corp.Fabrikam.com" Host (A) und Ressourceneinträge für IPv6-Host (AAAA) registriert. Der Domänencontroller weiterhin in _msdcs.na.corp.fabrikam.com und die Bezeichnung "na.corp.Fabrikam.com" DNS-Zonen, globale und standortspezifische Dienstidentifizierungs-Ressourceneinträge zu registrieren, wodurch dienstidentifizierung möglich.  
  
> [!IMPORTANT]  
> Auch wenn Windows-Betriebssysteme einen zusammenhanglosen Namespace unterstützt, funktionieren Anwendungen, die geschrieben werden, davon ausgehen, dass das primäre DNS-Suffix der Active Directory-Domänen-Suffix entspricht nicht in einer solchen Umgebung. Aus diesem Grund sollten Sie testen alle Anwendungen und ihre jeweiligen Betriebssysteme sorgfältig, bevor Sie mit einen zusammenhanglosen Namespace bereitstellen.  
  
Ein zusammenhangloser Namespace sollte funktionieren (und wird unterstützt) in den folgenden Situationen:  
  
-   Bei Verwendung eine Gesamtstruktur mit mehreren Active Directory-Domänen für einen einzelnen DNS-Namespace handelt es sich auch eine DNS-zone  
  
    Ein Beispiel hierfür ist ein Unternehmen, das verwendet Regionaldomänen mit Namen wie die Bezeichnung "na.corp.Fabrikam.com" sa.corp.fabrikam.com und asia.corp.fabrikam.com und einen einzigen DNS-Namespace, z. B. "corp.Fabrikam.com".  
  
-   Wenn eine einzelne Active Directory-Domäne in separaten DNS-Namespaces aufgeteilt ist  
  
    Ein Beispiel hierfür ist ein Unternehmen mit Active Directory-Domäne "corp.contoso.com", die DNS-Zonen, z. B. hr.corp.contoso.com production.corp.contoso.com und it.corp.contoso.com verwendet.  
  
Ein zusammenhangloser Namespace nicht ordnungsgemäß funktioniert (und wird nicht unterstützt) in den folgenden Situationen:  
  
-   Ein zusammenhangloser Suffix ein, die Mitglieder der Domäne entspricht, einen Active Directory-Domänennamen in dieser oder einer anderen Gesamtstruktur. Dies unterbricht Kerberos Namensuffix routing.  
  
-   Das gleiche zusammenhanglose Suffix wird in einer anderen Gesamtstruktur verwendet. Dies verhindert, dass diese Suffixe eindeutig zwischen Gesamtstrukturen routing.  
  
-   Wenn ändert Mitgliedsservers einer Domäne Zertifizierungsstelle (ZS) der vollständig qualifizierte Domänenname (FQDN), damit es nicht mehr verwenden das gleiche primäre DNS-Suffix, das verwendet wird, von den Domänencontrollern der Domäne, der der CA-Server Mitglied ist. In diesem Fall müssen Sie Probleme, die Überprüfung von Zertifikaten möglicherweise den CA-Server ausgegeben werden, je nachdem welche DNS-Namen in den Zertifikatsperrlisten-Verteilungspunkte verwendet werden. Aber wenn Sie einen stabilen zusammenhanglosen Namespace einen Zertifizierungsstellenserver versehen, diese ordnungsgemäß funktioniert und unterstützt wird.  
  
## <a name="considerations-for-disjoint-namespaces"></a>Überlegungen zu zusammenhanglosen namespaces  
Die folgenden Überlegungen helfen Ihnen die Entscheidung, ob Sie einen zusammenhanglosen Namespace verwenden sollten.  
  
### <a name="application-compatibility"></a>Anwendungskompatibilität  
Wie bereits erwähnt kann ein zusammenhangloser Namespace Probleme für beliebige Anwendungen und Dienste, die geschrieben werden, davon ausgehen, dass ein primäres DNS-Suffix des Computers mit den Namen der Domäne identisch ist, von denen er Mitglied ist. Bevor Sie einen zusammenhanglosen Namespace bereitstellen, müssen Sie die Anwendungen auf Kompatibilitätsprobleme prüfen. Darüber hinaus werden Sie sicher, dass die Kompatibilität aller Anwendungen, die Sie verwenden, wenn Sie Ihre Analyse ausführen, zu überprüfen. Dazu gehören Anwendungen von Microsoft und anderer Software-Entwickler.  
  
### <a name="advantages-of-disjoint-namespaces"></a>Vorteile von nicht zusammenhängenden namespaces  
Mit einem zusammenhanglosen Namespace haben die folgenden Vorteile:  
  
-   Da das primäre DNS-Suffix eines Computers auf andere Informationen angeben kann, können Sie den DNS-Namespace aus dem Active Directory-Domänennamen separat verwalten.  
  
-   Sie können die DNS-Namespace auf Grundlage der Unternehmensstruktur oder geografischen Standort trennen. Beispielsweise können Sie den Namespace, die basierend auf Business Unit-Namen oder physischen Standort wie Kontinent, Land/Region und Erstellen von trennen.  
  
### <a name="disadvantages-of-disjoint-namespaces"></a>Nachteile von nicht zusammenhängenden namespaces  
Mit einem zusammenhanglosen Namespace haben folgende Nachteile:  
  
-   Sie müssen erstellen und Verwalten von separaten DNS-Zonen für jede Active Directory-Domäne in der Gesamtstruktur mit Computern, die Mitglieder, die einen nicht zusammenhängenden Namespace verwenden. (D. h. muss es eine zusätzliche und eine komplexere Konfiguration.)  
  
-   Führen Sie manuelle Schritte zum Ändern und Verwalten von Active Directory-Attribut, das Mitglieder der Domäne angegeben wird, primäre DNS-Suffixe verwenden zu können.  
  
-   Um die namensauflösung zu optimieren, müssen Sie manuelle Schritte zum Ändern und Verwalten von Gruppenrichtlinien zum Konfigurieren von Computern, die Mitglieder in alternativen primären DNS-Suffixe ausführen.  
  
    > [!NOTE]  
    > Windows Internet Name Service (WINS) konnte für den offset dieser Nachteil durch Auflösen von Namen mit einfacher Bezeichnung verwendet werden. Weitere Informationen zu WINS, finden Sie unter technische Referenz WINS ([https://go.microsoft.com/fwlink/?LinkId=102303](https://go.microsoft.com/fwlink/?LinkId=102303)).  
  
-   Wenn Ihre Umgebung mehrere primäre DNS-Suffixe erforderlich sind, müssen Sie die DNS-Suffix-Suchreihenfolge für alle Active Directory-Domänen in der Gesamtstruktur entsprechend konfigurieren.  
  
    Um die DNS-Suffix-Suchreihenfolge festzulegen, können Sie Gruppenrichtlinienobjekte oder Dynamic Host Configuration Protocol (DHCP) Server-Service-Parameter. Sie können auch die Registrierung ändern.  
  
-   Sie müssen alle Anwendungen für Kompatibilitätsprobleme sorgfältig testen.  
  
Weitere Informationen zu Schritten, die Sie ergreifen können, um diese Nachteile zu beheben, finden Sie unter Erstellen ein Zusammenhangloser Namespace ([https://go.microsoft.com/fwlink/?LinkId=106638](https://go.microsoft.com/fwlink/?LinkId=106638)).  
  
### <a name="planning-a-namespace-transition"></a>Planen einen Namespace-Übergang  
Bevor Sie einen Namespace ändern, überprüfen Sie die folgenden Aspekte, die angewendet werden, geht aus zusammenhängenden Namespaces zu zusammenhanglosen Namespaces (oder umgekehrt):  
  
-   Manuell konfiguriert möglicherweise Dienstprinzipalnamen (SPN) nicht mehr übereinstimmen DNS-Namen nach einer Änderung des Namespace. Dies kann zu Authentifizierungsfehlern führen.  
  
    Weitere Informationen finden Sie unter Service Anmeldungen Fehler aufgrund von SPNs nicht ordnungsgemäß festgelegt ([https://go.microsoft.com/fwlink/?LinkId=102304](https://go.microsoft.com/fwlink/?LinkId=102304)).  
  
    -   Wenn Sie Windows Server 2003-basierte Computer bei der eingeschränkten Delegierung verwenden, erfordern diese Computer zusätzliche Konfiguration so ändern Sie die SPNs. Weitere Informationen finden Sie in der Microsoft Knowledge Base-Artikel 936628 ([https://go.microsoft.com/fwlink/?LinkId=102306](https://go.microsoft.com/fwlink/?LinkId=102306)).  
  
    -   Wenn Sie Berechtigungen zum Ändern von SPNs zu untergeordneten Administratoren delegieren möchten, finden Sie unter Delegieren der Autorität mit SPNs ändern ([https://go.microsoft.com/fwlink/?LinkId=106639](https://go.microsoft.com/fwlink/?LinkId=106639)).  
  
-   Wenn Sie Lightweight Directory Access Protocol (LDAP) über Secure Sockets Layer (SSL) (bekannt als LDAPS) mit einer Zertifizierungsstelle in einer Bereitstellung, die Domänencontroller installiert sind, die in einem zusammenhanglosen Namespace konfiguriert sind verwenden, müssen Sie die Namen der entsprechenden Active Directory-Domäne verwenden und primäre DNS-Suffix, beim Konfigurieren der LDAPS-Zertifikate.  
  
    Weitere Informationen zu domänencontrolleranforderungen Zertifikat finden Sie in der Microsoft Knowledge Base-Artikel 321051 ([https://go.microsoft.com/fwlink/?LinkId=102307](https://go.microsoft.com/fwlink/?LinkId=102307)).  
  
    > [!NOTE]  
    > Domänencontroller, auf denen Zertifikate für die LDAPS verwenden unter Umständen ihre Zertifikate erneut bereitgestellt. Wenn Sie dies tun, können Domänencontroller kein entsprechendes Zertifikat auswählen, bis Sie sie neu gestartet werden. Weitere Informationen über LDAPS-Authentifizierung und einen zugehörigen Updates für Windows Server 2003 finden Sie in der Microsoft Knowledge Base-Artikel 932834 ([https://go.microsoft.com/fwlink/?LinkId=102308](https://go.microsoft.com/fwlink/?LinkId=102308)).  
  
### <a name="planning-for-disjoint-namespace-deployments"></a>Zusammenhangloser Namespace liegt auch Bereitstellungen planen  
Wenn Sie Computer in einer Umgebung bereitstellen, die einen zusammenhanglosen Namespace aufweist, führen Sie die folgenden Vorsichtsmaßnahmen:  
  
1.  Benachrichtigen Sie alle Softwarehersteller, mit denen Sie Handel treiben, müssen sie testen und einen zusammenhanglosen Namespace unterstützt. Bitten sie stellen Sie sicher, dass sie ihre Anwendungen in Umgebungen unterstützen, die nicht zusammenhängenden Namespaces verwenden.  
  
2.  Testen Sie alle Versionen von Betriebssystemen und Anwendungen in Lab-Umgebungen nicht zusammenhängenden Namespace. Wenn Sie dies tun, befolgen Sie diese Empfehlungen:  
  
    1.  Beheben Sie alle Probleme mit Software, bevor Sie die Software in Ihrer Umgebung bereitstellen.  
  
    2.  Wenn möglich, teilnehmen von Beta-Tests von Betriebssystemen und Anwendungen, die Sie in nicht zusammenhängende Namespaces bereitstellen möchten.  
  
3.  Stellen Sie sicher, dass Administratoren und Helpdesk-Mitarbeiter die zusammenhanglosen Namespace und dessen Auswirkungen bekannt sind.  
  
4.  Erstellen Sie einen Plan, der Sie für den Übergang von einem zusammenhanglosen Namespace einem zusammenhängenden Namespace bei Bedarf ermöglicht.  
  
5.  Übertragen Sie die Wichtigkeit der zusammenhanglosen Namespace-Unterstützung mit Betriebssystem und Anbieter von Anwendungen.  
  


