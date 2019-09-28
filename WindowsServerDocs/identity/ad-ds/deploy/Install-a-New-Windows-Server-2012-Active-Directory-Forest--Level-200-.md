---
ms.assetid: b3d6fb87-c4d4-451c-b3de-a53d2402d295
title: Installieren einer neuen Active Directory-Gesamtstrukturdomäne in Windows Server 2012 (Stufe 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a9bdc3b237d0d0f44995f2c359cc3ef6ed8568a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71400367"
---
# <a name="install-a-new-windows-server-2012-active-directory-forest-level-200"></a>Installieren einer neuen Active Directory-Gesamtstrukturdomäne in Windows Server 2012 (Stufe 200)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel bietet eine Einführung in das neue Domänencontroller-Heraufstufungsfeature für Windows Server 2012 Active Directory-Domänendienste. AD DS ersetzt in Windows Server 2012 das Dcpromo-Tool durch ein Bereitstellungssystem mithilfe von Server-Manager und Windows PowerShell.  
  
-   [Vereinfachte Verwaltung Active Directory Domain Services](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SimplifiedAdmin)  
  
-   [Technische Übersicht](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_TechOverview)  
  
-   [Bereitstellen einer Gesamtstruktur mit Server-Manager](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Bereitstellen einer Gesamtstruktur mit Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_PSForest)  
  
## <a name="BKMK_SimplifiedAdmin"></a>Vereinfachte Verwaltung Active Directory Domain Services  
Mit Windows Server 2012 wurde die nächste Generation der vereinfachten Administration von Active Directory-Domänendiensten eingeführt. Dies ist die radikalste Umgestaltung von Domänen seit Windows 2000 Server. Die vereinfachte AD DS-Administration ist eine Umsetzung der Erfahrungen zwölf Jahren Active Directory und bietet Architekten und Administratoren ein flexibleres, intuitiveres und leichter zu unterstützendes Administrationserlebnis. Hierzu mussten wir neue Versionen existierender Technologien erstellen und die Funktionen einiger Komponenten aus Windows Server 2008 R2 erweitern.  
  
### <a name="what-is-ad-ds-simplified-administration"></a>Was ist die vereinfachte AD DS-Administration?  
Die vereinfachte AD DS-Administration ist ein neuartiger Weg der Domänen-Bereitstellung. Dazu gehören unter anderem die folgenden Features:  
  
-   Die AD DS-Rollenbereitstellung ist nun Teil der neuen Server-Manager-Architektur und erlaubt die Remote-Installation.  
  
-   Als AD DS-Bereitstellungs- und Konfigurationsmodul dient nun Windows PowerShell, selbst bei Verwendung einer grafischen Benutzeroberfläche.  
  
-   Zur Heraufstufung gehört nun eine Voraussetzungsprüfung, bei der die Bereitschaft von Gesamtstruktur und Domäne für den neuen Domänencontroller geprüft und somit Fehler bei der Heraufstufung vermieden werden.  
  
-   Die Windows Server 2012-Gesamtstrukturfunktionsebene enthält keine neuen Features, und die Domänenfunktionsebene wird nur für einen Teil der neuen Kerberos-Features benötigt. Administratoren sind daher weniger häufig auf homogene Domänencontroller-Umgebungen angewiesen.  
  
### <a name="purpose-and-benefits"></a>Zweck und Vorteile  
Manche dieser Änderungen erscheinen auf den ersten Blick komplexer anstatt einfacher. Durch die Neugestaltung des AD DS-Bereitstellungsprozesses entstand jedoch die Möglichkeit, zahlreiche Schritte und bewährte Methoden in wenige und einfache Schritte zusammenzufassen. Z. B. umfasst die grafische Konfiguration eines neuen Replikat-Domänencontrollers nun nur noch acht Dialogfelder anstatt wie bisher zwölf. Zum Erstellen einer neuen Active Directory-Gesamtstruktur genügt ein *einziger* Windows PowerShell-Befehl mit nur *einem* Argument: dem Namen der Domäne.  
  
Warum die starke Gewichtung von Windows PowerShell in Windows Server 2012? Die verteilte Datenverarbeitung entwickelt sich ständig weiter, und Windows PowerShell bietet ein einziges Modul für Konfiguration und Wartung in Form von grafischen Oberflächen und Befehlszeilenschnittstellen. IT-Fachleute erhalten die Möglichkeit, Skripts mit vollem Funktionsumfang für beliebige Komponenten mit demselben erstklassigen Komfort zu erstellen, den Entwickler in Form von APIs erhalten. Mit der universellen Verfügbarkeit von cloudbasiertem Computing bietet Windows PowerShell auch endlich die Möglichkeit, Server remote zu administrieren. Computer ohne grafische Oberfläche haben dabei dieselben Verwaltungsoptionen wie solche mit Monitor und Maus.  
  
Erfahrene AD DS-Administratoren werden feststellen, dass ihre bisherigen Kenntnisse von größtem Wert sind. Angehenden Administratoren bietet sich eine wesentlich flachere Lernkurve.  
  
## <a name="BKMK_TechOverview"></a>Technische Übersicht  
  
### <a name="what-you-should-know-before-you-begin"></a>Wichtige Informationen vorab  
Dieser Artikel geht davon aus, dass Sie mit den vorherigen Versionen der Active Directory-Domänendienste vertraut sind und enthält keine Grundsatzinformationen zu deren Zweck und Funktionen. Weitere Informationen zu AD DS finden Sie in den folgenden TechNet-Portalseiten:  
  
-   [Active Directory Domain Services für Windows Server 2008 R2](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
  
-   [Active Directory Domain Services für Windows Server 2008](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
  
-   [Technische Referenz zu Windows Server](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
  
### <a name="functional-descriptions"></a>Funktionsbeschreibungen  
  
#### <a name="ad-ds-role-installation"></a>AD DS-Rolleninstallation  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_SelectServerRoles.gif)  
  
Die Installation der Active Directory-Domänendienste verwendet Server-Manager und Windows PowerShell, wie auch alle anderen Serverrollen und Features in Windows Server 2012. Das Dcpromo.exe-Programm bietet keine GUI-Konfigurationsoptionen mehr.  
  
Sie verwenden einen grafischen Assistenten im Server-Manager oder dem Server-Manager-Modul für Windows PowerShell für lokale und Remote-Installationen. Sie können mehrere Instanzen dieser Assistenten bzw. Cmdlets und unterschiedliche Zielserver in einer einzigen Konsole verwenden, um AD DS gleichzeitig auf mehreren Domänencontrollern bereitzustellen. Obwohl diese neuen Features nicht abwärtskompatibel mit Windows Server 2008 R2 oder früheren Betriebssystemen sind, können Sie die in Windows Server 2008 R2 eingeführte Anwendung Dism.exe weiterhin zur lokalen Rolleninstallation in der klassischen Befehlszeile verwenden.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSAddWindowsFeature.png)  
  
#### <a name="ad-ds-role-configuration"></a>AD DS-Rollenkonfiguration  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
Active Directory Domain Services Konfiguration "früher als Dcpromo bezeichnet" ist jetzt ein diskreter Vorgang von der Rollen Installation. Nach der Installation der AD DS-Rolle konfiguriert ein Administrator den Server mithilfe eines separaten Assistenten im Server-Manager oder über das ADDSDeployment Windows PowerShell-Modul als Domänencontroller.  
  
Die AD DS-Rollenkonfiguration basiert auf zwölf Jahren Erfahrung und konfiguriert Domänencontroller anhand der aktuellsten bewährten Microsoft-Methoden. Domain Name System und globale Kataloge werden nun z. B. standardmäßig auf jedem Domänencontroller installiert.  
  
Mit dem Konfigurations-Assistenten für Server-Manager AD DS werden viele einzelne Dialogfelder in weniger Eingabe Aufforderungen zusammengeführt, und die Einstellungen werden im erweiterten Modus nicht mehr ausgeblendet. Der gesamte Heraufstufungsprozess erfolgt bei der Installation in einem einzigen, erweiterten Dialogfeld. Assistent und ADDSDeployment Windows PowerShell-Modul zeigen wichtige Änderungen und Sicherheitsbedenken an und enthalten Links zu weiteren Informationen.  
  
Dcpromo.exe verbleibt in Windows Server 2012 ausschließlich für unbeaufsichtigte Installationen per Befehlszeile und führt den grafischen Installations-Assistenten nicht mehr aus. Sie sollten die Verwendung von Dcpromo.exe für unbeaufsichtigte Installationen unbedingt einstellen und stattdessen das ADDSDeployment-Modul verwenden, da die nun veraltete ausführbare Datei in der nächsten Windows-Version nicht mehr enthalten sein wird.  
  
Diese neuen Features sind nicht abwärtskompatibel mit Windows Server 2008 R2 oder älteren Betriebssystemen.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSForest.png)  
  
> [!IMPORTANT]
> Dcpromo.exe enthält nun keinen grafischen Assistenten und installiert keine Binärdateien für Rollen oder Feature. Beim Ausführen von Dcpromo.exe aus der Explorer-Shell wird Folgendes zurückgegeben:  
> 
> "Die Assistent zum Installieren von Active Directory Domain Services wird in Server-Manager verschoben. Weitere Informationen finden Sie unter <https://go.microsoft.com/fwlink/?LinkId=220921> ".  
> 
> Bei der Ausführung von Dcpromo.exe /unattend werden die Binärdateien wie in älteren Betriebssystemen weiterhin installiert, allerdings wird eine Warnung ausgegeben:  
> 
> "Der unbeaufsichtigte Vorgang" Dcpromo "wird durch das addsdeployment-Modul für Windows PowerShell ersetzt. Weitere Informationen finden Sie unter <https://go.microsoft.com/fwlink/?LinkId=220924> ".  
> 
> dcpromo.exe ist in Windows Server 2012 veraltet und wird in zukünftigen Windows-Versionen nicht enthalten sein und in diesem Betriebssystem auch nicht mehr erweitert werden. Administratoren sollten dessen Verwendung einstellen und stattdessen die unterstützten Windows PowerShell-Module verwenden, wenn sie Domänencontroller per Befehlszeile erstellen möchten.  
  
#### <a name="prerequisite-checking"></a>Voraussetzungsprüfung  
Zur Domänencontroller-Konfiguration gehört auch eine Voraussetzungsprüfungsphase, die Gesamtstruktur und Domäne vor der Heraufstufung des Domänencontrollers prüft. Geprüft werden unter anderem die Verfügbarkeit der FSMO-Rolle, Benutzerrechte, erweiterte Schemakompatibilität und sonstige Anforderungen. Dieses neue Design verhindert Probleme, bei denen die Heraufstufung des Domänencontrollers beginnt und dann mit einem schwerwiegenden Konfigurationsfehler abgebrochen wird. Dies senkt die Gefahr verwaister Domänencontroller-Metadaten in der Gesamtstruktur und verhindert, dass Server fälschlicherweise davon ausgehen, sie seien Domänencontroller.  
  
## <a name="BKMK_SMForest"></a>Bereitstellen einer Gesamtstruktur mit Server-Manager  
Dieser Abschnitt beschreibt die Installation des ersten Domänencontrollers in einer Gesamtstruktur-Stammdomäne mithilfe des Server-Managers auf einem Windows Server 2012-Computer mit grafischer Oberfläche.  
  
### <a name="server-manager-ad-ds-role-installation-process"></a>AD DS-Rolleninstallation via Server-Manager  
Das folgende Diagramm zeigt den Prozess der AD DS-Rolleninstallation, von der Ausführung von ServerManager.exe bis zur Heraufstufung des Domänencontrollers.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment.png)  
  
#### <a name="server-pool-and-add-roles"></a>Serverpool und Hinzufügen von Rollen  
Alle Windows Server 2012-Computer, die von dem Computer erreichbar sind, auf dem Server-Manager ausgeführt wird, können für das Pooling verwendet werden. Nach der Zusammenfassung in einem Pool wählen Sie diese Server für die Remoteinstallation von AD DS oder eine andere mögliche Konfigurationsoption in Server-Manager aus.  
  
Wählen Sie zum Hinzufügen von Servern eine der folgenden Optionen aus:  
  
-   Klicken Sie auf **Weitere zu verwaltende Server hinzufügen** in der Dashboard-Begrüßungskachel  
  
-   Klicken Sie im Menü **Verwalten** auf **Server hinzufügen**  
  
-   Klicken Sie mit der rechten Maustaste auf **Alle Server** , und klicken Sie anschließend auf **Server hinzufügen**  
  
Dadurch wird das Dialogfeld Server hinzufügen geöffnet:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddServers.png)  
  
