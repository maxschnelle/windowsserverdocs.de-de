---
ms.assetid: b3d6fb87-c4d4-451c-b3de-a53d2402d295
title: Installieren einer neuen Windows Server 2012 Active Directory-Gesamtstruktur (Stufe 200)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b8a7502a1b9d27b0f61353f2544182a64d311496
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-new-windows-server-2012-active-directory-forest-level-200"></a>Installieren einer neuen Windows Server 2012 Active Directory-Gesamtstruktur (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird erläutert, das neue Windows Server 2012 Active Directory Domain Services Domain Controller Promotion Feature eine einführende Ebene. In Windows Server 2012 AD DS ersetzt das Dcpromo-Tool mit Server-Manager und Windows PowerShell-basierte Bereitstellung.  
  
-   [Active Directory Domain Services, um die Verwaltung](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SimplifiedAdmin)  
  
-   [Technische Übersicht](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_TechOverview)  
  
-   [Bereitstellen einer Gesamtstruktur mit Server-Manager](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Bereitstellen einer Gesamtstruktur mit WindowsPowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_PSForest)  
  
## <a name="BKMK_SimplifiedAdmin"></a>Active Directory Domain Services, um die Verwaltung  
Windows Server2012 führt die nächste Generation von Active Directory Domain Services Vereinfachte Administration und ist die am häufigsten radikal Domäne erneut Zielsetzung seit Windows2000 Server. Die vereinfachte AD DS-Administration Erfahrungen zwölf Jahren Active Directory und stellt ein flexibleres, flexibler und intuitiver Verwaltungsoberfläche Architekten und Administratoren. Das bedeutete, erstellen neue Versionen der vorhandenen Technologien als auch die Funktionen einiger Komponenten in Windows Server2008 R2 erweitern.  
  
### <a name="what-is-ad-ds-simplified-administration"></a>Was ist, dass AD DS vereinfachte Verwaltung?  
Die vereinfachte AD DS-Administration ist ein neuartiger Weg der Domänen-Bereitstellung. Zu diesen Features gehören:  
  
-   AD DS-rollenbereitstellung ist nun Teil der neuen Server-Manager-Architektur und erlaubt die remote-Installation.  
  
-   Die AD DS-bereitstellungs- und Konfigurationsmodul dient nun Windows PowerShell, auch wenn die Verwendung einer grafischen Benutzeroberfläche.  
  
-   Zur heraufstufung gehört nun voraussetzungsprüfung, die Bereitschaft von Gesamtstruktur und Domäne für den neuen Domänencontroller, die fehlgeschlagene Aktionen geprüft werden.  
  
-   Die Windows Server 2012-Gesamtstrukturfunktionsebene Ebene enthält keine neuen Features und Domänenfunktionsebene ist nur für eine Teilmenge der neuen Kerberos-Features sind daher weniger häufig Administratoren erforderlich, müssen eine homogene Domänencontroller-Umgebungen.  
  
### <a name="purpose-and-benefits"></a>Zweck und Vorteile  
Dieser Änderungen erscheinen, komplexere, anstatt einfacher. Den AD DS-Bereitstellungsprozess jedoch Neugestaltung, gab es Möglichkeit, zahlreiche Schritte und bewährte Methoden in wenige und zusammengefügt. Dies bedeutet beispielsweise, dass die grafische Konfiguration eines neuen Replikat-Domänencontrollers nun acht Dialogfelder anstatt zwölf ist. Zum Erstellen einer neuen Active Directory-Gesamtstruktur muss ein *einzelne* Windows PowerShell-Befehl mit nur *eine* Argument: den Namen der Domäne.  
  
Warum ist es starke Gewichtung von Windows PowerShell in Windows Server 2012? Verteilte Datenverarbeitung entwickelt, ermöglicht Windows PowerShell ein einziges Modul für Konfiguration und Wartung in Form von grafischen Oberflächen und Befehlszeilenschnittstellen. Sie ermöglicht es, Skripts mit vollem Funktionsumfang für beliebige Komponenten mit demselben erstklassigen Staatsangehörigkeit für IT-Experten, die eine API für Entwickler gewährt. Als Cloud-basierten von computing cloudbasiertem, bietet Windows PowerShell auch endlich die Möglichkeit, einen Server remote verwalten, in dem ein Computer ohne grafische Oberfläche dieselben Verwaltungsoptionen wie solche mit Monitor und Maus verfügt.  
  
Erfahrene AD DS-Administrator sollten ihre bisherigen Kenntnisse hoher Relevanz gefunden werden. Einen Einstieg in die Verwaltung findet eine wesentlich flachere Lernkurve.  
  
## <a name="BKMK_TechOverview"></a>Technische Übersicht  
  
### <a name="what-you-should-know-before-you-begin"></a>Was sollten Sie wissen, bevor Sie beginnen  
In diesem Thema wird davon ausgegangen Vertrautheit mit früheren Versionen von Active Directory Domain Services, und keine grundsatzinformationen zu deren Zweck und Funktionen. Weitere Informationen zu AD DS finden Sie in der TechNet-Portalseiten unter:  
  
