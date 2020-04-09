---
title: Einrichten von Hosts für die Live Migration ohne Failoverclustering
description: Enthält Anweisungen zum Einrichten einer Live Migration in einer nicht geclusterten Umgebung.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: b5e3c405-cb76-4ff2-8042-c2284448c435
author: kbdazure
ms.author: kathydav
ms.date: 9/30/2016
ms.openlocfilehash: 2c2f671bf59e95de2604c91944fab3d65f82410e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860883"
---
# <a name="set-up-hosts-for-live-migration-without-failover-clustering"></a>Einrichten von Hosts für die Live Migration ohne Failoverclustering

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

In diesem Artikel erfahren Sie, wie Sie Hosts einrichten, die nicht gruppiert sind, damit Sie Live Migrationen zwischen Ihnen ausführen können. Verwenden Sie diese Anweisungen, wenn Sie bei der Installation von Hyper-V keine Live Migration eingerichtet haben, oder wenn Sie die Einstellungen ändern möchten. Verwenden Sie zum Einrichten von gruppierten Hosts die Tools für Failoverclustering.

## <a name="requirements-for-setting-up-live-migration"></a>Anforderungen für die Einrichtung einer Live Migration

Um nicht gruppierte Hosts für die Live Migration einzurichten, benötigen Sie Folgendes:

-  Ein Benutzerkonto mit der Berechtigung zum Ausführen der verschiedenen Schritte. Die Mitgliedschaft in der lokalen Hyper-V-Administrator Gruppe oder der Gruppe "Administratoren" auf dem Quell-und dem Zielcomputer erfüllt diese Anforderung, es sei denn, Sie konfigurieren die eingeschränkte Delegierung. Die Mitgliedschaft in der Gruppe Domänen Administratoren ist erforderlich, um die eingeschränkte Delegierung zu konfigurieren.