Dort haben Sie drei Möglichkeiten, um Server für die Verwendung oder Gruppierung zum Pool hinzuzufügen:  
  
-   Active Directory-Suche (verwendet LDAP, Computer müssen zu einer Domäne gehören, Betriebssystemfilterung zulässig, unterstützt Platzhalter)  
  
-   DNS-Suche (verwendet DNS-Alias oder IP-Addresse via ARP- oder NetBIOS-Übertragung oder die WINS-Suche, lässt keine Betriebsystemfilterung zu und unterstützt keine Platzhalter)  
  
-   Importieren (verwendet eine Textdateiliste von Servern, die durch Wagenrücklauf/Zeilenvorschub getrennt ist)  
  
Klicken Sie auf **Suche starten**, um eine Serverliste aus demselben Active Directory zurückzugeben, zu dem der Computer gehört. Klicken Sie dann in der Serverliste auf einen oder mehrere Servernamen. Klicken Sie auf den Pfeil nach rechts, um die Server der Liste **Ausgewählt** hinzuzufügen. Verwenden Sie das Dialogfeld **Server hinzufügen** , um die ausgewählten Server zu den Dashboardrollengruppen hinzuzufügen. Klicken Sie alternativ auf **Verwalten** und auf **Servergruppe erstellen**, oder klicken Sie auf **Servergruppe erstellen** in der Dashboard-Kachel **Willkommen bei Server-Manager**, um benutzerdefinierte Servergruppen zu erstellen.  
  
