---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: Zusammenhangloser Namespace
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b21e849bb69068f66b1b80c6b1a3afbdef91459f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822533"
---
# <a name="disjoint-namespace"></a>Zusammenhangloser Namespace

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein Zusammenhang loser Namespace tritt auf, wenn ein oder mehrere Domänen Mitglieds Computer ein primäres Domain Name Service-Suffix (DNS) aufweisen, das nicht dem DNS-Namen der Active Directory Domäne entspricht, der die Computer angehören. Beispielsweise verwendet ein Mitglieds Computer, der ein primäres DNS-Suffix von Corp.fabrikam.com in einer Active Directory Domäne mit dem Namen na.Corp.fabrikam.com verwendet, einen Zusammenhang losen Namespace.  
  
Ein Zusammenhang loser Namespace ist komplexer für die Verwaltung, Wartung und Problembehandlung als ein zusammenhängender Namespace. In einem zusammenhängenden Namespace stimmt das primäre DNS-Suffix mit dem Active Directory Domänen Namen überein. Netzwerkanwendungen, die so geschrieben werden, dass der Active Directory-Namespace mit dem primären DNS-Suffix für alle Domänen Mitglieds Computer identisch ist, funktionieren in einem Zusammenhang losen Namespace nicht ordnungsgemäß.  
  
## <a name="support-for-disjoint-namespaces"></a>Unterstützung für disjunkt-Namespaces  
Domänen Mitglieds Computer, einschließlich Domänen Controllern, können in einem Zusammenhang losen Namespace funktionieren. Domänen Mitglieds Computer können Ihren Host (A)-Ressourcen Daten Satz und den IPv6 (IPv6)-Host (AAAA)-Ressourcen Daten Satz in einem nicht Zusammenhang losen DNS-Namespace registrieren. Wenn Domänen Mitglieds Computer Ihre Ressourcen Einträge auf diese Weise registrieren, registrieren Domänen Controller weiterhin globale und standortspezifische Dienst Ressourcen Einträge (SRV) in der DNS-Zone, die mit dem Active Directory Domänen Namen identisch sind.  
  
Nehmen wir beispielsweise an, dass ein Domänen Controller für die Active Directory Domäne mit dem Namen na.Corp.fabrikam.com, die ein primäres DNS-Suffix von Corp.fabrikam.com verwendet, Host-(a) und IPv6-Host Ressourcen Einträge (AAAA) in der Corp.fabrikam.com DNS-Zone registriert. Der Domänen Controller registriert weiterhin globale und standortspezifische Dienst Ressourcen Einträge (SRV) in den DNS-Zonen _msdcs. na. Corp. fabrikam. com und na.Corp.fabrikam.com, wodurch der Dienst Speicherort möglich wird.  
  
> [!IMPORTANT]  
> Obwohl Windows-Betriebssysteme möglicherweise einen Zusammenhang losen Namespace unterstützen, werden Anwendungen, die so geschrieben werden, dass das primäre DNS-Suffix mit dem Active Directory Domänen Suffix identisch ist, in einer solchen Umgebung möglicherweise nicht funktionieren. Aus diesem Grund sollten Sie alle Anwendungen und ihre jeweiligen Betriebssysteme sorgfältig testen, bevor Sie einen Zusammenhang losen Namespace bereitstellen.  
  
Ein Zusammenhang loser Namespace sollte in den folgenden Situationen funktionieren (und wird unterstützt):  
  
-   Wenn eine Gesamtstruktur mit mehreren Active Directory Domänen einen einzelnen DNS-Namespace verwendet, der auch als DNS-Zone bezeichnet wird  
  
    Ein Beispiel hierfür ist ein Unternehmen, das regionale Domänen mit Namen wie na.Corp.fabrikam.com, Sa.Corp.fabrikam.com und Asia.Corp.fabrikam.com verwendet und einen einzelnen DNS-Namespace verwendet, z. b. Corp.fabrikam.com.  
  
-   Wenn eine einzelne Active Directory Domäne in separate DNS-Namespaces aufgeteilt wird  
  
    Ein Beispiel hierfür ist ein Unternehmen mit einer Active Directory Domäne corp.contoso.com, die DNS-Zonen wie HR.Corp.contoso.com, Production.Corp.contoso.com und IT.Corp.contoso.com verwendet.  
  
Ein Zusammenhang loser Namespace funktioniert in folgenden Situationen nicht ordnungsgemäß (und wird nicht unterstützt):  
  
-   Ein disjunktsuffix, das von Domänen Mitgliedern verwendet wird, entspricht einem Active Directory Domänen Namen in dieser oder einer anderen Gesamtstruktur Dadurch wird das Kerberos-Name-Suffix-Routing unterbrochen.  
  
-   Das gleiche Zusammenhang lose Suffix wird in einer anderen Gesamtstruktur verwendet. Dies verhindert, dass diese Suffixe zwischen Gesamtstrukturen eindeutig weitergereicht werden.  
  