-   [Active Directory-Domänendienste für Windows Server 2008 R2](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
  
-   [Active Directory-Domänendienste für WindowsServer 2008](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
  
-   [Technische Referenz zu Windows Server](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
  
### <a name="functional-descriptions"></a>Funktionale Beschreibungen  
  
#### <a name="ad-ds-role-installation"></a>AD DS-Rolleninstallation  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_SelectServerRoles.gif)  
  
Installieren von Active Directory-Domänendienste verwendet Server-Manager und Windows PowerShell, wie alle anderen Serverrollen und Features in Windows Server 2012. Das Dcpromo.exe-Programm bietet keine GUI-Konfigurationsoptionen.  
  
Sie verwenden einen grafischen Assistenten im Server-Manager oder das ServerManager-Modul für Windows PowerShell in lokalen und remote-Installationen. Indem Sie mehrere Instanzen dieser Assistenten bzw. Cmdlets und unterschiedliche Zielserver, können Sie AD DS auf mehreren Domänencontrollern gleichzeitig von einer einzelnen Konsole aus bereitstellen. Obwohl diese neuen Features nicht abwärtskompatibel mit Windows Server 2008 R2 oder älteren Betriebssystemen sind, können Sie auch weiterhin die Anwendung Dism.exe in Windows Server 2008 R2 eingeführt wurde, zur lokalen Rolleninstallation in der klassischen Befehlszeile.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSAddWindowsFeature.png)  
  
#### <a name="ad-ds-role-configuration"></a>AD DS-Rollenkonfiguration  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
Active Directory-Domänendienste-Konfiguration "früher bekannt als DCPROMO" wird nun eine diskrete Operation von der Rolleninstallation. Nach der Installation von AD DS-Rolle konfiguriert ein Administrator den Server als Domänencontroller mithilfe eines separaten Assistenten im Server-Manager oder mithilfe des ADDSDeployment Windows PowerShell-Moduls.  
  
AD DS-Rollenkonfiguration basiert auf zwölf Jahren Erfahrung und konfiguriert Domänencontroller anhand der aktuellen best Practices von Microsoft. Domain Name System und globale Kataloge werden z. B. standardmäßig auf jedem Domänencontroller installiert.  
  
Der Server-Manager AD DS-Konfigurations-Assistenten vereint zahlreiche einzelne Dialoge in einfachere aufforderungen und versteckt keine Einstellungen im "erweiterten" Modus mehr. Der gesamte Heraufstufungsprozess erfolgt in einem erweiterten Dialogfeld während der Installation. Der Assistent und ADDSDeployment Windows PowerShell-Modul zeigen Sie wesentliche Änderungen und Sicherheitsbedenken mit Links zu weiteren Informationen.  
  
Dcpromo.exe in Windows Server 2012 nur Befehlszeile für das unbeaufsichtigte Installationen bleibt, und die grafischen Installations-Assistenten nicht mehr ausgeführt. Es wird dringend empfohlen, beenden Sie die Verwendung von Dcpromo.exe für unbeaufsichtigte Installationen und ihn durch das ADDSDeployment-Modul ersetzen, wie die nun veraltete ausführbare Datei nicht in der nächsten Version von Windows eingeschlossen wird.  
  
Diese neuen Features sind nicht abwärtskompatibel mit Windows Server 2008 R2 oder älteren Betriebssystemen.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSForest.png)  
  
> [!IMPORTANT]  
> Dcpromo.exe nicht mehr enthält einen grafischen Assistenten und installiert keine Binärdateien für Rollen oder Features. Es wird versucht, zum Ausführen von Dcpromo.exe aus der Explorer-Shell zurückgegeben:  
>   
> "Mit dem Assistenten zum Installieren von Active Directory-Domäne ist im Server-Manager verschoben. Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=220921."  
>   
> Versuch der Ausführung von Dcpromo.exe / unattend weiterhin installiert die Binärdateien in vorherigen Betriebssystemen, jedoch gibt eine Warnung aus:  
>   
> "Die Dcpromo unbeaufsichtigte Vorgang durch das ADDSDeployment-Modul für Windows PowerShell ersetzt wird. Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=220924."  
>   
> Windows Server 2012 veraltet dcpromo.exe und werden in zukünftigen Versionen von Windows enthalten, auch nicht Weitere Verbesserungen in diesem Betriebssystem. Administratoren sollten dessen Verwendung einstellen und wechseln Sie zu den unterstützten Windows PowerShell-Module, wenn sie Domänencontroller per Befehlszeile erstellen möchten.  
  
#### <a name="prerequisite-checking"></a>Voraussetzungsüberprüfung  
Domänencontroller-Konfiguration implementiert auch eine voraussetzungsprüfungs-Phase, die der Gesamtstruktur und Domäne vor der heraufstufung des Domänencontrollers ausgewertet wird. Dazu gehören die Verfügbarkeit der FSMO-Rolle, Benutzerrechte, erweiterte Schemakompatibilität und sonstige Anforderungen. Dieses neue Design verhindert Probleme, in dem Heraufstufen eines Domänencontrollers beginnt und dann in der Mitte mit einem schwerwiegenden Konfigurationsfehler. Dies verringert die Gefahr verwaister Domänencontroller-Metadaten in der Gesamtstruktur oder ein Server, der fälschlicherweise davon wird einem Domänencontroller.  
  
## <a name="BKMK_SMForest"></a>Bereitstellen einer Gesamtstruktur mit Server-Manager  
In diesem Abschnitt wird erläutert, wie den ersten Domänencontroller in einer Gesamtstruktur-Stammdomäne mithilfe von Server-Manager auf einem grafischen Windows Server 2012-Computer installiert wird.  
  
### <a name="server-manager-ad-ds-role-installation-process"></a>Server-Manager AD DS-Rolleninstallation via  
Das folgende Diagramm zeigt die Active Directory Domain Services-Rolleninstallation via, Sie die Ausführung von ServerManager.exe und die End-bis zur heraufstufung des Domänencontrollers ab.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment.png)  
  
#### <a name="server-pool-and-add-roles"></a>Server Serverpool und Hinzufügen von Rollen  
Alle Windows Server 2012-Computer auf dem Computer mit Server-Manager sind für pooling geeignet. Wenn in einem Pool zusammengefasste, wählen Sie diese Server für die Remoteinstallation von AD DS oder eine andere Konfigurationsoption in Server-Manager möglich.  
  
Wählen Sie zum Hinzufügen von Servern eine der folgenden aus:  
  