> [!NOTE]  
> Bei dem Verfahren %%amp;quot;Server hinzufügen%%amp;quot; wird nicht überprüft, ob ein Server online oder der Zugriff darauf möglich ist. Beim nächsten Aktualisieren werden jedoch nicht erreichbare Server in der Sicht Verwaltbarkeit von Server-Manager gekennzeichnet  
  
Sie können auf allen zum Pool hinzugefügten Windows Server 2012-Computern Rollen remote installieren:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/tADDS_SMI_TR_AddRolesFeatures.png)  
  
Server unter Betriebssystemen älter als Windows Server 2012 können nicht vollständig verwaltet werden. Die Auswahl **Rollen und Features hinzufügen** führt das ServerManager Windows PowerShell-Modul **Install-WindowsFeature**aus.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddADDSToAnotherServer.png)  
  
Sie können auch das Server-Manager-Dashboard auf einem existierenden Domänencontroller für die Remote-Installation von AD DS verwenden, wobei die Rolle bereits per Rechtsklick auf die AD DS-Dashboardkachel und Auswahl von **AD DS zu anderem Server hinzufügen**vorab ausgewählt ist. Dabei wird **Install-WindowsFeature AD-Domain-Services** aufgerufen.  
  
Der Computer, auf dem Sie Server-Manager ausführen, fügt sich selbst automatisch zum Pool hinzu. Um dort die AD DS-Rolle zu installieren, klicken Sie auf im Menü **Verwalten** auf **Rollen und Features hinzufügen**.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ManageAddRoles.png)  
  
#### <a name="installation-type"></a>Installationstyp  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectInstallationType.png)  
  
Das Dialogfeld **Installationstyp** bietet eine Option, die Active Directory-Domänendienste nicht unterstützt: **Szenariobasierte Installation von Remotedesktopdiensten**. Diese Option erlaubt nur Remotedesktopdienste in einer serverübergreifenden verteilten Arbeitsauslastung. Wenn Sie diese Option auswählen, kann AD DS nicht installiert werden.  
  
Lassen Sie die Standardeinstellungen unverändert, wenn Sie AD DS installieren: **Rollenbasierte oder featurebasierte Installation**.  
  
#### <a name="server-selection"></a>Serverauswahl  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectDestinationServer.png)  
  
Im Dialogfeld **Serverauswahl** können Sie einen der zuvor zum Pool hinzugefügten Server auswählen, sofern dieser erreichbar ist. Der lokale Server, auf dem Server-Manager ausgeführt wird, ist automatisch verfügbar.  
  
Außerdem können Sie offline Hyper-V VHD-Dateien mit dem Windows Server 2012-Betriebssystem auswählen, und Server-Manager fügt die Rolle zu diesen Dateien via Komponentendienste direkt hinzu. Auf diese Weise können Sie virtuelle Server mit den benötigten Komponenten bereitstellen, bevor Sie diese weiter konfigurieren.  
  
#### <a name="server-roles-and-features"></a>Serverrollen und Features  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectServerRoles.png)  
  
Wählen Sie die Rolle **Active Directory-Domänendienste** aus, wenn Sie einen Domänencontroller heraufstufen möchten. Alle Active Directory-Administrationsfeatures und benötigte Dienste werden automatisch installiert, selbst wenn sie eigentlich Teil einer anderen Rolle sind oder in der Server-Manager-Oberfläche nicht als ausgewählt angezeigt werden.  
  
Server-Manager zeigt außerdem in einem Informationsdialog an, welche Administrationsfeatures mit dieser Rolle implizit installiert werden. Dies entspricht dem Argument **-IncludeManagementTools**.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddFeaturesDialog.gif)  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectFeatures.png)  
  
Zusätzliche **Features** können an dieser Stelle nach Belieben hinzugefügt werden.  
  