-   Wenn der voll qualifizierte Domänen Name (Fully Qualified Domain Name, FQDN) eines Domänen Mitglieds-Zertifizierungsstellen Servers geändert wird, so dass er nicht mehr dasselbe primäre DNS-Suffix verwendet, das von den Domänen Controllern der Domäne verwendet wird, der der Zertifizierungsstellen Server angehört. In diesem Fall haben Sie möglicherweise Probleme beim Überprüfen von Zertifikaten, die der Zertifizierungsstellen Server ausgestellt hat, abhängig von den DNS-Namen, die in den CRL-Verteilungs Punkten verwendet werden. Wenn Sie einen Zertifizierungsstellen Server jedoch in einem stabilen, zusammenhängenden Namespace platzieren, funktioniert dieser ordnungsgemäß und wird unterstützt.  
  
## <a name="considerations-for-disjoint-namespaces"></a>Überlegungen zu Zusammenhang losen Namespaces  
Die folgenden Überlegungen können Ihnen bei der Entscheidung helfen, ob Sie einen Zusammenhang losen Namespace verwenden sollten.  
  
### <a name="application-compatibility"></a>Anwendungskompatibilität  
Wie bereits erwähnt, kann ein zusammenhängender Namespace Probleme für alle Anwendungen und Dienste verursachen, die geschrieben werden, um davon auszugehen, dass das primäre DNS-Suffix eines Computers mit dem Namen des Domänen namens identisch ist, dem er angehört. Bevor Sie einen Zusammenhang losen Namespace bereitstellen, müssen Sie Anwendungen auf Kompatibilitätsprobleme überprüfen. Überprüfen Sie außerdem die Kompatibilität aller Anwendungen, die Sie beim Durchführen der Analyse verwenden. Dies schließt Anwendungen von Microsoft und anderen Softwareentwicklern ein.  
  
### <a name="advantages-of-disjoint-namespaces"></a>Vorteile von disjunkten Namespaces  
Die Verwendung eines Zusammenhang losen Namespace kann folgende Vorteile haben:  
  
-   Da das primäre DNS-Suffix eines Computers unterschiedliche Informationen anzeigen kann, können Sie den DNS-Namespace getrennt vom Active Directory Domänen Namen verwalten.  
  
-   Sie können den DNS-Namespace basierend auf der Geschäftsstruktur oder dem geografischen Standort aufteilen. Beispielsweise können Sie den Namespace basierend auf den Namen von Geschäftseinheiten oder dem physischen Standort (z. b. Kontinent, Land/Region oder Gebäude) aufteilen.  
  
### <a name="disadvantages-of-disjoint-namespaces"></a>Nachteile von disjunkten Namespaces  
Die Verwendung eines Zusammenhang losen Namespace kann folgende Nachteile haben:  
  
-   Sie müssen separate DNS-Zonen für jede Active Directory Domäne in der Gesamtstruktur erstellen und verwalten, die über Mitglieds Computer mit einem Zusammenhang losen Namespace verfügt. (Das heißt, es ist eine zusätzliche und komplexere Konfiguration erforderlich.)  
  
-   Sie müssen manuelle Schritte ausführen, um das Active Directory-Attribut zu ändern und zu verwalten, mit dem Domänen Mitglieder bestimmte primäre DNS-Suffixe verwenden können.  
  
