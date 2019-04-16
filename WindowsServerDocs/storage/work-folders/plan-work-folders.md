---
ms.assetid: a7c39656-81ee-4c2b-80ef-4d017dd11b07
title: Arbeitsordnerbereitstellung planen
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dongill
ms.author: jgerend
ms.date: 4/5/2017
description: "So Planen Sie eine Arbeitsordnerbereitstellung, einschließlich Systemanforderungen und Vorbereitung der Netzwerkumgebung."
ms.openlocfilehash: 877b418439e77e39cbdc6821808e296f977c26dd
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="planning-a-work-folders-deployment"></a>Arbeitsordnerbereitstellung planen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

In diesem Thema wird der Entwurfsprozess für eine Arbeitsordnerimplementierung erläutert. Folgendes Hintergrundwissen wird vorausgesetzt:  
  
-   Grundlegende Kenntnisse von Arbeitsordnern (siehe [Arbeitsordner](work-folders-overview.md))  
  
-   Grundlegende Kenntnisse der Konzepte der Active Directory Domain Services (AD DS)  
  
-   Grundlegende Kenntnisse der Windows-Dateifreigabe und damit zusammenhängender Technologien  
  
-   Grundlegende Kenntnisse der Verwendung von SSL-Zertifikaten  
  
-   Grundlegende Kenntnisse der Aktivierung des Webzugriffs auf interne Ressourcen über einen Webreverseproxy  
  
 In den folgenden Abschnitten wird die Vorgehensweise zum Entwerfen der Arbeitsordnerimplementierung beschrieben. Die Bereitstellung von Arbeitsordnern wird im nächsten Thema, [Bereitstellen von Arbeitsordnern](deploy-work-folders.md), behandelt.  
  
##  <a name="BKMK_SOFT"></a> Softwareanforderungen  

Für Arbeitsordner gelten die folgenden Softwareanforderungen für Dateiserver und die Netzwerkinfrastruktur:  
  
-   Ein Server mit Windows Server2012 R2 oder Windows Server2016 um Hosten von Synchronisierungsfreigaben mit Benutzerdateien  
  
-   Ein mit dem NTFS-Dateisystem formatiertes Volume zum Speichern von Benutzerdateien  
  
-   Sie müssen Kennwortrichtlinien für Gruppenrichtlinien verwenden, um Kennwortrichtlinien auf Computern mit Windows7 zu erzwingen. Sie müssen die Computer mit Windows7 auch aus Kennwortrichtlinien für Arbeitsordner ausschließen (wenn Sie diese verwenden).

-   Ein Serverzertifikat für jeden Dateiserver, der Arbeitsordner hostet. Diese Zertifikate sollten von einer Zertifizierungsstelle (ZS) stammen, die von den Benutzern als vertrauenswürdig eingestuft wird – im Idealfall von einer öffentlichen ZS.

-   (Optional) Eine Active Directory Domain Services-Gesamtstruktur mit Schemaerweiterungen in Windows Server 2012 R2 zum Unterstützen der automatischen Weiterleitung von Computern und Geräten an den korrekten Server, wenn mehrere Server verwendet werden. 
  
Für die von Benutzern durchgeführte Synchronisierung über das Internet gelten die folgenden zusätzlichen Anforderungen:  
  
-   Die Möglichkeit, den Internetzugriff auf einen Server durch Erstellen von Veröffentlichungsregeln im Reverseproxy oder Netzwerkgateway der Organisation zu ermöglichen.  
  
-   (Optional) Ein öffentlich registrierter Domänenname und die Möglichkeit, zusätzliche öffentliche DNS-Einträge für die Domäne zu erstellen.  
  
-   (Optional) Active Directory-Verbunddienste (AD FS)-Infrastruktur bei Verwendung der AD FS-Authentifizierung.  
  
Für Arbeitsordner gelten die folgenden Softwareanforderungen für Clientcomputer:  
  