#### <a name="active-directory-domain-services"></a>Active Directory Domain Services  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSIntro.png)  
  
Das Dialogfeld **Active Directory-Domänendienste** enthält eingeschränkte Informationen zu Anforderungen und bewährten Methoden. Sie fungiert hauptsächlich als Bestätigung, dass Sie die AD DS Rolle gewählt haben. "Wenn dieser Bildschirm nicht angezeigt wird, haben Sie AD DS nicht ausgewählt.  
  
#### <a name="confirmation"></a>Bestätigung  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Confirmation.png)  
  
Das Dialogfeld **Bestätigung** ist der letzte Prüfpunkt vor Beginn der Installation. Dort haben Sie die Option, den Computer bei Bedarf nach der Rolleninstallation neu zu starten. Für die AD DS-Installation ist jedoch kein Neustart erforderlich.  
  
Klicken Sie auf **Installieren**, um zu bestätigen, dass die Rolleninstallation beginnen kann. Die Rolleninstallation kann nach deren Beginn nicht unterbrochen werden.  
  
#### <a name="results"></a>Ergebnisse  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Results.png)  
  
Das Dialogfeld **Ergebnisse** zeigt den aktuellen Installationsfortschritt und Installationsstatus an. Die Rolleninstallation wird auch dann fortgesetzt, wenn der Server-Manager geschlossen wird.  
  
Sie sollten die Installationsergebnisse dennoch stets überprüfen. Wenn Sie das Dialogfeld **Ergebnisse** vor dem Ende der Installation schließen, können Sie die Ergebnisse mit dem Server-Manager-Benachrichtigungskennzeichen prüfen. Server-Manager zeigt außerdem eine Warnmeldung für alle Server an, auf denen die AD DS-Rolle installiert wurde, die aber noch nicht als Domänencontroller konfiguriert wurden.  
  
**Aufgaben Benachrichtigungen**  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskNotofications.png)  
  
**AD DS Details**  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSDetails.png)  
  
**Aufgaben Details**  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskDetails.png)  
  
#### <a name="promote-to-domain-controller"></a>Heraufstufen als Domänencontroller  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Promote.png)  
  
Nach Abschluss der AD DS-Rolleninstallation können Sie die Konfiguration fortsetzen, indem Sie auf den Link **Server zu einem Domänencontroller heraufstufen** klicken. Dieser Schritt ist erforderlich, um den Server zu einem Domänencontroller zu machen. Allerdings muss der Konfigurations-Assistent nicht unbedingt sofort ausgeführt werden. Sie können z. B. Server lediglich mit den AD DS-Binärdateien bereitstellen und anschließend zur späteren Konfiguration an andere Filialen verschicken. Indem Sie die AD DS-Rolle vor dem Versand hinzufügen, sparen Sie Zeit nach dem Erreichen des endgültigen Standorts. Außerdem beachten Sie auf diese Weise die bewährte Methode, Domänencontroller nicht über Tage oder Wochen hinweg offline zu belassen. Zuletzt können Sie auf diese Weise Komponenten vor der Domänencontroller-Heraufstufung aktualisieren und in der Folge zumindest einen Neustart einsparen.  
  
Wenn Sie zu einem späteren Zeitpunkt auf diesen Link klicken, werden die folgenden ADDSDeployment-Cmdlets aufgerufen: **install-addsforest**, **install-addsdomain**oder **install-addsdomaincontroller**.  
  
### <a name="uninstallingdisabling"></a>Deinstallieren/Deaktivieren  
Sie können die AD DS-Rolle wie jede andere Rolle deaktivieren, unabhängig davon, ob Sie den Server zu einem Domänencontroller heraufgestuft haben. Nach dem Entfernen der AD DS-Rolle ist jedoch ein Neustart erforderlich.  
  
Die Entfernung der Active Directory-Domänendienste-Rolle unterscheidet sich von der Installation dadurch, dass der Domänencontroller vor deren Abschluss herabgestuft werden muss. Dadurch wird verhindert, dass die Rollen-Binärdateien eines Domänencontroller deinstalliert werden, ohne dass die Metadaten in der Gesamtstruktur zuvor bereinigt werden. Weitere Informationen finden Sie unter herab [Stufen von Domänen Controllern und Domänen &#40;Ebene 200&#41;](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
> [!WARNING]  
> Das Entfernen der AD DS-Rollen mithilfe von Dism.exe oder dem Windows PowerShell DISM-Modul nach der Heraufstufung eines Domänencontrollers wird nicht unterstützt und führt dazu, dass der Server nicht mehr normal startet.  
>   
> Im Gegensatz zu Server-Manager oder dem AD DS-Bereitstellungsmodul für Windows PowerShell handelt es sich bei DISM um einen systemeigenen Dienst, der keine Kenntnisse von AD DS und deren Konfiguration hat. Verwenden Sie Dism.exe oder das Windows PowerShell DISM-Modul nicht zum Entfernen der AD DS-Rolle, es sei denn, der Server ist bereits kein Domänencontroller mehr.  
  
### <a name="create-an-ad-ds-forest-root-domain-with-server-manager"></a>Erstellen einer AD DS Gesamtstruktur-Stammdomäne in Server-Manager  
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory-Domänendienste, wenn Sie die AD DS-Rolle zuvor installiert haben und den **Konfigurations-Assistenten für die Active Directory-Domänendienste** über den Server-Manager gestartet haben.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_forestdeploy2.png)  
  
#### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddNewForest.png)  
  
In Server-Manager beginnt jede Heraufstufung eines Domänencontrollers auf der Seite **Bereitstellungskonfiguration** . Die restlichen Optionen und erforderlichen Felder auf dieser Seite und den folgenden Seiten variieren in Abhängigkeit von dem von Ihnen ausgewählten Bereitstellungsvorgang.  
  