- Die Hyper-V-Rolle in Windows Server 2016 oder Windows Server 2012 R2, die auf dem Quell-und dem Zielserver installiert ist. Sie können eine Live Migration zwischen Hosts ausführen, auf denen Windows Server 2016 und Windows Server 2012 R2 ausgeführt wird, wenn der virtuelle Computer mindestens Version 5 ist. <br>Anweisungen zur Versions Aktualisierung finden Sie unter [Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server 2016](Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Installationsanweisungen finden Sie unter [Installieren der Hyper-V-Rolle unter Windows Server](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).

- Quell-und Zielcomputer, die entweder zur gleichen Active Directory Domäne gehören oder zu Domänen gehören, die einander vertrauen.
- Die Hyper-V-Verwaltungs Tools, die auf einem Computer installiert sind, auf dem Windows Server 2016 oder Windows 10 ausgeführt wird, es sei denn, die Tools sind auf dem Quell-oder Ziel Server installiert, und Sie führen die Tools vom Server aus.

## <a name="consider-options-for-authentication-and-networking"></a>Optionen für Authentifizierung und Netzwerk

Beachten Sie, wie Sie Folgendes einrichten möchten:

-  **Authentifizierung**: welches Protokoll wird verwendet, um den Datenverkehr für die Live Migration zwischen den Quell-und Ziel Servern zu authentifizieren? Die Auswahl bestimmt, ob Sie sich beim Quell Server anmelden müssen, bevor Sie eine Live Migration starten:
   - Mithilfe von Kerberos können Sie sich nicht beim Server anmelden, sondern müssen die eingeschränkte Delegierung einrichten. Weitere Informationen finden Sie weiter unten.
   - Mit "kredssp" können Sie die Konfiguration der eingeschränkten Delegierung vermeiden. Sie müssen sich jedoch beim Quell Server anmelden. Hierzu können Sie eine lokale Konsolen Sitzung, eine Remotedesktop Sitzung oder eine Windows PowerShell-Remote Sitzung verwenden.

      Für "kredspp" ist eine Anmeldung in Situationen erforderlich, die möglicherweise nicht offensichtlich sind. Wenn Sie sich beispielsweise bei TestServer01 anmelden, um eine virtuelle Maschine zu Bezeichnung testserver02 zu verschieben, und die virtuelle Maschine anschließend wieder in TestServer01 verschieben möchten, müssen Sie sich bei Bezeichnung testserver02 anmelden, bevor Sie versuchen, die virtuelle Maschine zurück auf TestServer01 zu verschieben. Wenn Sie dies nicht tun, schlägt der Authentifizierungs Versuch fehl, es tritt ein Fehler auf, und die folgende Meldung wird angezeigt:

      "Fehler beim Migrations Vorgang für den virtuellen Computer bei der Migrations Quelle.
      Fehler beim Herstellen einer Verbindung mit dem Host *Computernamen*: im Sicherheitspaket 0x8009030E sind keine Anmelde Informationen verfügbar. "

-   **Leistung**: ist es sinnvoll, Leistungsoptionen zu konfigurieren? Diese Optionen können die Netzwerk-und CPU-Auslastung reduzieren und die Live Migrationen schneller machen. Stellen Sie Ihre Anforderungen und ihre Infrastruktur in Erwägung, und testen Sie verschiedene Konfigurationen, um Ihnen die Entscheidung zu erleichtern. Die Optionen werden am Ende von Schritt 2 beschrieben.

-  **Netzwerk Präferenz**: lässt Sie Live Migration-Datenverkehr über ein beliebiges verfügbares Netzwerk zu, oder isolieren Sie den Datenverkehr für bestimmte Netzwerke? Als bewährte Sicherheitsmethode wird empfohlen, den Datenverkehr auf vertrauenswürdige, private Netzwerken zu isolieren, da der Datenverkehr für die Livemigration beim Senden über das Netzwerk nicht verschlüsselt wird. Die Netzwerkisolation kann über ein physisch isoliertes Netzwerk oder über eine andere vertrauenswürdige Netzwerktechnologie, z. B. VLANs, erreicht werden.

## <a name="step-1-configure-constrained-delegation-optional"></a><a name="BKMK_Step1"></a>Schritt 1: Konfigurieren der eingeschränkten Delegierung (optional)
Wenn Sie sich für die Verwendung von Kerberos zum Authentifizieren des Datenverkehrs für die Live Migration entschieden haben, konfigurieren Sie die eingeschränkte Delegierung mithilfe eines Kontos, das Mitglied der Gruppe Domänen Administratoren ist.

### <a name="use-the-users-and-computers-snap-in-to-configure-constrained-delegation"></a>Verwenden des Snap-Ins "Benutzer und Computer" zum Konfigurieren der eingeschränkten Delegierung

1.  Öffnen Sie das Snap-In %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;. (Wählen Sie unter Server-Manager den Server aus, wenn er nicht ausgewählt ist **, klicken Sie** auf Extras >> **Active Directory Benutzer und Computer**).

2.  Wählen Sie im Navigationsbereich von **Active Directory Benutzer und Computer**die Domäne aus, und doppelklicken Sie auf den Ordner **Computer** .

3.  Klicken Sie im Ordner **Computer** mit der rechten Maustaste auf das Computer Konto des Quell Servers, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie in **Eigenschaften**auf die Registerkarte **Delegierung** .

5.  Wählen Sie auf der Registerkarte Delegierung die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen aus** , und wählen Sie dann **beliebiges Authentifizierungsprotokoll verwenden**aus.

6.  Klicken Sie auf **Hinzufügen**.

7.  Klicken Sie unter **Dienste hinzufügen**auf **Benutzer oder Computer**.

8.  Geben **Sie in Benutzer oder Computer auswählen**den Namen des Zielservers ein. Klicken Sie auf **Namen überprüfen** , um Sie zu überprüfen, und klicken Sie auf **OK**

9. Führen Sie in der Liste der verfügbaren Dienste unter **Dienste hinzufügen**die folgenden Schritte aus, und klicken Sie dann auf **OK**:

    -   Wenn Sie den Speicher des virtuellen Computers entfernen möchten, wählen Sie **cifs** aus. Dies ist erforderlich, wenn Sie den Speicher zusammen mit dem virtuellen Computer verschieben möchten, und wenn Sie nur den Speicher eines virtuellen Computers verschieben möchten. Wenn der Server für die Verwendung des SMB-Speichers für Hyper-V konfiguriert ist, wurde diese Auswahl bereits getroffen.

    -   Wenn Sie virtuelle Computer verschieben möchten, wählen Sie den **Migrationsdienst für virtuelles System von Microsoft** aus.

10. Stellen Sie auf der Registerkarte **Delegierung** des Dialogfelds %%amp;quot;Eigenschaften%%amp;quot; sicher, dass die von Ihnen im vorherigen Schritt ausgewählten Dienste als Dienste aufgelistet sind, für die der Zielcomputer delegierte Anmeldeinformationen bereitstellen kann. Klicken Sie auf **OK**.

11. Wählen Sie im Ordner **Computers** das Computerkonto des Zielservers aus, und wiederholen Sie den Prozess. Vergewissern Sie sich, dass Sie im Dialogfeld **Benutzer oder Computer auswählen** den Namen des Quellservers angegeben haben.

Die Konfigurationsänderungen treten in Kraft, nachdem die beiden folgenden Aktionen durchgeführt wurden:

  -  Die Änderungen werden auf die Domänen Controller repliziert, bei denen die Server, auf denen Hyper-V ausgeführt wird, angemeldet sind.
  -  Der Domänen Controller gibt ein neues Kerberos-Ticket aus.

## <a name="step-2-set-up-the-source-and-destination-computers-for-live-migration"></a><a name="BKMK_Step2"></a>Schritt 2: Einrichten der Quell-und Zielcomputer für die Live Migration
Dieser Schritt umfasst die Auswahl von Optionen für die Authentifizierung und das Netzwerk. Als bewährte Sicherheitsmaßnahme empfiehlt es sich, bestimmte Netzwerke auszuwählen, die für den Datenverkehr für die Live Migration verwendet werden sollen, wie oben erläutert. Außerdem wird in diesem Schritt gezeigt, wie Sie die Option Leistung auswählen.

### <a name="use-hyper-v-manager-to-set-up-the-source-and-destination-computers-for-live-migration"></a>Verwenden des Hyper-V-Managers zum Einrichten der Quell-und Zielcomputer für die Live Migration

1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie** in Server-Manager auf Extras >>**Hyper-V-Manager**.)