-   Auf den Computern muss eines der folgenden Betriebssysteme ausgeführt werden:  
  
    -   Windows 10  
  
    -   Windows8.1  
  
    -   WindowsRT 8.1  
  
    -   Windows 7  
  
    -   Android 4.4 KitKat und Nachfolgeversionen  
  
    -   iOS10.2 und höher  
  
-   Computer mit Windows7 müssen eine der folgenden Versionen von Windows ausführen:  
  
    -   Windows 7 Professional  
  
    -   Windows 7 Ultimate  
  
    -   Windows 7 Enterprise  
  
-   Computer mit Windows7 müssen der Domäne Ihrer Organisation hinzugefügt werden (sie können keiner Arbeitsgruppe hinzugefügt werden).  
  
-   Ausreichend freier Speicherplatz auf einem lokalen, mit NTFS formatierten Laufwerk zum Speichern aller Dateien des Benutzers in Arbeitsordnern sowie zusätzliche 6GB freier Speicherplatz, wenn sich Arbeitsordner auf dem Systemlaufwerk befinden (Standard). Arbeitsordner verwendet den folgenden Speicherort als Standardeinstellung: **%USERPROFILE%\Work Folders**  
  
     Benutzer können den Speicherort jedoch während der Installation ändern (mit dem NTFS-Dateisystem formatierte microSD-Karten und USB-Laufwerke werden als Speicherorte unterstützt, die Synchronisierung wird allerdings beendet, wenn die Laufwerke entfernt werden).  
  
     Die maximale Größe für einzelne Dateien beträgt standardmäßig 10 GB. Es gibt keine Speicherbegrenzung pro Benutzer, Administratoren können jedoch mit der Kontingentfunktion des Resource Managers für Dateiserver Kontingente implementieren.  
  
-   Arbeitsordner unterstützen das Zurücksetzen des Status von virtuellen Clientcomputern nicht. Führen Sie Sicherungs- und Wiederherstellungsvorgänge stattdessen innerhalb des virtuellen Clientcomputers mithilfe der Systemabbildsicherung oder einer anderen Sicherungsanwendung durch.  
  