Klicken Sie auf **Neue Gesamtstruktur hinzufügen**, um eine neue Active Directory-Gesamtstruktur zu erstellen. Sie müssen einen gültigen Namen für die Stammdomäne angeben. der Name darf nicht aus einer einzelnen Bezeichnung bestehen (z. B. *contoso.com* oder ein ähnlicher Name, und nicht nur *contoso*) und muss die DNS-Anforderungen für Domänennamen erfüllen.  
  
Weitere Informationen zu gültigen Domänennamen finden Sie im KB-Artikel [Naming conventions in Active Directory for computers, domains, sites, and OUs](https://support.microsoft.com/kb/909264).  
  
> [!WARNING]  
> Erstellen Sie keine neuen Active Directory-Gesamtstrukturen, die denselben Namen haben wie ein externer DNS-Name. Wenn Ihre Internet-DNS-URL beispielsweise http://contoso.com ist, müssen Sie einen anderen Namen für die interne Gesamtstruktur auswählen, um zukünftige Kompatibilitätsprobleme zu vermeiden. Der Name sollte eindeutig und seine Verwendung für den Webdatenverkehr unwahrscheinlich sein. Zum Beispiel: corp.contoso.com.  
  
Neue Gesamtstrukturen benötigen keine neuen Anmeldeinformationen für das Domänen-Administratorkonto. Der Domänencontroller-Heraufstufungsprozess verwendet die Anmeldeinformationen des integrierten Administratorkontos des ersten Domänencontrollers, der zur Erstellung der Gesamtstruktur-Stammdomäne verwendet wurde. Das integrierte Administratorkonto kann (standardmäßig) nicht deaktiviert oder ausgesperrt werden. Dieses Konto kann der einzige Einstiegspunkt in eine Gesamtstruktur sein, wenn die anderen Administratorkonten der Domäne unbrauchbar sind. Sie müssen unbedingt das Kennwort kennen, bevor Sie eine neue Gesamtstruktur bereitstellen.  
  
**DomainName** muss ausgefüllt werden und erfordert einen vollqualifizierten DNS-Domänennamen.  
  
#### <a name="domain-controller-options"></a>Domänencontrolleroptionen  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DCOptions_Forest.gif)  
  
In den **Domänencontrolleroptionen** können Sie **Gesamtstrukturfunktionsebene** und **Domänenfunktionsebene** für die neue Gesamtstruktur-Stammdomäne konfigurieren. Standardmäßig sind diese Einstellungen Windows Server 2012 in einer neuen Gesamtstruktur-Stamm Domäne. Die Gesamtstruktur Funktionsebene von Windows Server 2012 bietet keine neuen Funktionen auf der Windows Server 2008 R2-Gesamtstruktur Funktionsebene. Die Domänen Funktionsebene Windows Server 2012 ist nur erforderlich, um die neuen Kerberos-Einstellungen "immer Ansprüche bereitstellen" und "nicht hochgerüstete Authentifizierungsanforderungen fehlschlagen" zu implementieren. Ein primärer Verwendungs Aufwand für Funktionsebenen in Windows Server 2012 besteht darin, die Teilnahme an der Domäne auf Domänen Controller einzuschränken, die die Mindestanforderungen für Betriebssysteme erfüllen. Anders ausgedrückt: Sie können die Domänen Funktionsebene Windows Server 2012 angeben, dass nur Domänen Controller, auf denen Windows Server 2012 ausgeführt wird, die Domäne hosten können.  Windows Server 2012 implementiert ein neues domänencontrollerflag namens **DS_WIN8_REQUIRED** in der **DsGetDcName** -Funktion von Netlogon, bei der ausschließlich Windows Server 2012-Domänen Controller verwendet werden. Auf diese Weise können Sie homogenere oder heterogenere Gesamtstrukturen hinsichtlich der erlaubten Betriebssysteme auf den Domänencontrollern nutzen.  
  
Weitere Informationen zur Domänencontrollersuche finden Sie unter [Directory Service Functions](https://msdn.microsoft.com/library/ms675900(VS.85).aspx).  
  
Die einzige konfigurierbare Domänencontroller-Funktion ist die DNS-Server-Option. Für eine hohe Verfügbarkeit in verteilten Umgebungen empfiehlt Microsoft, dass alle Domänencontroller DNS-Dienste bereitstellen. Aus diesem Grund aktiviert der Assistent diese Optionen beim Installieren eines Domänencontrollers in allen Modi und Domänen standardmäßig. Optionen für den globalen Katalog und schreibgeschützte Domänencontroller sind bei der Erstellung einer neuen Gesamtstruktur-Stammdomäne nicht verfügbar. Der erste Domänencontroller muss ein GC sein und darf kein schreibgeschützter Domänencontroller (RODC) sein.  
  
Das angegebene **Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus** muss die Kennwortrichtlinie für den Server erfüllen, laut der standardmäßig kein sicheres, sondern lediglich ein nicht leeres Kennwort erforderlich ist. Wählen Sie stets ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase aus.  
  
#### <a name="dns-options-and-dns-delegation-credentials"></a>DNS-Optionen und DNS-Delegierungs-Anmeldeinformationen  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestDNSOptions.png)  
  
Auf der Seite **DNS-Optionen** können Sie DNS-Delegierung konfigurieren und alternative DNS-Administratoranmeldeinformationen einrichten.  
  
Sie können DNS-Optionen oder -Delegierung bei der Installation einer neuen Active Directory-Gesamtstruktur-Stammdomäne im Konfigurations-Assistenten für Active Directory-Domänendienste nicht konfigurieren, wenn Sie **DNS-Server** auf der Seite **Domänencontrolleroptionen** ausgewählt haben. Die Option **DNS-Delegierung erstellen** ist verfügbar, wenn Sie eine neue Stamm-DNS-Zone für eine Gesamtstruktur in einer existierenden DNS-Server-Infrastruktur erstellen. Mit dieser Option können Sie alternative DNS-Administratoranmeldeinformationen eingeben, die Berechtigungen zur Änderung der DNS-Zone haben.  
  
Weitere Informationen dazu, ob Sie eine DNS-Delegierung erstellen müssen, finden Sie unter [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
#### <a name="additional-options"></a>Zusätzliche Optionen  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestAdditionalOptions.png)  
  
Auf der Seite **Zusätzliche Optionen** wird der NetBIOS-Name der Domäne angezeigt, und es besteht die Möglichkeit, den Namen zu überschreiben. Standardmäßig stimmt der NetBIOS-Domänenname mit dem linken Teil des vollqualifizierten Domänennamens überein, der auf der Seite **Bereitstellungskonfiguration** eingegeben wurde. Wenn Sie z. B. den vollqualifizierten Domänennamen corp.contoso.com eingegeben haben, dann ist der Standard-NetBIOS-Name CORP.  
  
Wenn der Name maximal 15 Zeichen lang ist und nicht mit anderen NetBIOS-Namen in Konflikt steht, wird er nicht verändert. Falls der Name mit einem anderen NetBIOS-Namen in Konflikt steht, wird eine Nummer an den Namen angefügt. Wenn der Name länger als 15 Zeichen ist, schlägt der Assistent einen eindeutigen, abgeschnittenen Namen vor. In beiden Fällen prüft der Assistent zunächst mit einer WINS-Suche und einem NetBIOS-Broadcast, ob der Name bereits vergeben ist.  
  
Weitere Informationen zu gültigen Domänennamen finden Sie im KB-Artikel [Naming conventions in Active Directory for computers, domains, sites, and OUs](https://support.microsoft.com/kb/909264).  
  
#### <a name="paths"></a>Pfade  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPaths.png)  
  
Auf der Seite **Pfade** können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von %systemroot% (z. B. C:\Windows).  
  
#### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestReviewOptions.png)  
  
Auf der Seite **Optionen prüfen** können Sie vor dem Starten der Installation Ihre Einstellungen überprüfen und sicherstellen, dass Ihre Anforderungen erfüllt werden. Dies ist jedoch nicht die letzte Möglichkeit, um die Installation mit Server-Manager zu stoppen. Dies ist lediglich eine Option zum Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetze  
  
Die Seite **Optionen prüfen** im Server-Manager bietet zudem die optionale Schaltfläche **Skript anzeigen** zum Erstellen einer Unicode-Textdatei, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dies ermöglicht Ihnen die Verwendung der grafischen Oberfläche von Server-Manager als Windows PowerShell-Bereitstellungsstudio. Mithilfe des Konfigurations-Assistenten für die Active Directory-Domänendienste können Sie Optionen konfigurieren, die Konfiguration exportieren und den Assistenten abbrechen. Bei diesem Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
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
> Server-Manager füllt bei der Heraufstufung normalerweise alle Argumente mit Werten aus und verlässt sich nicht auf Standardwerte (da sich diese in zukünftigen Windows-Versionen oder Service Packs ändern können). Die einzige Ausnahme hierbei ist das **-safemodeadministratorpassword**-Argument (das im Skript bewusst ausgelassen wird). Lassen Sie dieses Argument bei der interaktiven Ausführung des Cmdlets aus, um eine Bestätigungsaufforderung zu erzwingen.  
  
#### <a name="prerequisites-check"></a>Voraussetzungsüberprüfung  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in der AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration zur Unterstützung einer neuen AD DS-Gesamtstruktur geeignet ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne führt der Konfigurations-Assistent des Server-Managers für Active Directory-Domänendienste eine Reihe modularer Tests durch. Diese Tests geben anschließend Empfehlungen für Reparaturoptionen aus. Sie können die Tests beliebig oft ausführen. Der Prozess für den Domänencontroller kann erst fortgesetzt werden, wenn alle Voraussetzungstests positiv abgeschlossen wurden.  
  
Bei der **Voraussetzungsüberprüfung** werden außerdem relevante Informationen wie z. B. Sicherheitsänderungen angezeigt, die ältere Betriebssysteme betreffen.  
  
Weitere Informationen zu den Voraussetzungsprüfungen finden Sie unter [Prerequisite Checking](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
#### <a name="installation"></a>Installation  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestInstallation.png)  
  
Wenn die Seite **Installation** angezeigt wird, beginnt die Konfiguration des Domänencontrollers und kann nicht angehalten oder abgebrochen werden. Detaillierte Informationen werden auf dieser Seite angezeigt und in die Protokolle geschrieben:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
> [!NOTE]  
> Sie können mehrere Konfigurations-Assistenten für Rolleninstallationen und AD DS aus derselben Server-Manager-Konsole gleichzeitig ausführen.  
  
#### <a name="results"></a>Ergebnisse  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
Auf der Seite **Ergebnisse** werden Erfolg bzw. Misserfolg der Heraufstufung sowie alle wichtigen Administrationsinformationen angezeigt. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  
## <a name="BKMK_PSForest"></a>Bereitstellen einer Gesamtstruktur mit Windows PowerShell  
Dieser Abschnitt beschreibt die Installation des ersten Domänencontrollers in einer Gesamtstruktur-Stammdomäne mithilfe von Windows PowerShell auf einem Windows Server 2012-Core-Computer.  
  
### <a name="windows-powershell-ad-ds-role-installation-process"></a>AD DS-Rolleninstallation via Windows PowerShell  
Indem Sie einige unkomplizierte ServerManager Bereitstellungs-Cmdlets in Ihren Bereitstellungsprozess integrierten, können Sie die vereinfachte Administration von AD DS noch weiter vorantreiben.  
  
Die folgende Abbildung zeigt den Prozess der AD DS-Rolleninstallation, von der Ausführung von **PowerShell.exe** bis zur Heraufstufung des Domänencontrollers.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment_powershell.png)  
  
|||  
|-|-|  
|ServerManager-Cmdlet|Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-WindowsFeature/Add-WindowsFeature|***-Name***<br /><br />*-Neu starten*<br /><br />*-Includeallsubfeature*<br /><br />*-Includemanagementtools*<br /><br />-Source<br /><br />*-Computername*<br /><br />-Credential<br /><br />-LogPath<br /><br />*-VHD*<br /><br />*-Configurationfilepath*|  
  
> [!NOTE]  
> Das Argument **-IncludeManagementTools** ist zwar nicht zwingend erforderlich, sollte jedoch beim Installieren der AD DS-Rollenbinärdateien unbedingt angegeben werden  
  
Das ServerManager-Modul macht Rolleninstallation, Status und die Entfernungskomponenten des neuen DISM-Moduls für Windows PowerShell verfügbar. Diese Ebenenstruktur vereinfacht viele Aufgaben und senkt die Nutzung des umfangreichen (bei Fehlbedienung jedoch gefährlichen) DISM-Moduls.  
  
Verwenden Sie **Get-Command**, um Aliase und Cmdlets in ServerManager zu exportieren.  
  
```powershell  
Get-Command -module ServerManager  
```  
  
Zum Beispiel:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetCommand.png)  
  
Führen Sie einfach **Install-WindowsFeature** mit dem AD DS-Rollennamen als Argument aus, um die Active Directory-Domänendienste-Rolle hinzuzufügen. Wie auch beim Server-Manager werden alle implizit für die AD DS-Rolle benötigten Dienste automatisch installiert.  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services  
```  
  
Falls Sie die AD DS-Management-Tools installieren möchten - was sehr zu empfehlen ist - geben Sie zusätzlich das **-IncludeManagementTools** -Argument an:  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools  
```  
  
Zum Beispiel:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallWinFeature.png)  
  
Um alle Features und Rollen mit deren Installationsstatus anzuzeigen, rufen Sie **Get-WindowsFeature** ohne Argumente auf. Geben Sie das **-ComputerName**-Argument an, um den Installationsstatus eines Remote-Servers abzufragen.  
  
```powershell  
Get-WindowsFeature  
```  
  
Da **Get-WindowsFeature** keinen Filtermechanismus hat, müssen Sie **Where-Object** mit einer Pipeline verwenden, um bestimmte Features zu finden. Pipelines sind Kanäle zur Datenübergabe zwischen mehreren Cmdlets, und das Where-Object-Cmdlet dient als Filter. Die integrierte **$_** -Variable stellt das aktuelle Objekt mit allen eventuell enthaltenen Eigenschaften dar, das durch die Pipeline geleitet wird.  
  
```powershell  
Get-WindowsFeature | where-object <options>  
```  
  
Verwenden Sie den folgenden Befehl, um alls Features zu finden, deren **Display Name**-Eigenschaft die Zeichenfolge "Active Dir" enthält:  
  
```powershell  
Get-WindowsFeature | where displayname -like "*active dir*"  
```  
  
Weitere Beispiele:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetWindowsFeature.png)  
  
Weitere Informationen zu Windows PowerShell-Vorgängen mit Pipelines und Where-Object finden Sie unter [Piping and the Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).  
  
Windows PowerShell 3.0 hat die für diese Pipeline-Operation benötigten Befehlszeilenargumente deutlich vereinfacht. In Windows PowerShell 2.0 hätten Sie den folgenden Befehl verwendet:  
  
```powershell  
Get-WindowsFeature | where {$_.displayname - like "*active dir*"}  
```  
  
Mit der Windows PowerShell-Pipeline können Sie lesbare Ergebnisse erzielen. Zum Beispiel:  
  
```powershell  
Install-WindowsFeature | Format-List  
Install-WindowsFeature | select-object | Format-List  
  
```  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDS.png)  
  