-   Klicken Sie auf **hinzufügen Weitere zu verwaltende Server** auf dem Dashboard-begrüßungskachel  
  
-   Klicken Sie auf die **verwalten** Menü und wählen Sie **Hinzufügen von Servern**  
  
-   Mit der rechten Maustaste **alle Server** , und wählen Sie **Hinzufügen von Servern**  
  
Dadurch wird das Dialogfeld Server hinzufügen:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddServers.png)  
  
Dadurch haben Sie drei Möglichkeiten, um den Pool für die Verwendung oder Gruppierung hinzuzufügen:  
  
-   Active Directory-Suche (verwendet LDAP, erfordert, dass der Computer einer Domäne angehören, ermöglicht das Filtern von Betriebssystem und unterstützt Platzhalter)  
  
-   DNS-Suche (verwendet DNS-Alias oder IP-Addresse via ARP- oder NetBIOS-Übertragung oder die WINS-Suche, lässt nicht zu Betriebssystem betriebsystemfilterung zu und unterstützt Platzhalter)  
  
-   Importieren (verwendet eine Textdateiliste von Servern, die durch Wagenrücklauf/Zeilenvorschub getrennt)  
  
Klicken Sie auf **Jetzt suchen** eine Liste der Server aus der gleichen Active Directory-Domäne, der der Computer angehört, klicken Sie auf einen oder mehrere Servernamen aus der Liste der Server. Klicken Sie auf den Pfeil nach rechts, um die zum Hinzufügen von Servern die **ausgewählte** Liste. Verwenden der **Hinzufügen von Servern** Dialogfeld dashboardrollengruppen ausgewählte Server hinzu. Oder klicken Sie auf **verwalten**, und klicken Sie dann auf **Servergruppe erstellen**, oder klicken Sie auf **Servergruppe erstellen** auf dem Dashboard **Willkommen bei Server-Manager** Kachel, um benutzerdefinierte Servergruppen zu erstellen.  
  
> [!NOTE]  
> Das Hinzufügen von Servern Verfahren überprüft nicht, dass ein Server online oder zugänglich ist. Kennzeichnen jedoch nicht erreichbare Server in der Sicht Verwaltbarkeit im Server-Manager bei der nächsten Aktualisierung  
  
Installieren von Rollen können Sie per Remotezugriff auf alle Windows Server 2012 Computer zum Pool hinzugefügten wie gezeigt:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/tADDS_SMI_TR_AddRolesFeatures.png)  
  
Sie können keine Server unter Betriebssystemen älter als Windows Server 2012 vollständig verwalten. Die **Hinzufügen von Rollen und Features** Auswahl läuft ServerManager Windows PowerShell-Modul **Install-WindowsFeature**.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddADDSToAnotherServer.png)  
  
Sie können auch im Server-Manager-Dashboard auf einem vorhandenen Domänencontroller Remoteserver AD DS-Installation mit der Rolle, die bereits von der rechten Maustaste auf die AD DS-Dashboard-Kachel und auswählen vorausgewählt wählen **Hinzufügen der AD DS zu einem anderen Server**. Dies ist Aufrufen **Install-WindowsFeature AD-Domain-Services**.  
  
Der Computer, auf den Sie Server-Manager ausführen pools selbst automatisch. Um die AD DS-Rolle zu installieren, klicken Sie einfach auf die **verwalten** und dann auf **Hinzufügen von Rollen und Features**.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ManageAddRoles.png)  
  
#### <a name="installation-type"></a>Installationstyp  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectInstallationType.png)  
  
Die **Installationstyp** Dialogfeld bietet die Möglichkeit, die Active Directory-Domänendienste nicht unterstützt: die **Remote Desktop Services szenariobasierte Installation**. Diese Option erlaubt nur Remotedesktopdienste in einer serverübergreifenden verteilten arbeitsauslastung. Wenn Sie es aktivieren, können keine AD DS installieren.  
  
Lassen Sie die Standardauswahl immer vorhanden, bei der Installation von AD DS: **rollenbasierte oder featurebasierte Installation**.  
  
#### <a name="server-selection"></a>-Serverauswahl  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectDestinationServer.png)  
  
Die **Serverauswahl** Dialogfeld ermöglicht es Ihnen, wählen aus einem der zuvor zum Pool hinzugefügt Server als darauf zugegriffen werden kann. Der lokale Server mit Server-Manager ist automatisch verfügbar.  
  
Darüber hinaus können Sie offline Hyper-V-VHD-Dateien mit dem Windows Server 2012-Betriebssystem auswählen und Server-Manager fügt die Rolle Sie via Komponentendienste direkt hinzu. Dadurch können Sie virtuelle Server mit den benötigten Komponenten bereitstellen, bevor Sie diese weiter konfigurieren.  
  
#### <a name="server-roles-and-features"></a>Serverrollen und Features  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectServerRoles.png)  
  
Wählen Sie die **Active Directory Domain Services** Rolle, wenn Sie einen Domänencontroller heraufstufen möchten. Alle Features zur Verwaltung von Active Directory und erforderliche Dienste werden automatisch installiert, auch wenn sie offensichtliche Teil einer anderen Rolle sind oder werden nicht in der Benutzeroberfläche des Server-Manager ausgewählte angezeigt.  
  
Server-Manager wird auch ein Dialogfeld mit Informationen, die zeigt, welche Verwaltungsfunktionen dieser Rolle implizit installiert wird. Dies entspricht der **- IncludeManagementTools** Argument.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddFeaturesDialog.gif)  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectFeatures.png)  
  
Zusätzliche **Features** hier hinzugefügt werden können wie gewünscht.  
  
#### <a name="active-directory-domain-services"></a>Active Directory-Domänendienste  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSIntro.png)  
  