-   Um die Namensauflösung zu optimieren, müssen Sie manuelle Schritte zum Ändern und Verwalten von Gruppenrichtlinie durchführen, um Mitglieds Computer mit alternativen primären DNS-Suffixen zu konfigurieren.  
  
    > [!NOTE]  
    > Der Windows Internet Name Service (WINS) kann verwendet werden, um diesen Nachteil durch Auflösen von Namen mit nur einer Bezeichnung auszugleichen. Weitere Informationen zu WINS finden Sie in der technischen Referenz zu WINS ([https://go.microsoft.com/fwlink/?LinkId=102303](https://go.microsoft.com/fwlink/?LinkId=102303)).  
  
-   Wenn Ihre Umgebung mehrere primäre DNS-Suffixe erfordert, müssen Sie die DNS-Suffixsuchreihenfolge für alle Active Directory Domänen in der Gesamtstruktur entsprechend konfigurieren.  
  
    Um die Such Reihenfolge für das DNS-Suffix festzulegen, können Sie Gruppenrichtlinie Objekte oder DHCP-Server Dienst Parameter (Dynamic Host Configuration Protocol) verwenden. Sie können auch die Registrierung ändern.  
  
-   Sie müssen alle Anwendungen sorgfältig auf Kompatibilitätsprobleme testen.  
  
Weitere Informationen zu den Schritten, die Sie ergreifen können, um diese Nachteile zu beheben, finden Sie unter Erstellen eines disjunkten Namespace ([https://go.microsoft.com/fwlink/?LinkId=106638](https://go.microsoft.com/fwlink/?LinkId=106638)).  
  
### <a name="planning-a-namespace-transition"></a>Planen eines Namespace Übergangs  
Bevor Sie einen Namespace ändern, überprüfen Sie die folgenden Überlegungen, die für Übergänge von zusammenhängenden Namespaces zu disjunkten Namespaces (oder umgekehrt) gelten:  
  
-   Manuell konfigurierte Dienst Prinzipal Namen (SPNs) Stimmen nach einer Namespace Änderung möglicherweise nicht mehr mit DNS-Namen ab. Dies kann zu Authentifizierungs Fehlern führen.  
  
    Weitere Informationen finden Sie unter Dienst Anmeldungen schlagen aufgrund falsch fest gelegender SPNs ([https://go.microsoft.com/fwlink/?LinkId=102304](https://go.microsoft.com/fwlink/?LinkId=102304)) fehl.  
  
    -   Wenn Sie Windows Server 2003-basierte Computer mit eingeschränkter Delegierung verwenden, ist für diese Computer möglicherweise eine zusätzliche Konfiguration erforderlich, um SPNs zu ändern. Weitere Informationen finden Sie im Artikel 936628 in der Microsoft Knowledge Base ([https://go.microsoft.com/fwlink/?LinkId=102306](https://go.microsoft.com/fwlink/?LinkId=102306)).  
  
    -   Wenn Sie Berechtigungen zum Ändern von SPNs für untergeordnete Administratoren delegieren möchten, finden Sie weitere Informationen unter Delegieren der Autorisierungs Stelle zum Ändern von SPNs ([https://go.microsoft.com/fwlink/?LinkId=106639](https://go.microsoft.com/fwlink/?LinkId=106639)).  
  
-   Wenn Sie Lightweight Directory Access Protocol (LDAP) über Secure Sockets Layer (SSL) (LDAPS) mit einer Zertifizierungsstelle in einer Bereitstellung verwenden, die über Domänen Controller verfügt, die in einem Zusammenhang losen Namespace konfiguriert sind, müssen Sie beim Konfigurieren der LDAPS-Zertifikate den entsprechenden Active Directory Domänen Namen und das primäre DNS-Suffix verwenden.  
  
    Weitere Informationen zu Domänen Controller-Zertifikat Anforderungen finden Sie im Artikel 321051 in der Microsoft Knowledge Base ([https://go.microsoft.com/fwlink/?LinkId=102307](https://go.microsoft.com/fwlink/?LinkId=102307)).  
  
    > [!NOTE]  
    > Für Domänen Controller, die Zertifikate für LDAPS verwenden, müssen Sie möglicherweise Ihre Zertifikate erneut bereitstellen. Wenn Sie dies tun, wird von Domänen Controllern möglicherweise erst ein entsprechendes Zertifikat ausgewählt, wenn Sie neu gestartet werden. Weitere Informationen zur LDAPS-Authentifizierung und ein zugehöriges Update für Windows Server 2003 finden Sie im Artikel 932834 der Microsoft Knowledge Base ([https://go.microsoft.com/fwlink/?LinkId=102308](https://go.microsoft.com/fwlink/?LinkId=102308)).  
  
### <a name="planning-for-disjoint-namespace-deployments"></a>Planen von zusammenhängenden Namespace Bereitstellungen  
Treffen Sie die folgenden Vorsichtsmaßnahmen, wenn Sie Computer in einer Umgebung bereitstellen, die über einen Zusammenhang losen Namespace verfügt:  
  
1.  Benachrichtigen Sie alle Softwarehersteller, bei denen Sie Geschäfte ausführen müssen und einen Zusammenhang losen Namespace unterstützen müssen. Bitten Sie Sie, zu überprüfen, ob Sie Ihre Anwendungen in Umgebungen unterstützen, die nicht zusammenhängende Namespaces verwenden.  
  
2.  Testen Sie alle Versionen von Betriebssystemen und Anwendungen in Zusammenhang losen Namespace-Lab-Umgebungen. Befolgen Sie dabei die folgenden Empfehlungen:  
  
    1.  Beheben Sie alle Software Probleme, bevor Sie die Software in Ihrer Umgebung bereitstellen.  
  
    2.  Wenn möglich, nehmen Sie an Beta Tests von Betriebssystemen und Anwendungen Teil, die Sie in nicht zusammenhängenden Namespaces bereitstellen möchten.  
  
3.  Stellen Sie sicher, dass Administratoren und Helpdeskmitarbeiter den Zusammenhang losen Namespace und seine Auswirkung kennen.  
  
4.  Erstellen Sie einen Plan, der es Ihnen ermöglicht, bei Bedarf von einem zusammenhängenden Namespace zu einem zusammenhängenden Namespace zu wechseln.  
  
5.  Evangelisieren Sie die Wichtigkeit der disjunkten Unterstützung von Namespaces mit Betriebssystem-und Anwendungsanbietern.  
  