Beachten Sie, dass das **Select-Object**-Cmdlet mit dem **-expandproperty**-Argument interessante Daten zurückgibt:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSWithTools.png)  
  
> [!NOTE]  
> Das Argument **Select-Object -expandproperty** führt zu einer leichten Verlangsamung der Gesamtleistung der Installation.  
  
### <a name="BKMK_PS"></a>Erstellen einer AD DS-Gesamtstruktur-Stamm Domäne mit Windows PowerShell  
Verwenden Sie das folgende Cmdlet, um eine neue Active Directory-Gesamtstruktur mithilfe des ADDSDeployment-Moduls zu installieren:  
  
```powershell  
Install-addsforest  
```  
  
Das **Install-AddsForest** -Cmdlet besteht nur aus zwei Phasen (Voraussetzungsüberprüfung und Installation). Die beiden folgenden Abbildungen zeigen die Installationsphase mit dem benötigten Mindestargument **-domainname**.  
  
|||  
|-|-|  
|ADDSDeployment-Cmdlet|Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.)|  
|install-addsforest|-Confirm<br /><br />*-"-Kreatednsdelegation"*<br /><br />*-DatabasePath*<br /><br />*-DomainMode*<br /><br />***-Domain Name***<br /><br />***-DomainNetbiosName***<br /><br />*-Dnsdelegationcredential*<br /><br />*-ForestMode*<br /><br />-Force<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-NoDnsOnNetwork<br /><br />-NoRebootOnCompletion<br /><br />*-SafeModeAdministratorPassword*<br /><br />-SkipAutoConfigureDNS<br /><br />-SkipPreChecks<br /><br />*-Sysvolpath*<br /><br />*-WhatIf*|  
  