Die **Active Directory Domain Services** Dialogfeld enthält eingeschränkte Informationen zu Anforderungen und best Practices. Es dient hauptsächlich als Bestätigung dafür, dass Sie die AD DS-Rolle auswählen ", wenn dieser Bildschirm nicht angezeigt wird, haben Sie keine AD DS ausgewählt.  
  
#### <a name="confirmation"></a>Bestätigung  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Confirmation.png)  
  
Die **Bestätigung** Dialogfeld ist der letzte Prüfpunkt vor Beginn der Installation. Es bietet eine Option, um den Computer neu starten, bei Bedarf nach der Rolleninstallation, aber AD DS-Installation ist kein Neustart erforderlich.  
  
Durch Klicken auf **installieren**, zu bestätigen, dass die Installation zu beginnen. Sie können nicht die Rolleninstallation unterbrochen.  
  
#### <a name="results"></a>Ergebnisse  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Results.png)  
  
Die **Ergebnisse** Dialogfeld zeigt den aktuellen Installationsfortschritt und Installationsstatus an. Unabhängig davon, ob der Server-Manager geschlossen wird, wird die Installation fortgesetzt.  
  
Überprüfen der Installationsergebnisse wird weiterhin empfohlen. Wenn Sie schließen das **Ergebnisse** Dialogfeld, bevor die Installation abgeschlossen ist, Sie können die Ergebnisse mit dem Server-Manager-Benachrichtigungskennzeichen prüfen. Server-Manager zeigt außerdem eine Warnmeldung für alle Server, auf denen die AD DS-Rolle installiert, aber nicht weiter als Domänencontroller konfiguriert wurde.  
  
**Aufgabe Benachrichtigungen**  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskNotofications.png)  
  
**AD DS-Details**  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSDetails.png)  
  
**Aufgabendetails**  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskDetails.png)  
  
#### <a name="promote-to-domain-controller"></a>Heraufstufen als Domänencontroller  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Promote.png)  
  
Am Ende der Installation der AD DS-Rolle können Sie mit der Konfiguration fortfahren, mithilfe der **Server zu einem Domänencontroller heraufstufen** Link. Dies ist erforderlich, damit dem Server einen Domänencontroller, aber es ist nicht erforderlich, um den Konfigurations-Assistenten sofort auszuführen. Sie möchten z. B. nur Server mit AD DS-Binärdateien vor dem Senden an andere Filialen zur späteren Konfiguration bereitstellen. Hinzufügen der AD DS-Rolle vor dem Versand, sparen Sie Zeit, wenn sie ihr Ziel erreichen. Außerdem führen Sie die bewährte Methode nicht über einen Domänencontroller offline Tage oder Wochen. Schließlich können Sie auf diese Komponenten vor der heraufstufung des Domänencontrollers, speichern Sie mindestens einen Neustart zu aktualisieren.  
  
Wenn Sie diesen Link später die ADDSDeployment-Cmdlets aufgerufen: **Install-Addsforest**, **Install-Addsdomain**, oder **Install-Addsdomaincontroller**.  
  
### <a name="uninstallingdisabling"></a>Deinstallieren und Deaktivieren von  
Sie entfernen die AD DS-Rolle wie jede andere Rolle, unabhängig davon, ob Sie den Server zu einem Domänencontroller heraufgestuft. Entfernen der AD DS-Rolle werden jedoch einen Neustart erforderlich.  
  
Entfernen der Active Directory-Domänendienste-Rolle unterscheidet sich von Installation, dass es Herabstufung eines Domänencontrollers ist erforderlich, bevor er abgeschlossen werden kann. Dies ist erforderlich, um einen Domänencontroller zu verhindern, dass die Rollen-Binärdateien deinstalliert werden, ohne die richtigen Metadatencleanup in der Gesamtstruktur. Weitere Informationen finden Sie unter [Herabstufen von Domänencontrollern und Domänen & #40; Level 200 & #41; ](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
> [!WARNING]  
> Entfernen die AD DS-Rollen mit Dism.exe oder dem Windows PowerShell DISM-Modul nach der heraufstufung zu einem Domänencontroller wird nicht unterstützt und wird verhindert, dass den Server normal starten.  
>   
> Im Gegensatz zu Server-Manager oder das AD DS-Bereitstellung-Modul für Windows PowerShell ist DISM einen systemeigenen Dienst, der keine Kenntnisse von AD DS und deren Konfiguration hat. Verwenden Sie Dism.exe oder dem Windows PowerShell DISM-Modul nicht auf um die AD DS-Rolle zu deinstallieren, es sei denn, der Server nicht mehr als ein Domänencontroller ist.  
  
### <a name="create-an-ad-ds-forest-root-domain-with-server-manager"></a>Erstellen einer AD DS-Gesamtstruktur-Stammdomäne in Server-Manager  
Das folgende Diagramm zeigt den Konfigurationsprozess des Active Directory Domain Services, in dem Fall, in dem Sie zuvor die AD DS-Rolle installiert und gestartet, der **Active Directory Domain Services Konfigurations-Assistenten** mit Server-Manager.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_forestdeploy2.png)  
  
#### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddNewForest.png)  
  
Server-Manager beginnt jede heraufstufung des Domänencontrollers mit dem **Bereitstellungskonfiguration** Seite. Ändern die restlichen Optionen und erforderlichen Feldern auf dieser Seite und den darauf folgenden Seiten, je nachdem, welcher, die Bereitstellungsvorgang Sie wählen.  
  
Klicken Sie zum Erstellen einer neuen Active Directory-Gesamtstruktur auf **Hinzufügen einer neuen Gesamtstruktur**. Sie müssen einen gültiges Stammzertifizierungsstellen-Domänennamen angeben. der Name darf nicht einzelnen Bezeichnung bestehen (z. B. der Name muss sein *"contoso.com"* oder ähnliche und nicht nur *Contoso*) und müssen zulässige DNS-Anforderungen für Domänennamen erfüllen.  
  
