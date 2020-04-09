---
title: Schritt 2 Konfigurieren der Infrastruktur für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: faec70ac-88c0-4b0a-85c7-f0fe21e28257
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b636396ac7102d52ca5700dd2a4a4f81357b1685
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858402"
---
# <a name="step-2-configure-the-multisite-infrastructure"></a>Schritt 2 Konfigurieren der Infrastruktur für mehrere Standorte

>Gilt für: Windows Server 2012 R2, Windows Server 2012

Zum Konfigurieren einer Bereitstellung mit mehreren Standorten sind einige Schritte erforderlich, um die Einstellungen für die Netzwerkinfrastruktur zu ändern. dazu gehören: Konfigurieren zusätzlicher Active Directory Standorte und Domänen Controller, Konfigurieren zusätzlicher Sicherheitsgruppen und Konfigurieren von Gruppenrichtlinie Objekte (GPOs), wenn Sie keine automatisch konfigurierten GPOs verwenden.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|2.1. Zusätzliche Active Directory Standorte konfigurieren|Konfigurieren Sie zusätzliche Active Directory Standorte für die Bereitstellung.|  
|2.2. Zusätzliche Domänen Controller konfigurieren|Konfigurieren Sie zusätzliche Active Directory Domänen Controller nach Bedarf.|  
|2.3. Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen für alle Windows 7-Client Computer.|  
|2.4. Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie zusätzliche Gruppenrichtlinie Objekte nach Bedarf.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit deren Hilfe einige beschriebene Verfahren automatisiert werden können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="21-configure-additional-active-directory-sites"></a><a name="BKMK_ConfigAD"></a>2,1. Zusätzliche Active Directory Standorte konfigurieren  
Alle Einstiegspunkte können sich an einer einzigen Active Directory Site befinden. Daher ist mindestens eine Active Directory Site für die Implementierung von Remote Zugriffs Servern in einer Konfiguration mit mehreren Standorten erforderlich. Verwenden Sie dieses Verfahren, wenn Sie den ersten Active Directory Standort erstellen müssen oder wenn Sie zusätzliche Active Directory Standorte für die Bereitstellung mit mehreren Standorten verwenden möchten. Verwenden Sie das Snap-in Active Directory Sites und Dienste, um neue Standorte im Netzwerk Ihrer Organisation zu erstellen.  

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe "Organisations- **Admins** " in der Gesamtstruktur oder in der Gruppe " **Domänen-Admins** " in der Stamm Domäne der Gesamtstruktur oder einer gleichwertigen Gruppe erforderlich. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