> [!NOTE]  
> Das Argument **-DomainNetBIOSName** ist erforderlich, wenn Sie den automatisch generierten 15-stelligen Namen, der auf dem DNS-Domänennamenspräfix basiert, ändern möchten oder wenn der Name mehr als 15 Zeichen umfasst.  
  
Das entsprechende ADDSDeployment-Cmdlet und Argumente für die **Konfiguration der Bereitstellung** im Server-Manager sind:  
  
```powershell  
Install-ADDSForest  
-DomainName <string>  
```  
  
Die entsprechenden ADDSDeployment-Argumente für Domänencontrolleroptionen im Server-Manager sind:  
  
```powershell  
-ForestMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-InstallDNS <{$false | $true}>  
-SafeModeAdministratorPassword <secure string>  
  
```  
  
Die **Install-ADDSForest**-Argumente verwenden dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben sind.  
  
Das Argument **SafeModeAdministratorPassword** funktioniert etwas anders:  
  
-   Wenn dieses Argument *nicht angegeben* wird, fordert das Cmdlet Sie auf, ein maskiertes Kennwort einzugeben und zu bestätigen. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Um z. B. eine neue Gesamtstruktur namens corp.contoso.com zu erstellen und zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert zu werden:  
  
    ```powershell  
    Install-ADDSForest "DomainName corp.contoso.com  
    ```  
  