2.  Wählen Sie im Navigationsbereich einen der Server aus. (Falls nicht aufgeführt, klicken Sie mit der rechten Maustaste auf **Hyper-V-Manager**, klicken Sie auf **Verbindung mit Server herstellen**, geben Sie den Servernamen ein, und klicken Sie auf **OK** Wiederholen Sie den Vorgang, um weitere Server hinzuzufügen.

3.  Klicken Sie im Bereich **Aktion** auf **Hyper-V-Einstellungen** >>**Live Migrationen**.

4.  Aktivieren Sie im Bereich **Livemigrationen** die Option **Ein- und ausgehende Livemigrationen ermöglichen**.

5.  Geben Sie unter **gleichzeitige Live Migrationen**eine andere Zahl an, wenn Sie nicht den Standardwert von 2 verwenden möchten.

6.  Wenn spezielle Netzwerkverbindungen den Datenverkehr für die Livemigration akzeptieren sollen, klicken Sie unter **Eingehende Livemigrationen** auf **Hinzufügen**, um die IP-Adressinformationen einzugeben. Klicken Sie anderenfalls auf **Beliebiges Netzwerk für Livemigration verwenden**. Klicken Sie auf **OK**.

7.  Um die Kerberos-und Leistungsoptionen auszuwählen, erweitern Sie **Live Migrationen** , und wählen Sie dann **Erweiterte Funktionen**aus.

    - Wenn Sie die eingeschränkte Delegierung konfiguriert haben, wählen Sie unter **Authentifizierungsprotokoll**die Option **Kerberos**aus.
    - Überprüfen Sie unter **Leistungsoptionen**die Details, und wählen Sie eine andere Option aus, wenn Sie für Ihre Umgebung geeignet ist.

8. Klicken Sie auf **OK**.

9. Wählen Sie im Hyper-V-Manager den anderen Server aus, und wiederholen Sie die Schritte.

### <a name="use-windows-powershell-to-set-up-the-source-and-destination-computers-for-live-migration"></a>Verwenden von Windows PowerShell zum Einrichten der Quell-und Zielcomputer für die Live Migration

Zum Konfigurieren der Live Migration auf nicht gruppierten Hosts sind drei Cmdlets verfügbar: " [enable-vmmigration](https://technet.microsoft.com/library/hh848544.aspx)", " [Set-vmmigrationnetwork](https://technet.microsoft.com/library/hh848467.aspx)" und " [Set-VMHost](https://technet.microsoft.com/library/hh848524.aspx)". In diesem Beispiel werden alle drei verwendet und folgende Aktionen durchführt:
  - Hiermit wird die Live Migration auf dem lokalen Host konfiguriert.
  - Ermöglicht eingehenden Migrations Datenverkehr nur in einem bestimmten Netzwerk.
  - Wählt Kerberos als Authentifizierungsprotokoll aus.

Jede Zeile entspricht einem separaten Befehl.

```PowerShell
PS C:\> Enable-VMMigration

PS C:\> Set-VMMigrationNetwork 192.168.10.1

PS C:\> Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos
```

Mit "Set-VMHost" können Sie auch eine Leistungs Option (und viele andere Host Einstellungen) auswählen. Wenn Sie z. b. SMB auswählen, aber das Authentifizierungsprotokoll auf den Standardwert von "kredssp" festlegen, geben Sie Folgendes ein:

```PowerShell
PS C:\> Set-VMHost -VirtualMachineMigrationPerformanceOption SMB
```

In dieser Tabelle wird beschrieben, wie die Leistungsoptionen funktionieren.

|Option|Beschreibung|
|----------|---------------|
    |TCP/IP|Der Arbeitsspeicher des virtuellen Computers wird über eine TCP/IP-Verbindung auf den Zielserver kopiert.|
    |Komprimierung|Komprimiert den Speicherinhalt der virtuellen Maschine, bevor Sie über eine TCP/IP-Verbindung auf den Zielserver kopiert wird. **Hinweis:** Dies ist die **Standard** Einstellung.|
    |SMB|Der Arbeitsspeicher des virtuellen Computers wird über eine SMB 3,0-Verbindung auf den Zielserver kopiert.<p>-SMB Direct wird verwendet, wenn für die Netzwerkadapter auf den Quell-und Ziel Servern RDMA (Remote Direct Memory Access)-Funktionen aktiviert sind.<br />-SMB Multichannel erkennt und verwendet automatisch mehrere Verbindungen, wenn eine entsprechende SMB Multichannel-Konfiguration identifiziert wird.<p>Weitere Informationen finden Sie unter [Optimieren der Leistung von Dateiservern mit %%amp;quot;SMB Direct%%amp;quot;](https://technet.microsoft.com/library/jj134210(WS.11).aspx).|

 ## <a name="next-steps"></a>Nächste Schritte

 Nachdem Sie die Hosts eingerichtet haben, sind Sie bereit, eine Live Migration durchzuführen. Anweisungen hierzu finden [Sie unter Verwenden der Live Migration ohne Failoverclustering zum Verschieben einer virtuellen Maschine](../manage/Use-live-migration-without-Failover-Clustering-to-move-a-virtual-machine.md).
