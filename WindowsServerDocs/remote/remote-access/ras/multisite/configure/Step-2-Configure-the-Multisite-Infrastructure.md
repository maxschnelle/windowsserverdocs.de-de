---
title: Schritt 2 Konfigurieren der Infrastruktur für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: faec70ac-88c0-4b0a-85c7-f0fe21e28257
ms.author: pashort
author: shortpatti
ms.openlocfilehash: beecef692b2ac01e6cb6c36892fec16e55b08209
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835171"
---
# <a name="step-2-configure-the-multisite-infrastructure"></a>Schritt 2 Konfigurieren der Infrastruktur für mehrere Standorte

>Gilt für: Windows Server 2012 R2, Windows Server 2012

Um eine Bereitstellung für mehrere Standorte zu konfigurieren, es gibt eine Reihe von Schritten erforderlich, um einschließlich Infrastruktur-Netzwerkeinstellungen zu ändern: Zusätzliche Active Directory-Standorte und Domänencontroller zu konfigurieren, konfigurieren die zusätzlichen Sicherheitsgruppen und konfigurieren Gruppenrichtlinienobjekte (GPOs), wenn Sie nicht automatisch verwenden konfiguriert Gruppenrichtlinienobjekte.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|2.1. Zusätzliche Active Directory-Standorte konfigurieren|Konfigurieren Sie zusätzliche Active Directory-Standorte für die Bereitstellung an.|  
|2.2. Konfigurieren Sie zusätzliche Domänencontroller|Konfigurieren Sie nach Bedarf zusätzliche Active Directory-Domänencontroller.|  
|2.3. Konfigurieren von Sicherheitsgruppen|Konfigurieren Sie Sicherheitsgruppen für den Windows 7-Clientcomputern.|  
|2.4. Konfigurieren der Gruppenrichtlinienobjekte|Konfigurieren Sie zusätzliche Group Policy Objects, nach Bedarf.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_ConfigAD"></a>2.1. Zusätzliche Active Directory-Standorte konfigurieren  
Alle Einstiegspunkte können in einer einzelnen Active Directory-Standort befinden. Aus diesem Grund muss sich mindestens eine Active Directory-Standort für die Implementierung der RAS-Server in einer Konfiguration mit mehreren Standorten. Gehen Sie folgendermaßen vor, wenn müssen Sie die erste Active Directory-Standort zu erstellen oder wenn Sie wünschen zusätzliche Active Directory-Standorte für die Bereitstellung für mehrere Standorte verwendet. Verwenden Sie das Active Directory-Standorte und -Dienste-Snap-in zum Erstellen neuer Standorte in Ihrer Organisation "s-Netzwerk.  

Mitgliedschaft in der **Organisations-Admins** Gruppe in der Gesamtstruktur oder die **Domänen-Admins** Gruppe in der Gesamtstruktur-Stammdomäne oder eine entsprechende mindestens ist erforderlich, um dieses Verfahren abzuschließen. Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).  