-   wenn *mit einem Wert* angegeben, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Mithilfe des Cmdlets **Read-Host** können Sie beispielsweise manuell nach einem Kennwort fragen, um den Benutzer zur Eingabe einer sicheren Zeichenfolge aufzufordern:  
  
```powershell  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> Da mit der vorherigen Option das Kennwort nicht bestätigt wird, gehen Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können eine sichere Zeichenfolge auch als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird.  
  
```powershell  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
Zuletzt sollten Sie das verborgene Kennwort in einer Datei speichern und später wiederverwenden, ohne dass jemals das Klartextkennwort erscheint. Zum Beispiel:  
  
```powershell  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartext- oder abgeblendeten Kennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen zusehen, kennen dann das DSRM-Kennwort dieses Domänencontrollers. Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort extrahieren. Mit diesem Wissen können sie sich bei einem Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden, einen Identitätswechsel für den Domänencontroller selbst ausführen und ihre Rechte in einer Active Directory-Gesamtstruktur auf die höchste Stufe heraufstufen. Zusätzliche Schritte mit **System.Security.Cryptography** zur Verschlüsselung der Textdatei werden empfohlen, sind jedoch nicht Teil dieser Anleitung. Generell sollten Sie es vermeiden, Kennwörter zu speichern.  
  
Das ADDSDeployment-Cmdlet bietet eine zusätzliche Option zum Überspringen der automatischen Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Sie können diese Konfiguration nicht überspringen, wenn Sie Server-Manager verwenden. Dieses Argument ist nur relevant, wenn Sie die DNS-Serverrolle vor der Konfiguration des Domänencontrollers installiert haben:  
  
```powershell  
-SkipAutoConfigureDNS  
```  
  
Für die **DomainNetBIOSName** -Operation gelten ebenfalls Sonderregeln:  
  
-   Wenn das **DomainNetBIOSName** -Argument nicht mit einem NetBIOS-Domänennamen angegeben wird und das einteilige Präfix des Domänennamens im **DomainName** -Argument maximal 15 Zeichen lang ist, wird die Heraufstufung mit einem automatisch generierten Namen fortgesetzt.  
  
-   Wenn das **DomainNetBIOSName** -Argument nicht mit einem NetBIOS-Domänennamen angegeben wird und das einteilige Präfix des Domänennamens im **DomainName** -Argument mehr als 15 Zeichen lang ist, schlägt die Heraufstufung fehl.  
  
-   Wenn das **DomainNetBIOSName** -Argument mit einem NetBIOS-Domänennamen mit maximal 15 Zeichen angegeben ist, wird die Heraufstufung mit diesem angegebenen Namen fortgesetzt.  
  
-   Wenn das **DomainNetBIOSName**-Argument mit einem NetBIOS-Domänennamen mit mehr als 15 Zeichen angegeben ist, schlägt die Heraufstufung fehl.  
  
Die entsprechenden ADDSDeployment-Argumente für zusätzliche Optionen im Server-Manager sind:  
  
```powershell  
-domainnetbiosname <string>  
```  
  
Die entsprechenden Server-Manager- **Pfade** für die ADDSDeployment-Cmdlet-Argumente sind:  
  
```powershell  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
  
```  
  
Verwenden Sie das optionale **Whatif** -Argument für das Cmdlet **Install-ADDSForest** , um die Konfigurationsinformationen zu überprüfen. Auf diese Weise können Sie die expliziten und impliziten Werte der Argumente eines Cmdlets anzeigen.  
  
Zum Beispiel:  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSPaths.png)  
  
Bei Verwendung des Server-Managers können Sie die **Voraussetzungsüberprüfung** nicht überspringen. Sie können diese jedoch mit dem folgenden Argument überspringen, wenn Sie das Cmdlet „ADDSDeployment“ verwenden:  
  
```powershell  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft rät davon ab, die Voraussetzungsüberprüfung zu überspringen, da dies zu einer teilweisen Heraufstufung des Domänencontrollers oder zu einer beschädigten AD DS-Gesamtstruktur führen kann.  
  
Ebenso wie beim Server-Manager werden Sie von **Install-ADDSForest** darauf hingewiesen, dass der Server beim Heraufstufen automatisch neu gestartet wird.  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSReboot.png)  
  
![Neue Gesamtstruktur installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallProgress.png)  
  
Mit dem **-force** -Argument oder dem **-confirm:$false** -Argument können Sie den Neustart in allen Windows PowerShell-Cmdlets vom Typ „ADDSDeployment“ automatisch akzeptieren. Verwenden Sie das **-norebootoncompletion**-Argument, um den automatischen Neustart am Ende der Heraufstufung zu verhindern.  
  
> [!WARNING]  
> Es wird davon abgeraten, den Neustart zu verhindern. Der Domänencontroller muss neu gestartet werden, um korrekt zu funktionieren.  
  
## <a name="see-also"></a>Siehe auch  
[Active Directory Domain Services (Technet-Portal)](https://technet.microsoft.com/library/cc770946(WS.10).aspx)  
[Active Directory Domain Services für Windows Server 2008 R2](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
[Active Directory Domain Services für Windows Server 2008](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
[Technische Referenz zu Windows Server (Windows Server 2003)](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
[active Directory-Verwaltungs Center: "Getting Started" (Windows Server 2008 R2) ](https://technet.microsoft.com/library/dd560651(WS.10).aspx)  
[Active Directory Verwaltung mit Windows PowerShell (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd378937(WS.10).aspx)  
[Fragen Sie das Verzeichnis Services-Team (offizieller Microsoft-Blog für kommerziellen technischen Support)](http://blogs.technet.com/b/askds)  
  