Weitere Informationen finden Sie unter [Hinzufügen einer Site zur](https://technet.microsoft.com/library/cc732761.aspx)Gesamtstruktur.  

### <a name="to-configure-additional-active-directory-sites"></a>So konfigurieren Sie zusätzliche Active Directory Standorte  
  
1.  Klicken Sie auf dem primären Domänen Controller auf **Start**, und klicken Sie dann auf **Active Directory Websites und Dienste**.  
  
2.  Klicken Sie in der Konsole Active Directory Standorte und Dienste in der Konsolen Struktur mit der rechten Maustaste auf **Standorte**, und klicken Sie dann auf **neuer Standort**.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt-Standort** im Feld **Name** einen Namen für den neuen Standort ein.  
  
4.  Klicken Sie unter **Linkname**auf ein Standort Verknüpfungs Objekt, und klicken Sie dann zweimal auf **OK** .  
  
5.  Erweitern Sie in der Konsolen Struktur **Standorte**, klicken Sie mit der rechten Maustaste auf **Subnetze**, und klicken Sie dann auf **Neues Subnetz**.  
  
6.  Geben Sie im Dialogfeld **Neues Objekt-Subnetz** unter **Präfix**das IPv4-oder IPv6-Subnetzpräfix ein, klicken Sie in der Liste **Wählen Sie ein Standort Objekt für dieses Präfix aus** auf die Site, die diesem Subnetz zugeordnet werden soll, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte 5 und 6, bis Sie alle Subnetze erstellt haben, die für die Bereitstellung erforderlich sind.  
  
8.  Schließen Sie Active Directory Websites und Dienste.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
So installieren Sie die Windows-Funktion "Active Directory-Modul für Windows PowerShell":  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
oder fügen Sie das "Active Directory PowerShell-Snap-in" über OptionalFeatures hinzu.  
  
Wenn Sie die folgenden Cmdlets unter Windows 7 oder Windows Server 2008 R2 ausführen, muss das Active Directory PowerShell-Modul importiert werden:  
  
```  
Import-Module ActiveDirectory  
```  
  
So konfigurieren Sie eine Active Directory Site mit dem Namen "Second-Site" unter Verwendung der integrierten DEFAULTIPSITELINK:  
  
```  
New-ADReplicationSite -Name "Second-Site"  
Set-ADReplicationSiteLink -Identity "DEFAULTIPSITELINK" -sitesIncluded @{Add="Second-Site"}  
```  
  
So konfigurieren Sie IPv4-und IPv6-Subnetze für den zweiten Standort:  
  
```  
New-ADReplicationSubnet -Name "10.2.0.0/24" -Site "Second-Site"  
New-ADReplicationSubnet -Name "2001:db8:2::/64" -Site "Second-Site"  
```  
  
## <a name="22-configure-additional-domain-controllers"></a><a name="BKMK_AddDC"></a>2,2. Zusätzliche Domänen Controller konfigurieren  
Zum Konfigurieren einer Bereitstellung mit mehreren Standorten in einer einzelnen Domäne empfiehlt es sich, mindestens einen beschreibbaren Domänen Controller für jeden Standort in der Bereitstellung zu haben.  
  
Um dieses Verfahren auszuführen, müssen Sie mindestens Mitglied der Gruppe "Domänen-Admins" in der Domäne sein, in der der Domänen Controller installiert wird.  
  
Weitere Informationen finden Sie unter [Installieren eines zusätzlichen Domänen Controllers](https://technet.microsoft.com/library/cc733027.aspx).
  
### <a name="to-configure-additional-domain-controllers"></a>So konfigurieren Sie zusätzliche Domänen Controller  
  
1.  Klicken Sie auf dem Server, der als Domänen Controller fungieren soll, in **Server-Manager**auf dem **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **weiter** , um zum Bildschirm für die Server Rollenauswahl zu gelangen.  
  
3.  Wählen Sie auf der Seite **Server Rollen auswählen** die Option **Active Directory Domain Services**aus. Klicken Sie bei entsprechender Aufforderung auf **Features hinzufügen** , und klicken Sie dann dreimal auf **weiter** .  
  
4.  Klicken Sie auf der Seite **Bestätigung** auf **Installieren**.  
  
5.  Wenn die Installation erfolgreich abgeschlossen wurde, klicken Sie auf **Server zu einem Domänen Controller**herauf Stufen.  
  
6.  Klicken Sie im Konfigurations-Assistenten für Active Directory Domain Services auf der Seite **Bereitstellungs Konfiguration** auf **Domänen Controller einer vorhandenen Domäne hinzufügen**.  
  
7.  Geben Sie unter **Domäne**den Domänen Namen ein. beispielsweise Corp.contoso.com.  
  
8.  Klicken Sie unter Geben Sie **die Anmelde Informationen an, um diesen Vorgang auszuführen**, auf **ändern**. Geben Sie im Dialogfeld **Windows-Sicherheit** den Benutzernamen und das Kennwort für ein Konto an, mit dem der zusätzliche Domänen Controller installiert werden kann. Zum Installieren eines zusätzlichen Domänencontrollers müssen Sie ein Mitglied der Gruppe Organisations-Admins oder Domänen-Admins sein. Klicken Sie nach Eingabe der Anmeldeinformationen auf **Weiter**.  
  
9. Gehen Sie auf der Seite **Domänen Controller Optionen** wie folgt vor:  
  
    1.  Nehmen Sie folgende Auswahl vor:  
  
        -   **Domain Name System (DNS)-Server**"diese Option ist standardmäßig ausgewählt, sodass der Domänen Controller als Domain Name System Server (DNS) fungieren kann. Falls der Domänencontroller nicht als DNS-Server verwendet werden soll, können Sie diese Option deaktivieren.  
  
            Wenn die DNS-Server Rolle nicht auf dem PDC-Emulator (primärer Domänen Controller) in der Stamm Domäne der Gesamtstruktur installiert ist, ist die Option zum Installieren des DNS-Servers auf einem zusätzlichen Domänen Controller nicht verfügbar. Um dieses Problem zu umgehen, können Sie die DNS-Server Rolle vor oder nach der AD DS Installation installieren.  
  
            > [!NOTE]  
            > Wenn Sie die Option zum Installieren des DNS-Servers auswählen, erhalten Sie möglicherweise eine Meldung mit dem Hinweis, dass keine DNS-Delegierung für den DNS-Server erstellt werden konnte und dass Sie manuell eine DNS-Delegierung an den DNS-Server erstellen sollten, um eine zuverlässige Namensauflösung sicherzustellen. Wenn Sie einen zusätzlichen Domänen Controller in der Stamm Domäne der Gesamtstruktur oder in einer Struktur Stamm Domäne installieren, müssen Sie keine DNS-Delegierung erstellen. Klicken Sie in diesem Fall auf **Ja** , und ignorieren Sie die Meldung.  
  
        -   **Globaler Katalog (GC)** : diese Option ist standardmäßig ausgewählt. Damit werden dem Domänencontroller die schreibgeschützten Verzeichnispartitionen des globalen Katalogs hinzugefügt. Außerdem wird die Suchfunktion für den globalen Katalog aktiviert.  
  
        -   Schreib geschützter **Domänen Controller (RODC)** : diese Option ist standardmäßig nicht ausgewählt. Der zusätzliche Domänen Controller ist schreibgeschützt. Das heißt, der Domänen Controller wird zu einem RODC.  
  
    2.  Wählen Sie unter **Website Name**einen Standort aus der Liste aus.  
  
    3.  Geben Sie unter **Kennwort** und **Kennwort bestätigen**ein Kennwort für **den Verzeichnisdienst-Wiederherstellungs Modus (Directory Services Restore Mode, DSRM)** ein, und klicken Sie dann auf **weiter**. Dieses Kennwort muss verwendet werden, um AD DS in DSRM für Aufgaben zu starten, die offline ausgeführt werden müssen.  
  
10. Aktivieren Sie auf der Seite **DNS-Optionen** das Kontrollkästchen **DNS-Delegierung aktualisieren** , wenn Sie die DNS-Delegierung während der Rollen Installation aktualisieren möchten, und klicken Sie dann auf **weiter**.  
  
11. Geben Sie auf der Seite **zusätzliche Optionen** die Volumes und Ordner Orte für die Datenbankdatei, die Verzeichnisdienst-Protokolldateien und die Dateien des System Volume (SYSVOL) ein, oder navigieren Sie zu diesen. Geben Sie gegebenenfalls Replikations Optionen an, und klicken Sie dann auf **weiter**.  
  
12. Überprüfen Sie die Installationsoptionen auf der Seite **Optionen prüfen** , und klicken Sie dann auf **weiter**.  
  
13. Klicken Sie nach der Überprüfung der Voraussetzungen auf der Seite Voraussetzungs **Prüfung** auf **Installieren**.  
  
14. Warten Sie, bis der Assistent die Konfiguration abgeschlossen hat, und klicken Sie dann auf **Schließen**.  
  
15. Starten Sie den Computer neu, wenn er nicht automatisch neu gestartet wurde.  
  
## <a name="23-configure-security-groups"></a><a name="BKMK_ConfigSG"></a>2,3. Konfigurieren von Sicherheitsgruppen  
Für eine Bereitstellung mit mehreren Standorten ist eine zusätzliche Sicherheitsgruppe für Windows 7-Client Computer für jeden Einstiegspunkt in der Bereitstellung erforderlich, der den Zugriff auf Windows 7-Client Computer ermöglicht. Wenn mehrere Domänen mit Windows 7-Client Computern vorhanden sind, empfiehlt es sich, in jeder Domäne eine Sicherheitsgruppe für denselben Einstiegspunkt zu erstellen. Alternativ kann eine universelle Sicherheitsgruppe verwendet werden, die die Client Computer aus beiden Domänen enthält. Wenn Sie in einer Umgebung mit zwei Domänen z. b. den Zugriff auf Windows 7-Client Computer in den Einstiegspunkten 1 und 3 zulassen möchten, aber nicht auf Einstiegspunkt 2, dann erstellen Sie zwei neue Sicherheitsgruppen, die die Windows 7-Client Computer für jeden Einstiegspunkt in jedem der Gebiete.  
  
### <a name="to-configure-additional-security-groups"></a>So konfigurieren Sie zusätzliche Sicherheitsgruppen  
  
1.  Klicken Sie auf dem primären Domänen Controller auf **Start**, und klicken Sie dann auf **Active Directory Benutzer und Computer**.  
  
2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Ordner, in dem Sie eine neue Gruppe hinzufügen möchten, z. b. Corp.contoso.com/users. Zeigen Sie auf **Neu**, und klicken Sie dann auf **Gruppe**.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt-Gruppe** unter **Gruppenname**den Namen der neuen Gruppe ein, z. b. Win7_Clients_Entrypoint1.  
  
4.  Klicken Sie unter **Gruppenbereich**auf **universell**, klicken Sie unter **Gruppentyp**auf **Sicherheit**, und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie der neuen Sicherheitsgruppe Computer hinzufügen möchten, doppelklicken Sie auf die Sicherheitsgruppe, und klicken Sie im Dialogfeld **Eigenschaften von < Group_Name >** auf die Registerkarte **Mitglieder** .  
  
6.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
7.  Wählen Sie die Windows 7-Computer aus, die dieser Sicherheitsgruppe hinzugefügt werden sollen, und klicken Sie auf **OK**.  
  
8.  Wiederholen Sie dieses Verfahren, um eine Sicherheitsgruppe für jeden Einstiegspunkt nach Bedarf zu erstellen.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
So installieren Sie die Windows-Funktion "Active Directory-Modul für Windows PowerShell":  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
oder fügen Sie das "Active Directory PowerShell-Snap-in" über OptionalFeatures hinzu.  
  
Wenn Sie die folgenden Cmdlets unter Windows 7 oder Windows Server 2008 R2 ausführen, muss das Active Directory PowerShell-Modul importiert werden:  
  
```  
Import-Module ActiveDirectory  
```  
  
So konfigurieren Sie eine Sicherheitsgruppe mit dem Namen Win7_Clients_Entrypoint1 und zum Hinzufügen eines Client Computers mit dem Namen CLIENT2:  
  
```  
New-ADGroup -GroupScope universal -Name Win7_Clients_Entrypoint1  
Add-ADGroupMember -Identity Win7_Clients_Entrypoint1 -Members CLIENT2$  
```  
  
## <a name="24-configure-gpos"></a><a name="ConfigGPOs"></a>2,4. Konfigurieren der Gruppenrichtlinienobjekte  
Für eine Remote Zugriffs Bereitstellung mit mehreren Standorten sind die folgenden Gruppenrichtlinie Objekte erforderlich:  
  
-   Ein Gruppenrichtlinien Objekt für jeden Einstiegspunkt für den Remote Zugriffs Server.  
  
-   Ein GPO für alle Windows 8-Client Computer für jede Domäne.  
  
-   Ein GPO in jeder Domäne, die Windows 7-Client Computer für jeden Einstiegspunkt enthält, der für die Unterstützung von Windows 7-Clients konfiguriert ist.  
  
    > [!NOTE]  
    > Wenn Sie über keine Windows 7-Client Computer verfügen, müssen Sie keine Gruppenrichtlinien Objekte für Windows 7-Computer erstellen.  
  
Wenn Sie den Remote Zugriff konfigurieren, erstellt der Assistent automatisch die erforderlichen Gruppenrichtlinie Objekte, wenn Sie nicht bereits vorhanden sind. Wenn Sie nicht über die erforderlichen Berechtigungen zum Erstellen von Gruppenrichtlinie Objekten verfügen, müssen Sie vor dem Konfigurieren des Remote Zugriffs erstellt werden. Der DirectAccess-Administrator muss über vollständige Berechtigungen für die Gruppenrichtlinien Objekte verfügen (Bearbeiten und Ändern von Sicherheit + löschen).  
  
> [!IMPORTANT]  
> Nachdem Sie die Gruppenrichtlinien Objekte für den Remote Zugriff manuell erstellt haben, müssen Sie dem Domänen Controller am Active Directory Standort, der dem RAS-Server zugeordnet ist, ausreichend Zeit für die Active Directory-und DFS-Replikation gewähren. Wenn der Remote Zugriff die Gruppenrichtlinie Objekte automatisch erstellt hat, ist keine Wartezeit erforderlich.  
  
Informationen zum Erstellen von Gruppenrichtlinie Objekten finden Sie unter [Erstellen und Bearbeiten eines Gruppenrichtlinie Objekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
### <a name="domain-controller-maintenance-and-downtime"></a><a name="DCMaintandDowntime"></a>Wartung und Ausfall von Domänen Controllern  
Wenn ein Domänen Controller, auf dem der PDC-Emulator ausgeführt wird, oder Domänen Controller, die Server-Gruppenrichtlinien Objekte verwalten, Ausfallzeiten auftreten, ist es nicht möglich, die Konfiguration des Remote Zugriffs zu laden Dies hat keine Auswirkung auf die Client Konnektivität, wenn andere Domänen Controller verfügbar sind.  
  
Wenn Sie die Remote Zugriffs Konfiguration laden oder ändern möchten, können Sie die PDC-Emulatorrolle auf einen anderen Domänen Controller für den Client oder die Anwendungsserver-Gruppenrichtlinien Objekte übertragen. Ändern Sie für Server-Gruppenrichtlinien Objekte die Domänen Controller, die die Server-Gruppenrichtlinien Objekte verwalten.  
  
> [!IMPORTANT]  
> Dieser Vorgang kann nur von einem Domänen Administrator ausgeführt werden. Die Auswirkungen der Änderung des primären Domänen Controllers sind nicht auf den Remote Zugriff beschränkt. Verwenden Sie daher beim Übertragen der PDC-Emulatorrolle Vorsicht.  
  
> [!NOTE]  
> Vergewissern Sie sich vor dem Ändern der Domänen Controller Zuordnung, dass alle GPOs in der Remote Zugriffs Bereitstellung auf allen Domänen Controllern in der Domäne repliziert wurden. Wenn das Gruppenrichtlinien Objekt nicht synchronisiert ist, können nach dem Ändern der Domänen Controller Zuordnung die aktuellen Konfigurationsänderungen verloren gehen. Dies kann zu einer beschädigten Konfiguration führen. Informationen zum Überprüfen der Gruppenrichtlinien Objekt-Synchronisierung finden [Sie unter Überprüfen des Gruppenrichtlinie](https://technet.microsoft.com/library/jj134176.aspx)  
  
#### <a name="to-transfer-the-pdc-emulator-role"></a><a name="TransferPDC"></a>So übertragen Sie die PDC-Emulatorrolle  
  
1.  Geben Sie auf dem **Start** Bildschirm**DSA. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie im linken Bereich der Konsole Active Directory Benutzer und Computer mit der rechten Maustaste auf **Active Directory Benutzer und Computer**, und klicken Sie dann auf **Domänen Controller ändern**. Klicken Sie im Dialogfeld Verzeichnis Server ändern auf **diesen Domänen Controller oder AD LDS Instanz**, klicken Sie in der Liste auf den Domänen Controller, der als neuer Rollen Inhaber verwendet werden soll, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Sie müssen diesen Schritt ausführen, wenn Sie sich nicht auf dem Domänen Controller befinden, an den Sie die Rolle übertragen möchten. Führen Sie diesen Schritt nicht aus, wenn Sie bereits eine Verbindung mit dem Domänen Controller hergestellt haben, an den Sie die Rolle übertragen möchten.  
  
3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Active Directory Benutzer und Computer**, zeigen Sie auf **Alle Tasks**, und klicken Sie dann auf **Betriebs Master**.  
  
4.  Klicken Sie im Dialogfeld Betriebs Master auf die Registerkarte **PDC** , und klicken Sie dann auf **ändern**.  
  
5.  Klicken Sie auf **Ja** , um zu bestätigen, dass Sie die Rolle übertragen möchten, und klicken Sie dann auf **Schließen**.  
  
#### <a name="to-change-the-domain-controller-that-manages-server-gpos"></a><a name="ChangeDC"></a>So ändern Sie den Domänen Controller, der Server-GPOs verwaltet  
  
-   Führen Sie das Windows PowerShell-Cmdlet [Set-daentrypointdc](https://docs.microsoft.com/powershell/module/remoteaccess/set-daentrypointdc) auf dem Remote Zugriffs Server aus, und geben Sie den nicht erreichbaren Domänen Controller Namen für den *existingdc* -Parameter an. Mit diesem Befehl wird die Domänen Controller Zuordnung für die Server-Gruppenrichtlinien Objekte der Einstiegspunkte geändert, die derzeit von diesem Domänen Controller verwaltet werden.
  
    -   Gehen Sie folgendermaßen vor, um den nicht erreichbaren Domänen Controller "DC1.Corp.contoso.com" durch den Domänen Controller "DC2.Corp.contoso.com" zu ersetzen:  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "NewDC 'dc2.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
    -   Führen Sie die folgenden Schritte aus, um den nicht erreichbaren Domänen Controller "DC1.Corp.contoso.com" durch einen Domänen Controller am nächstgelegenen Active Directory Standort zum RAS-Server "da1.Corp.contoso.com" zu ersetzen:  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
### <a name="change-two-or-more-domain-controllers-that-manage-server-gpos"></a><a name="ChangeTwoDCs"></a>Ändern von mindestens zwei Domänen Controllern, die Server-Gruppenrichtlinien Objekte verwalten  
In einer minimalen Anzahl von Fällen sind mindestens zwei Domänen Controller, die Server-Gruppenrichtlinien Objekte verwalten, nicht verfügbar. Wenn dies auftritt, sind weitere Schritte erforderlich, um die Domänen Controller Zuordnung für die Server-Gruppenrichtlinien Objekte zu ändern.  
  
Domänen Controller-Zuordnungs Informationen werden sowohl in der Registrierung der RAS-Server als auch in allen Server-GPOs gespeichert. Im folgenden Beispiel gibt es zwei Einstiegspunkte mit zwei Remote Zugriffs Servern: "da1" in "Entry Point 1" und "da2" in "Entry Point 2". Das Server-GPO von "Einstiegspunkt 1" wird auf dem Domänen Controller "DC1" verwaltet, während das Server-Gruppenrichtlinien Objekt "Einstiegspunkt 2" auf dem Domänen Controller "DC2" verwaltet wird. "DC1" und "DC2" sind nicht verfügbar. Ein Dritter Domänen Controller ist weiterhin in der Domäne "DC3" verfügbar, und die Daten von "DC1" und "DC2" wurden bereits in "DC3" repliziert.  
  
![Konfigurieren der Infrastruktur für mehrere Standorte](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc1.png)  
  
##### <a name="to-change-two-or-more-domain-controllers-that-manage-server-gpos"></a>So ändern Sie mindestens zwei Domänen Controller, die Server-Gruppenrichtlinien Objekte verwalten  
  
1.  Führen Sie den folgenden Befehl aus, um den nicht verfügbaren Domänen Controller "DC2" durch den Domänen Controller "DC3" zu ersetzen:  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    Mit diesem Befehl wird die Domänen Controller Zuordnung für das Server-Gruppenrichtlinien Objekt "Entry Point 2" in der Registrierung von da2 und im Server-Gruppenrichtlinien Objekt "Entry Point 2" aktualisiert. Allerdings wird das Server-Gruppenrichtlinien Objekt "Einstiegspunkt 1" nicht aktualisiert, da der Domänen Controller, der ihn verwaltet, nicht verfügbar ist.  
  
    > [!TIP]  
    > Dieser Befehl verwendet den Continue-Wert für den *ErrorAction* -Parameter, der das Server-GPO "Entry Point 2" aktualisiert, obwohl das Server-Gruppenrichtlinien Objekt "Einstiegspunkt 1" nicht aktualisiert werden konnte.  
  
    Die resultierende Konfiguration ist in der folgenden Abbildung dargestellt.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc2.png)  
  
2.  Führen Sie den folgenden Befehl aus, um den nicht verfügbaren Domänen Controller "DC1" durch den Domänen Controller "DC3" zu ersetzen:  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC1' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    Mit diesem Befehl wird die Domänen Controller Zuordnung für das Server-Gruppenrichtlinien Objekt "Entry Point 1" in der Registrierung von da1 und in den Server-Gruppenrichtlinien Objekten "Entry Point 1" und "Entry Point 2" aktualisiert. Die resultierende Konfiguration ist in der folgenden Abbildung dargestellt.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc3.png)  
  
3.  Um die Domänen Controller Zuordnung für das Server-Gruppenrichtlinien Objekt "Entry Point 2" im Server-Gruppenrichtlinien Objekt "Einstiegspunkt 1" zu synchronisieren, führen Sie den Befehl aus, um "DC2" durch "DC3" zu ersetzen, und geben Sie den Remote Zugriffs Server an, dessen Server-GPO nicht synchronisiert ist, in diesem Fall "da1" für den *Computername* -Parameter  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA1' "ErrorAction Continue  
    ```  
  
    Die endgültige Konfiguration ist in der folgenden Abbildung dargestellt.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssocFinal.png)  
  
### <a name="optimization-of-configuration-distribution"></a><a name="ConfigDistOptimization"></a>Optimierung der Konfigurations Verteilung  
Wenn Sie Konfigurationsänderungen vornehmen, werden die Änderungen erst angewendet, nachdem die Server-Gruppenrichtlinien Objekte an die RAS-Server weitergegeben wurden. Um die Konfigurations Verteilung zu verkürzen, wählt der Remote Zugriff automatisch einen beschreibbaren Domänen Controller aus, der dem RAS- [Server am nächsten](https://technet.microsoft.com/library/cc978016.aspx) liegt, wenn das zugehörige Server-Gruppenrichtlinien Objekt erstellt wird.  
  
In einigen Szenarien kann es erforderlich sein, den Domänen Controller, von dem ein Server-Gruppenrichtlinien Objekt verwaltet wird, manuell zu ändern, um die Konfigurationszeit für die Verteilung zu optimieren:  
  
-   Es waren keine beschreibbaren Domänen Controller an der Active Directory Site eines RAS-Servers zum Zeitpunkt des Hinzufügens als Einstiegspunkt vorhanden. Ein Beschreib barer Domänen Controller wird jetzt der Active Directory Site des RAS-Servers hinzugefügt.  
  
-   Durch eine Änderung der IP-Adresse oder durch Änderungen an Active Directory Standorten und Subnetzen konnte der RAS-Server möglicherweise an einen anderen Active Directory Standort verschoben werden.  
  
-   Die Domänen Controller Zuordnung für einen Einstiegspunkt wurde manuell aufgrund von Wartungsarbeiten auf einem Domänen Controller geändert, und der Domänen Controller ist nun wieder online.  
  
Führen Sie in diesen Szenarien das PowerShell-Cmdlet `Set-DAEntryPointDC` auf dem RAS-Server aus, und geben Sie mit dem Parameter *entrypointname*den Namen des Einstiegs Punkts an, den Sie optimieren möchten. Dies sollten Sie nur tun, nachdem die GPO-Daten des Domänen Controllers, der das Server-GPO derzeit speichert, bereits vollständig auf dem gewünschten neuen Domänen Controller repliziert wurden.  
  
> [!NOTE]  
> Vergewissern Sie sich vor dem Ändern der Domänen Controller Zuordnung, dass alle GPOs in der Remote Zugriffs Bereitstellung auf allen Domänen Controllern in der Domäne repliziert wurden. Wenn das Gruppenrichtlinien Objekt nicht synchronisiert ist, können nach dem Ändern der Domänen Controller Zuordnung die aktuellen Konfigurationsänderungen verloren gehen. Dies kann zu einer beschädigten Konfiguration führen. Informationen zum Überprüfen der Gruppenrichtlinien Objekt-Synchronisierung finden [Sie unter Überprüfen des Gruppenrichtlinie](https://technet.microsoft.com/library/jj134176.aspx)  
  
Führen Sie einen der folgenden Schritte aus, um die Konfigurations Verteilung zu optimieren:  
  
-   Führen Sie den folgenden Befehl aus, um das Server-Gruppenrichtlinien Objekt des Einstiegs Punkts "Einstiegspunkt 1" auf einem Domänen Controller am nächstgelegenen Active Directory Standort zum RAS-Server "da1.Corp.contoso.com" zu verwalten:  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
-   Führen Sie den folgenden Befehl aus, um das Server-Gruppenrichtlinien Objekt des Einstiegs Punkts "Einstiegspunkt 1" auf dem Domänen Controller "DC2.Corp.contoso.com" zu verwalten:  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "NewDC 'dc2.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
    > [!NOTE]  
    > Wenn Sie den einem bestimmten Einstiegspunkt zugeordneten Domänen Controller ändern, müssen Sie einen Remote Zugriffs Server angeben, der Mitglied dieses Einstiegs Punkts für den *Computername* -Parameter ist.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 3: Konfigurieren der Bereitstellung für mehrere Standorte](Step-3-Configure-the-Multisite-Deployment.md)  
-   [Schritt 1: Implementieren einer Remote Zugriffs Bereitstellung für einen einzelnen Server](Step-1-Implement-a-Single-Server-Remote-Access-Deployment.md)  