> [!NOTE]
>  Installieren Sie das Windows8.1 und Windows Server2012R2 General Availability-Updaterollup auf allen Arbeitsordnerservern und Clientcomputern, die Windows8.1 und Windows Server2012R2 ausführen. Weitere Informationen finden Sie in der Microsoft Knowledge Base im Artikel [2883200](http://support.microsoft.com/kb/2883200).  
  
## <a name="deployment-scenarios"></a>Bereitstellungsszenarien  
 Arbeitsordner können auf einer beliebigen Anzahl von Dateiservern in einer Kundenumgebung implementiert werden. Dies ermöglicht die Skalierung von Arbeitsordnerimplementierungen entsprechend den Anforderungen des Kunden und somit hochgradig individualisierte Bereitstellungen. Die meisten Bereitstellungen lassen sich jedoch einem der folgenden drei grundlegenden Szenarien zuordnen.  
  
### <a name="single-site-deployment"></a>Bereitstellung mit einem einzigen Standort  
 Bei einer Bereitstellung mit einem einzigen Standort werden Dateiserver an einem zentralen Standort in der Kundeninfrastruktur gehostet. Dieser Bereitstellungstyp ist am häufigsten bei Kunden mit einer hochgradig zentralisierten Infrastruktur oder kleineren Filialen ohne lokale Dateiserver zu finden. Die Verwaltung dieses Bereitstellungsmodells kann für IT-Mitarbeiter einfacher sein, da alle Serverressourcen lokal sind und Internetzugang/-ausgang vermutlich ebenfalls an diesem Standort zentralisiert ist. Das Bereitstellungsmodell erfordert jedoch eine gute WAN-Konnektivität zwischen dem zentralen Standort und Filialen, und bei Benutzern in Filialen sind durch Netzwerkbedingungen verursachte Dienstunterbrechungen möglich.  
  
### <a name="multiple-site-deployment"></a>Bereitstellung mit mehreren Standorten  
 Bei einer Bereitstellung mit mehreren Standorten werden Dateiserver an mehreren Standorten in der Kundeninfrastruktur gehostet. Dabei kann es sich um mehrere Rechenzentren oder Filialen mit eigenen Dateiservern handeln. Dieser Bereitstellungstyp ist am häufigsten in größeren Kundenumgebungen oder bei Kunden mit mehreren großen Filialen mit lokalen Serverressourcen zu finden. Die Verwaltung des Bereitstellungsmodells ist für IT-Mitarbeiter aufwändiger und erfordert eine sorgfältige Koordination der Datenspeicherung und Verwaltung der Active Directory Domain Services (AD DS), um sicherzustellen, dass Benutzer den korrekten Synchronisierungsserver für Arbeitsordner verwenden.  
  
### <a name="hosted-deployment"></a>Gehostete Bereitstellung  
 Bei einer gehosteten Bereitstellung werden Synchronisierungsserver in einer IAAS (Infrastructure-as-a-Service)-Lösung wie einer WindowsAzure-VM bereitgestellt. Diese Bereitstellungsmethode bietet den Vorteil, dass Dateiserver weniger abhängig von der WAN-Konnektivität innerhalb des Unternehmens eines Kunden sind. Wenn ein Gerät eine Verbindung mit dem Internet herstellen kann, kann es den Synchronisierungsserver erreichen. Die in der gehosteten Umgebung bereitgestellten Server müssen aber dennoch die Active Directory-Domäne der Organisation erreichen können, um Benutzer zu authentifizieren. Die lokalen Infrastrukturanforderungen sind somit zwar geringer, aber die Verwaltung der Verbindung ist komplexer.  
  
## <a name="deployment-technologies"></a>Bereitstellungstechnologien  
 Arbeitsordnerbereitstellungen bestehen aus einer Reihe von Technologien, die gemeinsam Dienste für Geräte in den internen und externen Netzwerken bereitstellen. Vor dem Entwerfen einer Arbeitsordnerbereitstellung sollten Kunden sich mit den Anforderungen der folgenden Technologien vertraut machen.  
  
### <a name="active-directory-domain-services"></a>Active Directory Domain Services  
 AD DS bietet zwei wichtige Dienste in einer Arbeitsordnerbereitstellung. Zum einen stellt AD DS als Back-End für die Windows-Authentifizierung die Sicherheits- und Authentifizierungsdienste bereit, mit denen der Zugriff auf Benutzerdaten gewährt wird. Wenn ein Domänencontroller nicht erreicht werden kann, kann ein Dateiserver eine eingehende Anforderung nicht authentifizieren, und das Gerät kann nicht auf Daten zugreifen, die in der Synchronisierungsfreigabe dieses Dateiservers gespeichert sind.  
  
 Zum anderen verwaltet AD DS (mit dem Windows Server 2012 R2-Schemaupdate) das msDS-SyncServerURL-Attribut für jeden Benutzer. Dieses Attribut wird verwendet, um Benutzer automatisch zum entsprechenden Synchronisierungsserver weiterzuleiten.  
  
### <a name="file-servers"></a>Dateiserver  
 Dateiserver unter Windows Server 2012 R2 oder Windows Server 2016 hosten den Rollendienst für Arbeitsordner und die Synchronisierungsfreigaben, in denen Arbeitsordnerdaten von Benutzern gespeichert werden. Dateiserver können auch von anderen im internen Netzwerk verwendeten Technologien gespeicherte Daten hosten (z.B. Dateifreigaben) und gruppiert werden, um Fehlertoleranz für Benutzerdaten bereitzustellen.  
  
###  <a name="GroupPolicy"></a> Gruppenrichtlinie  
 Wenn sich in Ihrer Umgebung Computer mit Windows7 befinden, wird Folgendes empfohlen:  
  
-   Verwenden Sie die Gruppenrichtlinie, um Kennwortrichtlinien für alle zur Domäne hinzugefügten Computer zu steuern, die Arbeitsordner verwenden.  
  
-   Verwenden Sie die Richtlinie **Bildschirm automatisch sperren und ein Kennwort anfordern** für Arbeitsordner auf den Computern, die Ihrer Domäne nicht hinzugefügt wurden.  
  
 Mit Gruppenrichtlinien können Sie auch einen Arbeitsordnerserver für Computer angeben, die einer Domäne angehören. Dies vereinfacht die Einrichtung von Arbeitsordnern ein wenig. Benutzer müssten andernfalls ihre geschäftliche E-Mail-Adresse eingeben, um nach den Einstellungen zu suchen (dies setzt voraus, dass Arbeitsordner korrekt eingerichtet sind), oder die Arbeitsordner-URL, die Sie ihnen explizit per E-Mail oder auf anderem Wege mitgeteilt haben.  
  
 Sie können Gruppenrichtlinien auch verwenden, um die Einrichtung von Arbeitsordnern pro Benutzer oder pro Computer zu erzwingen. Dies führt jedoch dazu, dass Arbeitsordner auf jedem Computer synchronisiert werden, auf dem sich ein Benutzer anmeldet (bei der "Pro Benutzer"-Richtlinieneinstellung), und Benutzer keinen alternativen Speicherort für Arbeitsordner auf ihrem Computer angeben können (z.B. eine microSD-Karte, um Speicherplatz auf dem primären Laufwerk zu sparen). Wir empfehlen, die Anforderungen der Benutzer sorgfältig zu prüfen, bevor Sie eine automatische Einrichtung erzwingen.  
  
### <a name="windows-intune"></a>Windows Intune  
 WindowsIntune stellt eine Sicherheitsschicht bereit und ermöglicht die Verwaltung von Geräten, die keiner Domäne angehören und andernfalls nicht verwaltet werden könnten. Sie können WindowsIntune zum Konfigurieren und Verwalten der persönlichen Geräte von Benutzern verwenden, z.B. Tablets, die über das Internet auf Arbeitsordner zugreifen. WindowsIntune kann die zu verwendende Synchronisierungsserver-URL für Geräte bereitstellen. Andernfalls müssen Benutzer ihre geschäftliche E-Mail-Adresse eingeben, um nach den Einstellungen zu suchen (sofern Sie eine öffentliche Arbeitsordner-URL im Format https://workfolders.*contoso.com* veröffentlichen), oder die Synchronisierungsserver-URL direkt eingeben.  
  
 Ohne eine WindowsIntune-Bereitstellung müssen Benutzer externe Geräte manuell konfigurieren, was zu einer erhöhten Anzahl von Anfragen beim Helpdesk des Kunden führen kann.  
  
 Mit WindowsIntune können Sie auch Daten in Arbeitsordnern auf dem Gerät eines Benutzers selektiv zurücksetzen, ohne dass sich dies auf die übrigen Daten auswirkt. Dies ist hilfreich, wenn ein Benutzer die Organisation verlässt oder ein Gerät gestohlen wird.  
  
### <a name="web-application-proxyazure-ad-application-proxy"></a>Web Application Proxy/Azure AD-Anwendungsproxy  
 Das Konzept von Arbeitsordnern besteht darin, mit dem Internet verbundenen Geräten das sichere Abrufen von Unternehmensdaten aus dem internen Netzwerk zu ermöglichen. Auf diese Weise können Benutzer ihre Daten auf Tablets und Geräten „mitnehmen“, die normalerweise nicht auf Arbeitsdateien zugreifen können. Zu diesem Zweck müssen Synchronisierungsserver-URLs mithilfe eines Reverseproxys veröffentlicht und für Internetclients verfügbar gemacht werden. 
 
Arbeitsordner unterstützen die Verwendung von Web Application Proxy, Azure AD-Anwendungsproxy oder Reverseproxy-Lösung eines Drittanbieters: 

-  Der Webanwendungsproxy ist eine lokale Reverseproxy-Lösung. Weitere Informationen finden Sie unter [Webanwendungsproxy unter Windows Server 2016](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server).  
  
-  Der Azure AD-Anwendungsproxy ist eine Cloud-Reverseproxy-Lösung. Weitere Informationen finden Sie unter [Richtlinien zur Bereitstellung des sicheren Remotezugriffs für lokale Anwendungen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-application-proxy-get-started)

## <a name="additional-design-considerations"></a>Weitere Überlegungen zum Entwurf  
 Nachdem sie sich mit den oben beschriebenen Komponenten vertraut gemacht haben, müssen Kunden beim Entwerfen ihrer Implementierung die Anzahl zu verwendender Synchronisierungsserver und Freigaben bestimmen und entscheiden, ob Failoverclustering genutzt werden soll, um Fehlertoleranz für die Synchronisierungsserver bereitzustellen.  
  
### <a name="number-of-sync-servers"></a>Anzahl von Synchronisierungsservern  
 Ein Kunde kann mehrere Synchronisierungsserver in einer Umgebung ausführen. Eine solche Konfiguration kann aus mehreren Gründen wünschenswert sein:  
  
-   Geografische Verteilung von Benutzern – z.B. Dateiserver in Filialen oder regionale Rechenzentren.  
  
-   Anforderungen an die Datenspeicherung – für bestimmte Unternehmensabteilungen können spezifische Anforderungen bezüglich der Datenspeicherung und -verarbeitung gelten, die sich mit einem dedizierten Server leichter erfüllen lassen.  
  
-   Lastenausgleich – in großen Umgebungen, in denen Benutzerdaten auf mehreren Servern gespeichert werden, kann der Lastenausgleich die Serverleistung und -betriebszeit verbessern.  
  
 Informationen zur Skalierung und Leistung von Arbeitsordnerservern finden Sie unter [Überlegungen zur Leistung von Arbeitsordnerbereitstellungen](http://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx).  
  
> [!NOTE]
>  Bei der Verwendung mehrerer Synchronisierungsserver wird empfohlen, die automatische Serverermittlung für Benutzer einzurichten. Dieser Prozess beruht auf der Konfiguration eines Attributs in jedem Benutzerkonto in ADDS. Dieses Attribut mit dem Namen **msDS-SyncServerURL** wird in Benutzerkonten verfügbar, nachdem der Domäne ein Windows Server 2012 R2-Domänencontroller hinzugefügt wurde oder die Active Directory-Schemaupdates installiert wurden. Das Attribut sollte für alle Benutzer festgelegt werden, um sicherzustellen, dass sie eine Verbindung mit dem korrekten Synchronisierungsserver herstellen. Bei der Verwendung der automatischen Serverermittlung können Organisationen Arbeitsordner unabhängig von der Anzahl verwendeter Synchronisierungsserver mit einer benutzerfreundlichen URL wie *https://workfolders.contoso.com* veröffentlichen.  
  
### <a name="number-of-sync-shares"></a>Anzahl von Synchronisierungsfreigaben  
 Einzelne Synchronisierungsserver können mehrere Synchronisierungsfreigaben hosten. Dies kann aus folgenden Gründen nützlich sein:  
  
-   Überwachungs- und Sicherheitsanforderungen. Wenn von einer bestimmten Abteilung verwendete Daten strikter überwacht oder länger aufbewahrt werden müssen, erleichtern separate Synchronisierungsfreigaben Administratoren die Trennung von Benutzerordnern mit unterschiedlichen Überwachungsebenen.  
  
-   Unterschiedliche Kontingente oder Dateiprüfungen. Wenn Sie unterschiedliche Speicherkontingente bzw. -begrenzungen oder die in Arbeitsordnern zulässigen Dateitypen (Dateiprüfungen) für verschiedene Benutzergruppen festlegen möchten, könne separate Synchronisierungsfreigaben hilfreich sein.  
  
-   Abteilungsspezifische Steuerung. Wenn Administratoraufgaben nach Abteilung aufgeteilt sind, kann die Verwendung separater Freigaben für verschiedene Abteilungen Administratoren das Erzwingen von Kontingenten oder anderer Richtlinien erleichtern.  
  
-   Unterschiedliche Geräterichtlinien. Wenn eine Organisation mehrere Geräterichtlinien (z.B. Verschlüsselung von Arbeitsordnern) für verschiedene Benutzergruppen benötigt, ist dies mithilfe mehrerer Freigaben möglich.  
  
-   Speicherkapazität. Wenn ein Dateiserver über mehrere Volumes verfügt, können zusätzliche Freigaben verwendet werden, um diese zusätzlichen Volumes zu nutzen. Eine einzelne Freigabe hat nur Zugriff auf das Volume, auf dem sie gehostet wird, und kann keine weiteren Volumes auf einem Dateiserver nutzen.  
  
#### <a name="access-to-sync-shares"></a>Zugriff auf Synchronisierungsfreigaben  

Während der Synchronisierungsserver, auf den ein Benutzer zugreift, durch die auf dem Client eingegebene URL (oder die für den Benutzer veröffentlichte URL in ADDS bei Verwendung der automatischen Serverermittlung) bestimmt wird, wird der Zugriff auf einzelne Synchronisierungsfreigaben durch die vorliegenden Berechtigungen für die Freigabe gesteuert.  
  
Wenn ein Kunde mehrere Synchronisierungsfreigaben auf demselben Server hostet, muss daher sichergestellt werden, dass einzelne Benutzer nur für eine dieser Freigaben zugriffsberechtigt sind. Andernfalls kann der Client eine Verbindung mit der falschen Freigabe herstellen, wenn er auf den Server zugreift. Zu diesem Zweck kann eine separate Sicherheitsgruppe für jede Synchronisierungsfreigabe erstellt werden.  
  
Zudem wird der Zugriff auf den Ordner eines Benutzers innerhalb einer Synchronisierungsfreigabe durch Besitzrechte für den Ordner bestimmt. Beim Erstellen einer Synchronisierungsfreigabe gewähren Arbeitsordner Benutzern standardmäßig exklusiven Zugriff auf ihre Dateien (die Vererbung wird deaktiviert, und Benutzer werden als Besitzer ihrer Ordner festgelegt).  
  
## <a name="design-checklist"></a>Prüfliste für den Entwurf  

Die folgenden Fragen zum Entwurf sollen Kunden dabei helfen, die am besten geeignete Arbeitsordnerimplementierung für ihre Umgebung zu entwerfen. Diese Prüfliste sollte vor der Bereitstellung von Servern vom Kunden durchgearbeitet werden.  
  
-   Zielgruppe  
  
    -   Von welchen Benutzern werden Arbeitsordner verwendet?  
  
    -   Wie sind Benutzer organisiert? (Geografisch, nach Büro, Abteilung usw.)  
  
    -   Gibt es Benutzer, für die besondere Anforderungen an die Datenspeicherung, -sicherheit oder -aufbewahrung gelten?  
  
    -   Gibt es Benutzer, für die bestimmte Anforderungen an die Geräterichtlinien (z.B. Verschlüsselung) gelten?  
  
    -   Welche Clientcomputer und Geräte müssen Sie unterstützen? (Windows8.1, Windows RT8.1, Windows7)  
  
         Wenn Sie Computer mit Windows7 unterstützen und Kennwortrichtlinien verwenden möchten, schließen Sie die Domäne, die ihre Computerkonten speichert, aus der Kennwortrichtlinie für Arbeitsordner aus, und verwenden Sie stattdessen die Kennwortrichtlinien für Gruppenrichtlinien für in eine Domäne eingebundene Computer in dieser Domäne.  
  
    -   Ist Interoperabilität mit anderen Benutzerdaten-Verwaltungslösungen oder eine Migration von solchen Lösungen erforderlich (z.B. Ordnerumleitung)?  
  
    -   Müssen Benutzer aus mehreren Domänen über das Internet Daten mit einem einzigen Server synchronisieren?  
  
    -   Müssen Benutzer unterstützt werden, die nicht Mitglieder der lokalen Administratorgruppe auf ihren mit einer Domäne verbundenen Computern sind? (Wenn dies der Fall ist, müssen die entsprechenden Domänen aus den Geräterichtlinien für Arbeitsordner ausgeschlossen werden, z.B. Verschlüsselungs- und Kennwortrichtlinien.)  
  
-   Infrastruktur- und Kapazitätsplanung  
  
    -   An welchen Standorten im Netzwerk sollen sich Synchronisierungsserver befinden?  
  
    -   Werden Synchronisierungsserver von einem Infrastructure-as-a-Service (IaaS)-Anbieter gehostet, z.B. in einer Azure-VM?  
  
    -   Sind dedizierte Server für bestimmte Benutzergruppen erforderlich, und wenn ja, wie viele Benutzer müssen von jedem dedizierten Server unterstützt werden?  
  
    -   Wo befinden sich die Internetzugangs-/-ausgangspunkte im Netzwerk?  
  
    -   Werden Synchronisierungsserver gruppiert, um Fehlertoleranz bereitzustellen?  
  
    -   Sind auf Synchronisierungsservern mehrere Datenvolumes zum Hosten von Benutzerdaten erforderlich?  
  
-   Datensicherheit  
  
    -   Müssen auf Synchronisierungsservern mehrere Synchronisierungsfreigaben erstellt werden?  
  
    -   Welche Gruppen werden verwendet, um den Zugriff auf Synchronisierungsfreigaben bereitzustellen?  
  
    -   Bei der Verwendung mehrerer Synchronisierungsserver: Welche Sicherheitsgruppe wird für die delegierte Fähigkeit zum Ändern der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten erstellt?  
  
    -   Gelten besondere Sicherheits- oder Überwachungsanforderungen für einzelne Synchronisierungsfreigaben?  
  
    -   Ist Multi-Factor Authentication (MFA) erforderlich?  
  
    -   Müssen Sie in der Lagen sein, Daten in Arbeitsordnern remote auf Computern und Geräten zurückzusetzen?  
  
-   Gerätezugriff  
  
    -   Welche URL wird verwendet, um internetbasierten Geräten den Zugriff zu ermöglichen (*die für die E-Mail-basierte automatische Serverermittlung erforderliche Standard-URL ist "workfolders.domänenname"*)?  
  
    -   Wie wird die URL im Internet veröffentlicht?  
  
    -   Wird die automatische Serverermittlung verwendet?  
  
    -   Werden Gruppenrichtlinien verwendet, um in Domänen eingebundene Computer zu konfigurieren?  
  
    -   Wird WindowsIntune zum Konfigurieren externer Geräte verwendet?  
  
    -   Ist eine Geräteregistrierung erforderlich, damit Geräte eine Verbindung herstellen können?  
  
## <a name="next-steps"></a>Nächste Schritte  
 Der nächste Schritt nach dem Entwerfen der Arbeitsordnerimplementierung ist die Bereitstellung von Arbeitsordnern. Weitere Informationen finden Sie unter [Bereitstellen von Arbeitsordnern](deploy-work-folders.md).  
  
## <a name="see-also"></a>Weitere Informationen:  
 Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:  
  
|Inhaltstyp|Verweise|  
|------------------|----------------|  
|**Produktbewertung**|-   [Arbeitsordner](work-folders-overview.md)<br />-   [Arbeitsordner für Windows7](http://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) (Blogbeitrag)|  
|**Bereitstellung**|-   [Entwerfen einer Arbeitsordnerimplementierung](plan-work-folders.md)<br />-   [Bereitstellen von Arbeitsordnern](deploy-work-folders.md)<br />-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy (WAP)](deploy-work-folders-adfs-overview.md)<br />- [Bereitstellen von Arbeitsordnern mit Azure AD-Anwendungsproxy](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)<br />-   [Überlegungen zur Leistung von Arbeitsordnerbereitstellungen](http://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />-   [Arbeitsordner für Windows7 (64-Bit-Download)](http://www.microsoft.com/download/details.aspx?id=42558)<br />-   [Arbeitsordner für Windows7 (32-Bit-Download)](http://www.microsoft.com/download/details.aspx?id=42559)<br />-   [Bereitstellung von Arbeitsordnern in einer Testumgebung](http://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) (Blogbeitrag)|