Weitere Informationen zu gültigen Domänennamen finden Sie im KB-Artikel [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](https://support.microsoft.com/kb/909264).  
  
> [!WARNING]  
> Erstellen Sie keine neue Active Directory-Gesamtstrukturen mit dem gleichen Namen wie ein externer DNS-Name. Wenn Ihre Internet-DNS-URL http://contoso.com ist, müssen Sie einen anderen Namen für Ihre interne Gesamtstruktur um künftige Kompatibilitätsprobleme zu vermeiden auswählen. Der Name sollte eindeutig und für den Webdatenverkehr unwahrscheinlich sein. Beispiel: corp.contoso.com.  
  
Eine neue Gesamtstruktur benötigt keine neue Anmeldeinformationen für die Domänen Administratorkonto. Der Domänencontroller-Heraufstufungsprozess verwendet die Anmeldeinformationen des integrierten Administratorkontos aus den ersten Domänencontroller verwendet, um den Stamm der Gesamtstruktur zu erstellen. Es gibt keine Möglichkeit (standardmäßig) deaktivieren oder Sperren Sie das integrierte Administratorkonto und möglicherweise der einzige Einstiegspunkt in einer Gesamtstruktur, wenn die andere Domäne unbrauchbar sind. Es ist wichtig, das Kennwort kennen, bevor Sie eine neue Gesamtstruktur bereitstellen.  
  
**DomainName** erfordert einen gültigen vollqualifizierten DNS-Namen und ist erforderlich.  
  
#### <a name="domain-controller-options"></a>Domänencontroller-Optionen  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DCOptions_Forest.gif)  
  
Die **Domänencontrolleroptionen** können Sie konfigurieren die **Gesamtstruktur-Funktionsebene** und **Domänenfunktionsebene** für die neue Gesamtstruktur-Stammdomäne. Standardmäßig sind diese Einstellungen für Windows Server 2012 in einer neuen Gesamtstruktur-Stammdomäne. Die Gesamtstrukturfunktionsebene Windows Server 2012 bietet keine neuen Funktionen gegenüber der Windows Server 2008 R2-Gesamtstrukturfunktionsebene. Die Domänenfunktionsebene Windows Server 2012 wird nur benötigt, um die neuen Kerberos-Einstellungen zu implementieren "immer Ansprüche bereitstellen" und "Fehler bei authentifizierungsanforderungen ohne Armor". Eine primäre Funktionsebenen in Windows Server 2012 wird die Teilnahme an der Domäne auf Domänencontroller zu beschränken, die Betriebssysteme Mindestanforderungen erfüllen. Anders ausgedrückt, können Sie angeben, dass Windows Server 2012-Domäne Gesamtstrukturfunktionsebene nur von Domänencontrollern, auf denen Windows Server 2012 ausgeführt, die Domäne hosten können.  Windows Server 2012 implementiert eine neue Domänencontroller-Kennzeichnung aufgerufen **DS_WIN8_REQUIRED** in der **DSGetDcName** -Funktion von NetLogon, die ausschließlich Windows Server 2012-Domänencontroller nach. Dadurch können Sie die Flexibilität, eine homogenere oder heterogenere Gesamtstrukturen, die hinsichtlich der erlaubten Betriebssysteme auf Domänencontrollern ausgeführt werden.  
  
Weitere Informationen zur Domänencontrollersuche finden Sie [Directory Service Functions](https://msdn.microsoft.com/library/ms675900(VS.85).aspx).  
  
Die einzige konfigurierbare Domänencontroller-Funktion ist die Option der DNS-Server. Microsoft empfiehlt, dass alle Domänencontroller DNS-Dienste für hohe Verfügbarkeit in verteilten Umgebungen bereitstellen, weshalb diese Option bei der Installation von eines Domänencontrollers in allen Modi und Domänen standardmäßig ausgewählt ist. Den globalen Katalog und schreibgeschützte nur Domänencontroller-Optionen sind nicht verfügbar, beim Erstellen einer neuen Gesamtstruktur-Stammdomäne. der erste Domänencontroller muss ein GC sein und nicht möglich, eine schreibgeschützte nur Domänencontroller (RODC).  
  
Das angegebene **Directory Services Kennwort für den Wiederherstellungsmodus** müssen eingehalten werden die Kennwortrichtlinie auf den Server, die in der Standardeinstellung kein sicheres Kennwort; erforderlich ist nur ein nicht leeres eins. Wählen Sie immer ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase.  
  
#### <a name="dns-options-and-dns-delegation-credentials"></a>DNS-Optionen und Anmeldeinformationen für DNS-Delegierung  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestDNSOptions.png)  
  
Die **DNS-Optionen** Seite können Sie die DNS-Delegierung konfigurieren und alternative DNS-Administratoranmeldeinformationen angeben.  
  
Sie können DNS-Optionen oder konfigurieren Delegierung der Active Directory-Domäne Konfigurations-Assistenten bei der Installation einer neuen Active Directory Gesamtstruktur-Stammdomäne, Sie ausgewählt haben, in denen, die **DNS-Server** auf die **Domänencontrolleroptionen** Seite. Die **DNS-Delegierung erstellen** Option ist verfügbar, wenn eine neue Gesamtstruktur Stamm-DNS-Zone in eine vorhandene DNS-Server-Infrastruktur zu erstellen. Diese Option können Sie alternative DNS-Administratoranmeldeinformationen bereitstellen, die die Rechte zum Aktualisieren von DNS-Zone haben.  
  
Weitere Informationen dazu, ob Sie eine DNS-Delegierung erstellen müssen, finden Sie unter [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
#### <a name="additional-options"></a>Weitere Optionen  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestAdditionalOptions.png)  
  
Die **zusätzliche Optionen** Seite zeigt den NetBIOS-Namen der Domäne, und ermöglicht es Ihnen zu überschreiben. Standardmäßig entspricht der NetBIOS-Domänenname die Bezeichnung ganz links des vollqualifizierten Domänennamens zur Verfügung gestellt, auf die **Bereitstellungskonfiguration** Seite. Wenn Sie den vollständig qualifizierten Domänennamen "corp.contoso.com" angegeben, ist der Standard-NetBIOS-Domänenname z. B. CORP.  
  
Wenn der Name mehr als 15 Zeichen oder weniger beträgt nicht in Konflikt mit einem anderen NetBIOS-Namen, wird er nicht verändert. Wenn es mit einem anderen NetBIOS-Namen in Konflikt steht, wird eine Zahl an den Namen angefügt. Wenn der Name mehr als 15 Zeichen ist, bietet der Assistent einen eindeutigen, abgeschnittenen Vorschlag. In beiden Fällen prüft der Assistent zuerst der Namen nicht bereits mit einer WINS-Suche und NetBIOS-broadcast.  
  
Weitere Informationen zu gültigen Domänennamen finden Sie im KB-Artikel [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](https://support.microsoft.com/kb/909264).  
  
#### <a name="paths"></a>Pfade  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPaths.png)  
  
Die **Pfade** Seite können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle außer Kraft setzen und der SYSVOL-Freigabe. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von %systemroot% (z. B. C:\Windows).  
  
#### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestReviewOptions.png)  
  
Die **Optionen prüfen** Seite können Sie Ihre Einstellungen überprüfen und stellen Sie sicher, dass Ihre Anforderungen erfüllt, bevor Sie die Installation zu starten. Dies ist nicht die letzte Gelegenheit, um die Installation beendet, wenn Sie Server-Manager verwenden. Dies ist lediglich eine Option zum Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetzen  
  
Die **Optionen prüfen** im Server-Manager bietet auch einen optionalen **Skript anzeigen**, um eine Unicode-Textdatei zu erstellen, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dadurch können Sie die Benutzeroberfläche des Server-Manager als Studio ein Windows PowerShell-Bereitstellung verwenden. Verwenden Sie die Dienste Konfigurations-Assistenten von Active Directory-Domäne, um Optionen konfigurieren, exportieren Sie die Konfiguration und den Assistenten abbrechen. Dieser Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
```powershell 
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSForest `  
-CreateDNSDelegation `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainMode "Win2012" `  
-DomainName "corp.contoso.com" `  
-DomainNetBIOSName "CORP" `  
-ForestMode "Win2012" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-NoRebootOnCompletion:$false `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> Server-Manager füllt normalerweise alle Argumente mit Werten, die beim Heraufstufen und nicht auf Standardwerte basiert (wie zwischen zukünftige Versionen von Windows oder Servicepacks geändert werden können). Die einzige Ausnahme hierbei ist die **- Safemodeadministratorpassword** -Argument (das Skript bewusst ausgelassen wird). Um eine bestätigungsaufforderung zu erzwingen, lassen Sie bei der interaktiven Ausführung des Cmdlets.  
  
#### <a name="prerequisites-check"></a>Prüfung der erforderlichen Komponenten  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration unterstützen einer neuen AD DS-Gesamtstruktur ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Server-Manager Active Directory Konfigurations-Assistent Domänendienste eine Reihe modularer Tests. Diese Tests, die Sie mit vorgeschlagenen Reparaturoptionen benachrichtigt. Sie können die Tests ausführen, so oft wie erforderlich. Prozess für den Domänencontroller kann nicht fortgesetzt, bis alle voraussetzungstests positiv übergeben.  
  
Die **Voraussetzungsüberprüfung** auch Flächen relevante Informationen wie z. B., die ältere Betriebssysteme betreffen.  
  
Weitere Informationen zu den voraussetzungsprüfungen finden Sie unter [Prerequisite Checking](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
#### <a name="installation"></a>Installation  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestInstallation.png)  
  
Wenn die **Installation** Seite wird angezeigt, die Konfiguration des Domänencontrollers beginnt und kann nicht angehalten oder abgebrochen. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in die Protokolle geschrieben werden:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
> [!NOTE]  
> Sie können mehrere rolleninstallationen und AD DS-Konfigurations-Assistenten über die gleichen Server-Manager-Konsole gleichzeitig ausführen.  
  
#### <a name="results"></a>Ergebnisse  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
Die **Ergebnisse** Seite zeigt den Erfolg oder Misserfolg der heraufstufung sowie alle wichtigen Administrationsinformationen. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  
## <a name="BKMK_PSForest"></a>Bereitstellen einer Gesamtstruktur mit WindowsPowerShell  
In diesem Abschnitt wird erläutert, wie des ersten Domänencontrollers in einer Gesamtstruktur-Stammdomäne mithilfe von Windows PowerShell auf einem zentralen Windows Server 2012-Computer installiert wird.  
  
### <a name="windows-powershell-ad-ds-role-installation-process"></a>Windows PowerShell AD DS-Rolleninstallation via  
Durch die Implementierung einige unkomplizierte ServerManager bereitstellungs-Cmdlets in Ihren Bereitstellungsprozess, bemerken Sie weiter, dass die Vision von AD DS Verwaltung vereinfacht werden.  
  
Die folgende Abbildung zeigt die Active Directory-Domänendienste-Rolle Installationsvorgang Ausführung **PowerShell.exe** und bis zur heraufstufung des Domänencontrollers.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment_powershell.png)  
  
|||  
|-|-|  
|ServerManager-Cmdlets|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-WindowsFeature/Add-WindowsFeature|***-Name***<br /><br />*– Starten*<br /><br />*-IncludeAllSubFeature*<br /><br />*-IncludeManagementTools*<br /><br />-Quelle<br /><br />*-ComputerName*<br /><br />-Credential<br /><br />-LogPath<br /><br />*-Vhd*<br /><br />*-ConfigurationFilePath*|  
  
> [!NOTE]  
> Zwar nicht zwingend erforderlich, das Argument **- IncludeManagementTools** wird dringend empfohlen, wenn Sie die Binärdateien der AD DS-Serverrolle installieren  
  
Das ServerManager-Modul macht Rolle Installation, Status und Teile des neuen DISM-Moduls für Windows PowerShell verfügbar. Diese Ebenenstruktur vereinfacht viele Aufgaben und senkt die Nutzung des umfangreichen (bei Fehlbedienung jedoch) DISM-Modul.  
  
Verwendung **Get-Command** Aliase und Cmdlets in ServerManager zu exportieren.  
  
```powershell  
Get-Command -module ServerManager  
```  
  
Zum Beispiel:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetCommand.png)  
  
Um die Active Directory-Domänendienste-Rolle hinzuzufügen, führen Sie einfach die **Install-WindowsFeature** mit der AD DS-Rollennamen als Argument. Wie Server-Manager werden alle erforderlichen Dienste, die implizit für die AD DS-Rolle automatisch installiert.  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services  
```  
  
Wenn Sie auch die AD DS-Verwaltungstools - und sehr zu empfehlen ist - Geben Sie dann die **- IncludeManagementTools** Argument:  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools  
```  
  
Zum Beispiel:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallWinFeature.png)  
  
Verwenden Sie zum Auflisten aller Features und Rollen mit deren Installationsstatus **Get-WindowsFeature** ohne Argumente. Geben Sie **- ComputerName** Argument, um den Installationsstatus von einem Remoteserver aus.  
  
```powershell  
Get-WindowsFeature  
```  
  
Da **Get-WindowsFeature** verfügt nicht über eine Filterung Mechanismus, müssen Sie verwenden **Where-Object** mit einer Pipeline auf bestimmte Features zu finden. Pipelines sind Kanäle zur Datenübergabe zwischen mehreren Cmdlets zum Übergeben von Daten und das Where-Object-Cmdlet dient als Filter. Die integrierte **$_** -Variable stellt das aktuelle Objekt über die Pipeline mit allen eventuell enthaltenen Eigenschaften übergeben.  
  
```powershell  
Get-WindowsFeature | where-object <options>  
```  
  
Z. B. alle Funktionen mit "Active Dir" in ihren **Anzeigenamen** Eigenschaft verwenden:  
  
```powershell  
Get-WindowsFeature | where displayname -like "*active dir*"  
```  
  
Weitere Beispiele:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetWindowsFeature.png)  
  
Weitere Informationen zu Windows PowerShell-Operationen mit Pipelines und Where-Object finden Sie unter [Piping und die Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).  
  
Beachten Sie auch, dass Windows PowerShell 3.0 die diese Pipeline-Operation benötigten Befehlszeilenargumente deutlich vereinfacht. Windows PowerShell 2.0 würde erforderlich sind:  
  
```powershell  
Get-WindowsFeature | where {$_.displayname - like "*active dir*"}  
```  
  
Mithilfe von Windows PowerShell-Pipeline können Sie lesbare Ergebnisse erzielen. Zum Beispiel:  
  
```powershell  
Install-WindowsFeature | Format-List  
Install-WindowsFeature | select-object | Format-List  
  
```  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDS.png)  
  
Hinweis: wie durch die Verwendung der **Select-Object** Cmdlet mit dem **- Expandproperty** -Argument interessante Daten zurückgibt:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSWithTools.png)  
  
> [!NOTE]  
> Die **Select-Object - Expandproperty** Argument gesamtleistung der Installation etwas verlangsamt.  
  
### <a name="BKMK_PS"></a>Erstellen einer AD DS-Gesamtstruktur-Stammdomäne mit WindowsPowerShell  
Um eine neue Active Directory-Gesamtstruktur, die mithilfe des ADDSDeployment-Moduls zu installieren, verwenden Sie das folgende Cmdlet:  
  
```powershell  
Install-addsforest  
```  
  
Die **Install-AddsForest** Cmdlet hat nur zwei Phasen (voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den mindestargument **- Domainname**.  
  
|||  
|-|-|  
|ADDSDeployment-Cmdlet|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-Addsforest|-Bestätigen<br /><br />*-CreateDNSDelegation*<br /><br />*-DatabasePath*<br /><br />*-DomainMode*<br /><br />***-Domänenname***<br /><br />***-DomainNetBIOSName***<br /><br />*-Dnsdelegationcredential über*<br /><br />*-ForestMode*<br /><br />-Force<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-NoDnsOnNetwork<br /><br />-NoRebootOnCompletion<br /><br />*-SafeModeAdministratorPassword*<br /><br />-SkipAutoConfigureDNS<br /><br />– SkipPreChecks<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> Die **- DomainNetBIOSName** Argument ist erforderlich, wenn Sie den automatisch generierten 15-stelligen Namen basierend auf dem DNS-Domänennamen als Präfix ändern möchten, oder wenn der Name mehr als 15 Zeichen umfasst.  
  
Die entsprechenden Server-Manager **Bereitstellungskonfiguration** ADDSDeployment-Cmdlet und Argumente sind:  
  
```powershell  
Install-ADDSForest  
-DomainName <string>  
```  
  
Die entsprechende Server-Manager Domain Controller ADDSDeployment-Argumente sind:  
  
```powershell  
-ForestMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-InstallDNS <{$false | $true}>  
-SafeModeAdministratorPassword <secure string>  
  
```  
  
Die **Install-ADDSForest** -Argumente dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben.  
  
Die **SafeModeAdministratorPassword** des Arguments Sonderregeln:  
  
-   Wenn *nicht angegeben* als Argument, das Cmdlet fordert Sie zur Eingabe und Bestätigung eines maskierten Kennworts. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Z. B. zum Erstellen einer neuen Gesamtstruktur mit dem Namen "corp.contoso.com" und werden zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert:  
  
    ```powershell  
    Install-ADDSForest "DomainName corp.contoso.com  
    ```  
  
-   Wenn angegeben *mit dem Wert*, der Wert muss eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Angenommen, Sie können manuell Kennwort anfordern mithilfe der **Read-Host** Cmdlet, um den Benutzer für eine sichere Zeichenfolge aufzufordern:  
  
```powershell  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> Wie die vorherige Option keine kennwortbestätigung umfasst, verwenden Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können auch eine sichere Zeichenfolge als eine konvertierte klartextvariable angeben, obwohl davon dringend abgeraten wird.  
  
```powershell  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
Schließlich können Sie das verborgene Kennwort in einer Datei speichern und später wiederverwenden, ohne das Klartextkennwort angezeigt. Zum Beispiel:  
  
```powershell  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartext-oder abgeblendeten Kennworts wird nicht empfohlen. Jeder der Ausführung dieses Befehls in einem Skript oder über die Schulter schaut, weiß das DSRM-Kennwort dieses Domänencontrollers. Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort rückgängig machen. Mit diesem Wissen können sie auf einen Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden und Identitätswechsel für den Domänencontroller selbst, erhöhen ihre Berechtigungen auf der höchsten Ebene im Active Directory-Gesamtstruktur. Eine Reihe von Schritten mit weiteren **System.Security.Cryptography** zum Verschlüsseln der Datei Daten werden empfohlen, sind jedoch nicht. Die bewährte Methode ist die Speicherung des Kennworts vollständig zu vermeiden.  
  
Das ADDSDeployment-Cmdlet bietet eine zusätzliche Option zum Überspringen der automatischen Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Sie können nicht diese Konfigurationsoption überspringen, wenn Sie Server-Manager verwenden. Dieses Argument ist nur dann, wenn Sie die DNS-Serverrolle vor der Konfiguration des Domänencontrollers installiert relevant:  
  
```powershell  
-SkipAutoConfigureDNS  
```  
  
Die **DomainNetBIOSName** Vorgang ist auch spezielle:  
  
-   Wenn die **DomainNetBIOSName** -Argument nicht angegeben wird, mit einem NetBIOS-Domänenname und das einteilige Präfix des Domänennamens in der **Domänenname** maximal 15 Zeichen lang ist, und klicken Sie dann heraufstufung mit einem automatisch generierten Namen fortgesetzt.  
  
-   Wenn die **DomainNetBIOSName** -Argument nicht angegeben wird, mit einem NetBIOS-Domänenname und das einteilige Präfix des Domänennamens in der **Domänenname** 16 Zeichen lang ist, schlägt die heraufstufung fehl.  
  
-   Wenn die **DomainNetBIOSName** -Argument mit einem NetBIOS-Domänennamen mit maximal 15 Zeichen angegeben ist, und klicken Sie dann heraufstufung mit diesem angegebenen Namen fortgesetzt.  
  
-   Wenn die **DomainNetBIOSName** Argument mit mindestens einen NetBIOS-Domänennamen mit 16 Zeichen angegeben ist, schlägt die heraufstufung fehl.  
  
Die entsprechenden Server-Manager zusätzliche Optionen ADDSDeployment-Argumente ist:  
  
```powershell  
-domainnetbiosname <string>  
```  
  
Die entsprechenden Server-Manager **Pfade** ADDSDeployment-Argumente sind:  
  
```powershell  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
  
```  
  
Verwenden Sie das optionale **Whatif** Argument mit dem **Install-ADDSForest** Cmdlet, um Konfigurationsinformationen zu überprüfen. Dadurch können Sie die expliziten und impliziten Werte der Argumente eines Cmdlets finden Sie unter.  
  
Zum Beispiel:  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSPaths.png)  
  
Sie können nicht umgehen der **Prüfung** Wenn mithilfe von Server-Manager, aber Sie können überspringen, wenn das AD DS-Bereitstellung-Cmdlet mit dem folgenden Argument verwendet wird:  
  
```powershell  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft rät davon ab, die voraussetzungsüberprüfung zu überspringen, kann dazu führen, dass eine teilweise heraufstufung des Domänencontrollers oder AD DS-Gesamtstruktur beschädigt.  
  
Genau wie beim Server-Manager **Install-ADDSForest** darauf hingewiesen, dass die Förderung der Server automatisch neu gestartet wird.  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSReboot.png)  
  
![Installieren einer neuen Gesamtstruktur](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallProgress.png)  
  
Verwenden, um die Aufforderung zum Neustart automatisch zu akzeptieren, die **-erzwingen** oder **-bestätigen: $false** Argumente mit jedem ADDSDeployment Windows PowerShell-Cmdlet. Um zu verhindern, dass den Server am Ende der heraufstufung automatisch neu, verwenden Sie die **- Norebootoncompletion** Argument.  
  
> [!WARNING]  
> Überschreiben des Neustarts wird nicht empfohlen. Der Domänencontroller muss neu gestartet, um korrekt zu funktionieren.  
  
## <a name="see-also"></a>Siehe auch  
[Active Directory Domain Services (TechNet-Portal)](https://technet.microsoft.com/library/cc770946(WS.10).aspx)  
[Active Directory-Domänendienste für Windows Server 2008 R2](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
[Active Directory-Domänendienste für WindowsServer 2008](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
[Technische Referenz zu Windows Server (WindowsServer 2003)](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
[Active Directory-Verwaltungscenter: Erste Schritte (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd560651(WS.10).aspx)  
[Active Directory-Verwaltung mit WindowsPowerShell (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd378937(WS.10).aspx)  
[Bitten Sie den Directory Services Team (Official Microsoft Commercial Technical Support Blog)](http://blogs.technet.com/b/askds)  
  