Weitere Informationen finden Sie unter [Hinzufügen eines Standorts zur Gesamtstruktur](https://technet.microsoft.com/library/cc732761.aspx).  

### <a name="to-configure-additional-active-directory-sites"></a>So konfigurieren Sie zusätzliche Active Directory-Standorte  
  
1.  Klicken Sie auf dem primären Domänencontroller, auf **starten**, und klicken Sie dann auf **Active Directory-Standorte und-Dienste**.  
  
2.  In der Konsole Active Directory-Standorte und-Dienste in der Konsolenstruktur mit der Maustaste **Websites**, und klicken Sie dann auf **neuen Standort**.  
  
3.  Auf der **neues Objekt - Standort** Dialogfeld die **Namen** Geben Sie einen Namen für den neuen Standort.  
  
4.  In **Linkname**, klicken Sie auf ein Standortverknüpfungsobjekt, und klicken Sie dann auf **OK** zweimal.  
  
5.  Erweitern Sie in der Konsolenstruktur **Websites**, mit der rechten Maustaste **Subnetze**, und klicken Sie dann auf **neues Subnetz**.  
  
6.  Auf der **neues Objekt – Subnetz** Dialogfeld **Präfix**, geben Sie die IPv4- oder IPv6-Subnetzpräfix, in der **Standortobjekt für dieses Präfix auswählen** Liste, klicken Sie auf der Website zuordnen mit diesem Subnetz, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte 5 und 6, bis Sie alle Subnetze, die erforderlich sind, in der Bereitstellung erstellt haben.  
  
8.  Schließen Sie die Active Directory-Standorte und Dienste.  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So installieren Sie das Windows-Feature "Active Directory-Modul für Windows PowerShell"  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
oder fügen Sie die "Active Directory PowerShell-Snap-In" über OptionalFeatures.  
  
Wenn die folgenden Cmdlets in Windows 7" oder Windows Server 2008 R2 ausgeführt wird, muss das Active Directory-PowerShell-Modul importiert werden:  
  
```  
Import-Module ActiveDirectory  
```  
  
So konfigurieren Sie Active Directory-Standort mit dem Namen "Zweite-Website" mithilfe der integrierten DEFAULTIPSITELINK:  
  
```  
New-ADReplicationSite -Name "Second-Site"  
Set-ADReplicationSiteLink -Identity "DEFAULTIPSITELINK" -sitesIncluded @{Add="Second-Site"}  
```  
  
So konfigurieren Sie IPv4 und IPv6-Subnetzen für die zweite-Website:  
  
```  
New-ADReplicationSubnet -Name "10.2.0.0/24" -Site "Second-Site"  
New-ADReplicationSubnet -Name "2001:db8:2::/64" -Site "Second-Site"  
```  
  
## <a name="BKMK_AddDC"></a>2.2. Konfigurieren Sie zusätzliche Domänencontroller  
Um eine Bereitstellung für mehrere Standorte in einer einzelnen Domäne konfigurieren zu können, empfiehlt es sich, dass Sie mindestens ein beschreibbarer Domänencontroller für jeden Standort in Ihrer Bereitstellung verfügen.  
  
Zum Ausführen dieser Prozedur mindestens, mit denen Sie Mitglied der Gruppe "Domänen-Admins" in der Domäne in der der Domänencontroller installiert wird.  
  
Weitere Informationen finden Sie unter [Installieren eines zusätzlichen Domänencontrollers](https://technet.microsoft.com/library/cc733027.aspx).
  
### <a name="to-configure-additional-domain-controllers"></a>So konfigurieren Sie zusätzliche Domänencontroller  
  
1.  Auf dem Server, der als Domänencontroller, in fungiert **Server-Manager**auf die **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie auf **Weiter** dreimal, um dem Auswahlbildschirm des Server-Rolle zu erhalten  
  
3.  Auf der **Serverrollen auswählen** Seite **Active Directory Domain Services**. Klicken Sie auf **Features hinzufügen** wenn dazu aufgefordert werden, und klicken Sie dann auf **Weiter** drei Mal.  
  
4.  Klicken Sie auf der Seite **Bestätigung** auf **Installieren**.  
  
5.  Wenn die Installation erfolgreich abgeschlossen wurde, klicken Sie auf **Server zu einem Domänencontroller heraufstufen**.  
  
6.  Die Active Directory-Domäne Konfigurations-Assistenten auf die **Bereitstellungskonfiguration** auf **Domänencontroller vorhandener Domäne hinzufügen**.  
  
7.  In **Domäne**, geben Sie die Domäne Namen, z. B. "corp.contoso.com".  
  
8.  Klicken Sie unter **Geben Sie die Anmeldeinformationen zum Ausführen dieses Vorgangs**, klicken Sie auf **Änderung**. Auf der **Windows Security** Dialogfeld geben den Benutzernamen und das Kennwort für ein Konto, das den zusätzlichen Domänencontroller installieren können. Zum Installieren eines zusätzlichen Domänencontrollers müssen Sie ein Mitglied der Gruppe Organisations-Admins oder Domänen-Admins sein. Klicken Sie nach Eingabe der Anmeldeinformationen auf **Weiter**.  
  
9. Auf der **Domänencontrolleroptionen** Seite, gehen Sie folgendermaßen vor:  
  
    1.  Stellen Sie die folgenden Optionen:  
  
        -   **Domain Name System (DNS) Server**"Diese Option ist standardmäßig aktiviert, damit der Domänencontroller als Domain Name System (DNS)-Server verwendet werden kann. Falls der Domänencontroller nicht als DNS-Server verwendet werden soll, können Sie diese Option deaktivieren.  
  
            Wenn die DNS-Serverrolle nicht auf dem primären Domänencontroller (PDC)-Emulator in der Gesamtstruktur-Stammdomäne installiert ist, ist die Option zum Installieren von DNS-Server auf einen zusätzlichen Domänencontroller nicht verfügbar. Als problemumgehung in diesem Fall können Sie die DNS-Serverrolle vor oder nach der AD DS-Installation installieren.  
  
            > [!NOTE]  
            > Wenn Sie die Option zum Installieren von DNS-Server auswählen, erhalten Sie möglicherweise eine Meldung, die angibt, dass eine DNS-Delegierung für den DNS-Server konnte nicht erstellt werden und Sie eine DNS-Delegierung auf dem DNS-Server, um sicherzustellen, dass zuverlässige namensauflösung manuell erstellen sollen. Wenn Sie einen zusätzlichen Domänencontroller in der Stammdomäne der Gesamtstruktur oder einer Strukturstammdomäne installieren, müssen Sie keinen der DNS-Delegierung erstellen. Klicken Sie in diesem Fall auf **Ja** und die Nachricht ignorieren.  
  
        -   **Globaler Katalog (GC)**"Diese Option ist standardmäßig aktiviert. Damit werden dem Domänencontroller die schreibgeschützten Verzeichnispartitionen des globalen Katalogs hinzugefügt. Außerdem wird die Suchfunktion für den globalen Katalog aktiviert.  
  
        -   **Read-only-Domänencontroller (RODC)**"Diese Option ist standardmäßig nicht aktiviert. Es ist den zusätzliche Domänencontroller schreibgeschützt; Dabei handelt es sich sie dem Domänencontroller einen RODC.  
  
    2.  In **Standortname**, wählen Sie einen Standort aus der Liste.  
  
    3.  Klicken Sie unter **Geben Sie das Verzeichnis Verzeichnisdienst-Wiederherstellungsmodus (DSRM) Kennwort**im **Kennwort** und **Bestätigungskennwort**, ein sicheres Kennwort zweimal eingeben, und klicken Sie dann auf  **Nächste**. Dieses Kennwort muss verwendet werden, um AD DS im Verzeichnisdienst-Wiederherstellungsmodus für Aufgaben zu starten, die offline ausgeführt werden muss.  
  
10. Auf der **DNS-Optionen** Seite die **Aktualisieren von DNS-Delegierung** Kontrollkästchen, wenn Sie verwenden möchten, aktualisieren DNS-Delegierung bei der Rolleninstallation, und klicken Sie dann auf **Weiter**.  
  
11. Auf der **zusätzliche Optionen** Seite geben oder die Volume und URLs für die Datenbankdatei, die Protokolldateien des Directory-Dienst und die Systemdateien für das Systemvolume (SYSVOL). Geben Sie Optionen für die Replikation nach Bedarf aus, und klicken Sie dann auf **Weiter**.  
  
12. Auf der **Optionen prüfen** Seite überprüfen Sie die Installationsoptionen, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **Voraussetzungsüberprüfung** Seite, nachdem die erforderlichen Komponenten überprüft wurden, klicken Sie auf **installieren**.  
  
14. Warten Sie, bis der Assistent die Konfiguration abgeschlossen ist, und klicken Sie dann auf **schließen**.  
  
15. Starten Sie den Computer neu, wenn Sie nicht automatisch neu gestartet haben.  
  
## <a name="BKMK_ConfigSG"></a>2.3. Konfigurieren von Sicherheitsgruppen  
Eine Bereitstellung für mehrere Standorte erfordert eine weitere Sicherheitsgruppe für Windows 7-Clientcomputer für jeden Einstiegspunkt in der Bereitstellung, die Zugriff auf Windows 7-Clientcomputern zulässt. Wenn mehrere Domänen, die mit Windows 7-Clientcomputer vorhanden sind, wird es empfohlen, dass es so erstellen eine Sicherheitsgruppe in den einzelnen Domänen für den gleichen Einstiegspunkt. Alternativ kann eine universelle Sicherheitsgruppe, die mit den Clientcomputern, die von beiden Domänen verwendet werden. Z. B. in einer Umgebung mit zwei Domänen, wenn Sie möchten zulassen des Zugriffs auf Windows 7-Clientcomputer in Einstiegspunkte 1 und 3, weisen Sie aber nicht im Eintrag 2, klicken Sie dann zwei neue Gruppen erstellen, enthält die Windows 7-Clientcomputer für jeden Einstiegspunkt in den einzelnen der  Domänen.  
  
### <a name="to-configure-additional-security-groups"></a>So konfigurieren Sie die zusätzlichen Sicherheitsgruppen  
  
1.  Klicken Sie auf dem primären Domänencontroller, auf **starten**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**.  
  
2.  Klicken Sie in der Konsolenstruktur den Ordner, in dem Sie eine neue Gruppe ein, z. B. corp.contoso.com/Users hinzufügen möchten. Zeigen Sie auf **Neu**, und klicken Sie dann auf **Gruppe**.  
  
3.  Auf der **neues Objekt – Gruppe** Dialogfeld **Gruppenname**, geben Sie den Namen der neuen Gruppe, z. B. Win7_Clients_Entrypoint1.  
  
4.  Klicken Sie unter **Gruppenbereich**, klicken Sie auf **universelle**unter **Gruppentyp**, klicken Sie auf **Sicherheit**, und klicken Sie dann auf **OK**.  
  
5.  Um die neue Sicherheitsgruppe Computer hinzuzufügen, doppelklicken Sie auf die Sicherheitsgruppe, und klicken Sie auf die **< Gruppenname > Eigenschaften** im Dialogfeld klicken Sie auf die **Mitglieder** Registerkarte.  
  
6.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
7.  Wählen Sie die Windows 7-Computer, um dieser Sicherheitsgruppe hinzufügen, und klicken Sie dann auf **OK**.  
  
8.  Wiederholen Sie dieses Verfahren, um eine Sicherheitsgruppe für jeden Einstiegspunkt nach Bedarf erstellen.  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So installieren Sie das Windows-Feature "Active Directory-Modul für Windows PowerShell"  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
oder fügen Sie die "Active Directory PowerShell-Snap-In" über OptionalFeatures.  
  
Wenn die folgenden Cmdlets in Windows 7" oder Windows Server 2008 R2 ausgeführt wird, muss das Active Directory-PowerShell-Modul importiert werden:  
  
```  
Import-Module ActiveDirectory  
```  
  
So konfigurieren Sie eine Sicherheitsgruppe namens Win7_Clients_Entrypoint1 und Hinzufügen eines Clientcomputers mit dem Namen CLIENT2:  
  
```  
New-ADGroup -GroupScope universal -Name Win7_Clients_Entrypoint1  
Add-ADGroupMember -Identity Win7_Clients_Entrypoint1 -Members CLIENT2$  
```  
  
## <a name="ConfigGPOs"></a>2.4. Konfigurieren der Gruppenrichtlinienobjekte  
Eine Bereitstellung des Remotezugriffs für mehrere Standorte erfordert die folgenden Gruppenrichtlinienobjekte:  
  
-   Ein Gruppenrichtlinienobjekt für jeden Einstiegspunkt für den RAS-Server.  
  
-   Ein Gruppenrichtlinienobjekt für alle Windows 8-Clientcomputern für jede Domäne.  
  
-   Ein Gruppenrichtlinienobjekt in jeder Domäne, die Windows 7-Clientcomputer enthält, für jeden Einstiegspunkt zur Unterstützung von Windows 7-Clients konfiguriert werden soll.  
  
    > [!NOTE]  
    > Wenn Sie keine Windows 7-Clientcomputer verfügen, müssen Sie keine Gruppenrichtlinienobjekte für Windows 7-Computer zu erstellen.  
  
Wenn Sie Remotezugriff konfigurieren, erstellt der Assistent automatisch die erforderlichen Gruppenrichtlinienobjekte. Wenn sie nicht "t ist bereits vorhanden. Wenn Sie nicht über die erforderlichen Berechtigungen zum Erstellen von Gruppenrichtlinienobjekten verfügen, müssen sie vor dem Konfigurieren des Remotezugriffs erstellt werden. Der DirectAccess-Administrator muss über vollständige Berechtigungen in den Gruppenrichtlinienobjekten verfügen (bearbeiten und Ändern der Sicherheit + ENTF).  
  
> [!IMPORTANT]  
> Nach dem manuellen Erstellen der Gruppenrichtlinienobjekte für den Remotezugriff auf lassen Sie genügend Zeit für Active Directory und DFS-Replikation mit dem Domänencontroller in Active Directory-Standort, der mit dem RAS-Server zugeordnet ist. Wenn der Remotezugriff automatisch die Gruppenrichtlinienobjekte erstellt, ist keine Wartezeit erforderlich.  
  
Group Policy Objects erstellen zu können, finden Sie unter [erstellen und Bearbeiten eines Gruppenrichtlinienobjekts](https://technet.microsoft.com/library/cc754740.aspx).  
  
### <a name="DCMaintandDowntime"></a>Wartung der Domänencontroller und downtime  
Wenn ein Domänencontroller, der als PDC-Emulator oder Domänencontroller, die Verwaltung von Server-GPOs Ausfallzeiten auftreten, ist es nicht möglich, zu laden, oder ändern die Konfiguration des Remotezugriffs. Dies betrifft nicht-Clientkonnektivität, wenn andere Domänencontroller verfügbar sind.  
  
Zum Laden oder die RAS-Konfiguration ändern, können Sie die PDC-Emulatorrolle auf einem anderen Domänencontroller für die Client- oder Anwendungscode Gruppenrichtlinienobjekte Servers übertragen; Ändern Sie für Gruppenrichtlinienobjekte des Servers die Domänencontrollern, die die Gruppenrichtlinienobjekte des Servers zu verwalten.  
  
> [!IMPORTANT]  
> Dieser Vorgang kann nur von einem Domänenadministrator ausgeführt werden. Die Auswirkungen einer Änderung des primäre Domänencontrollers ist nicht mit Remote Access beschränkt; daher vorsichtig, wenn es sich bei die PDC-Emulatorrolle übertragen.  
  
> [!NOTE]  
> Vor dem Ändern von Domain-Controller-Zuordnung, stellen Sie sicher, dass alle GPOs in der Bereitstellung des Remotezugriffs auf alle Domänencontroller in der Domäne repliziert wurden. Wenn das Gruppenrichtlinienobjekt nicht synchronisiert ist, verloren Änderungen an der aktuellen Konfiguration nach dem Ändern der Domäne-Controller-Zuordnung, was zu einer fehlerhaften Konfiguration führen kann. Um die GPO-Synchronisierung zu überprüfen, finden Sie unter [überprüfen Gruppenrichtlinieninfrastruktur-Status](https://technet.microsoft.com/library/jj134176.aspx).  
  
#### <a name="TransferPDC"></a>Übertragen der PDC-Emulatorrolle  
  
1.  Auf der **starten** geben**dsa.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie im linken Bereich der Konsole Active Directory-Benutzer und-Computer mit der Maustaste **Active Directory-Benutzer und-Computer**, und klicken Sie dann auf **Domänencontroller ändern**. Klicken Sie auf das Dialogfeld Änderung Verzeichnisserver auf **dieser Domänencontroller oder AD LDS-Instanz**in die Liste, klicken Sie auf dem Domänencontroller, die die Funktion übernehmen, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Sie müssen diesen Schritt ausführen, wenn Sie nicht auf dem Domänencontroller sind, die um die Rolle nicht übertragen werden soll. Führen Sie diesen Schritt nicht aus, wenn Sie bereits mit dem Domänencontroller verbunden sind, die um die Rolle nicht übertragen werden soll.  
  
3.  In der Konsolenstruktur mit der Maustaste **Active Directory-Benutzer und-Computer**, zeigen Sie auf **alle Aufgaben**, und klicken Sie dann auf **Betriebsmaster**.  
  
4.  Klicken Sie auf das Dialogfeld Betriebsmaster, auf die **PDC** Registerkarte, und klicken Sie dann auf **Änderung**.  
  
5.  Klicken Sie auf **Ja** zu bestätigen, dass Sie verwenden möchten, übertragen die Rolle, und klicken Sie dann auf **schließen**.  
  
#### <a name="ChangeDC"></a>Zum Ändern des Domänencontrollers verwaltet, die Server-GPOs  
  
-   Führen Sie das Windows PowerShell-Cmdlet `HYPERLINK "https://technet.microsoft.com/library/hh918412.aspx" Set-DAEntryPointDC` auf dem RAS-Server, und geben Sie den Namen des Domänencontrollers nicht erreichbar ist für die *ExistingDC* Parameter. Dieser Befehl ändert die Domain Controller-Zuordnung für die Gruppenrichtlinienobjekte des Servers der Einstiegspunkte, die derzeit von diesem Domänencontroller verwaltet werden.  
  
    -   Führen Sie folgende Schritte aus, um den Domänencontroller nicht erreichbar "dc1.corp.contoso.com" mit dem Domänencontroller "dc2.corp.contoso.com" zu ersetzen:  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "NewDC 'dc2.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
    -   Führen Sie folgende Schritte aus, um den Domänencontroller nicht erreichbar "dc1.corp.contoso.com" mit einem Domänencontroller in der nächstgelegenen Active Directory-Standort, an den RAS-Server "DA1.corp.contoso.com" zu ersetzen:  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
### <a name="ChangeTwoDCs"></a>Ändern Sie mindestens zwei Domänencontroller, auf denen Server-GPOs verwalten  
In einer minimalen Anzahl von Fällen sind mindestens zwei Domänencontroller, auf denen Server-GPOs zu verwalten, nicht verfügbar. In diesem Fall sind weitere Schritte erforderlich, um die Domäne-Controller-Zuordnung für die Gruppenrichtlinienobjekte des Servers zu ändern.  
  
Informationen zur Zuordnung von Domain Controller ist sowohl in der Registrierung des RAS-Server als auch in der alle Server-GPOs gespeichert. Im folgenden Beispiel stehen zwei Einstiegspunkte mit zwei RAS-Server, "DA1" in "1" und "DA2" Entry point-in "Einstiegspunkt 2". Das Server-Gruppenrichtlinienobjekt "Einstiegspunkt 1" wird verwaltet, auf dem Domänencontroller "DC1", während sich der Server-Gruppenrichtlinienobjekt von "Einstiegspunkt 2" auf dem Domänencontroller "DC2" verwaltet wird. Sowohl "DC1" und "DC2" sind nicht verfügbar. Ein drittes Domänencontrollers weiterhin verfügbar in der Domäne "DC3", und die Daten aus "DC1" und "DC2" wurde bereits auf "DC3" repliziert.  
  
![Konfigurieren der Infrastruktur für mehrere Standorte](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc1.png)  
  
##### <a name="to-change-two-or-more-domain-controllers-that-manage-server-gpos"></a>So ändern Sie mindestens zwei Domänencontroller, die Server-GPOs verwalten  
  
1.  Führen Sie den folgenden Befehl, um den Domänencontroller nicht verfügbar "DC2" mit dem Domänencontroller "DC3" zu ersetzen:  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    Dieser Befehl aktualisiert die Domain Controller-Zuordnung für das "Einstiegspunkt" 2 "-Server-GPO in der Registrierung DA2 und auf dem Server"Einstiegspunkt 2"GPO selbst; Es ist jedoch nicht "Einstiegspunkt 1" Server-Gruppenrichtlinienobjekts aktualisiert werden, weil der Domänencontroller, der er verwaltet nicht verfügbar ist.  
  
    > [!TIP]  
    > Dieser Befehl verwendet den Wert "Fortfahren" für die *ErrorAction* -Parameter, der das "Einstiegspunkt" 2 "-Server-GPO trotz des Fehlers beim Aktualisieren von"Punkt 1-Eintrag"Server-Gruppenrichtlinienobjekt aktualisiert.  
  
    Die resultierende Konfiguration ist in der folgenden Abbildung dargestellt.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc2.png)  
  
2.  Führen Sie den folgenden Befehl, um den Domänencontroller nicht verfügbar "DC1" mit dem Domänencontroller "DC3" zu ersetzen:  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC1' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    Dieser Befehl aktualisiert die Zuordnung des Domäne-Controller für Gruppenrichtlinienobjekte für die Server-Gruppenrichtlinienobjekt in der Registrierung von da1 aufgelöst und in der "Einstiegspunkt 1" und "Einstiegspunkt 2"-Servers "Einstiegspunkt 1". Die resultierende Konfiguration ist in der folgenden Abbildung dargestellt.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc3.png)  
  
3.  Synchronisieren Sie die Domäne-Controller-Zuordnung für das "Einstiegspunkt" 2 "-Server-Gruppenrichtlinienobjekt auf dem Server"Einstiegspunkt 1"Gruppenrichtlinienobjekt, und führen Sie den Befehl"DC2"mit"DC3"zu ersetzen, und geben Sie den RAS-Server, dessen Server-Gruppenrichtlinienobjekt nicht, in diesem Fall synchronisiert ist"DA1", für die  *ComputerName* Parameter.  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA1' "ErrorAction Continue  
    ```  
  
    Die endgültige Konfiguration ist in der folgenden Abbildung dargestellt.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssocFinal.png)  
  
### <a name="ConfigDistOptimization"></a>Optimierung der konfigurationsverteilung  
Wenn Sie Änderungen an der Konfiguration vornehmen, werden die Änderungen übernommen, nur nach dem Server-GPOs werden an den RAS-Server weitergegeben. Um die Konfigurationszeit für die Verteilung zu reduzieren, wählt Remotezugriff automatisch einen beschreibbaren Domänencontroller der Link ist "https://technet.microsoft.com/library/cc978016.aspx" am nächsten an den RAS-Server beim die Server-Gruppenrichtlinienobjekt zu erstellen.  
  
In einigen Szenarien kann es erforderlich, auf den Domänencontroller manuell zu ändern, der einen Server-Gruppenrichtlinienobjekt verwaltet wird, um die Konfigurationszeit für die Verteilung zu optimieren:  
  
-   Gab es keine beschreibbaren Domänencontroller im Active Directory-Standort des RAS-Server zum Zeitpunkt der als Einstiegspunkt hinzufügen. Ein beschreibbarer Domänencontroller wird nun an der Active Directory-Standort des RAS-Servers hinzugefügt wird.  
  
-   Eine Änderung der IP-Adresse oder eine Änderung für Active Directory-Standorte und Subnetze kann RAS-Servers zu einem anderen Active Directory-Standort verschoben.  
  
-   Die Domäne-Controller-Zuordnung als Einstiegspunkt wurde aufgrund von Wartungsarbeiten auf einem Domänencontroller manuell geändert, und jetzt der Domänencontroller wieder online ist.  
  
Führen Sie in diesen Szenarien wird die PowerShell-Cmdlet `Set-DAEntryPointDC` auf dem RAS-Server, und geben Sie den Namen des Einstiegspunkts zu optimieren, mit dem Parameter *EntryPointName*. Sie sollten dies tun erst nach der GPO-Daten auf dem Domänencontroller speichert aktuell auf den Server, die Gruppenrichtlinienobjekt bereits vollständig auf den gewünschten neuen Domänencontroller repliziert wurde.  
  
> [!NOTE]  
> Vor dem Ändern von Domain-Controller-Zuordnung, stellen Sie sicher, dass alle GPOs in der Bereitstellung des Remotezugriffs auf alle Domänencontroller in der Domäne repliziert wurden. Wenn das Gruppenrichtlinienobjekt nicht synchronisiert ist, verloren Änderungen an der aktuellen Konfiguration nach dem Ändern der Domäne-Controller-Zuordnung, was zu einer fehlerhaften Konfiguration führen kann. Um die GPO-Synchronisierung zu überprüfen, finden Sie unter [überprüfen Gruppenrichtlinieninfrastruktur-Status](https://technet.microsoft.com/library/jj134176.aspx).  
  
Führen Sie eine der folgenden Schritte aus, um die Konfigurationszeit für die Verteilung zu optimieren:  
  
-   Zum Verwalten des Servers GPO Eintrags zeigen "Einstiegspunkt 1" auf einem Domänencontroller in der nächstgelegenen Active Directory-Standort an den RAS-Server "DA1.corp.contoso.com", führen Sie den folgenden Befehl:  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
-   Zum Verwalten des Servers GPO Eintrags zeigen "Einstiegspunkt 1", auf dem Domain Controller "dc2.corp.contoso.com", führen Sie den folgenden Befehl:  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "NewDC 'dc2.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
    > [!NOTE]  
    > Wenn der Domänencontroller, die einem bestimmten Einstiegspunkt zugeordnet zu ändern, müssen Sie angeben, dass RAS-Server, der ein Mitglied dieser Einstiegspunkt für die *ComputerName* Parameter.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 3: Konfigurieren Sie die Bereitstellung für mehrere Standorte](Step-3-Configure-the-Multisite-Deployment.md)  
-   [Schritt 1: Implementieren Sie einen Einzelserver-Bereitstellung des Remotezugriffs](Step-1-Implement-a-Single-Server-Remote-Access-Deployment.md)  

