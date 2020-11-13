---
title: Erweitern Ihrer lokalen Subnetze in Azure mithilfe von Azure Extended Network
description: Erweitern Ihrer lokalen Subnetze in Azure mithilfe von Azure Extended Network
ms.technology: manage
ms.topic: article
author: grcusanz
ms.author: grcusanz
ms.date: 12/17/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 29e370da31b02a475f0fdd5d7914348189ca616b
ms.sourcegitcommit: 6a245fefdf958bfc0aeb69f7a887d11a07bdcd23
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2020
ms.locfileid: "94570355"
---
# <a name="extend-your-on-premises-subnets-into-azure-using-azure-extended-network"></a>Erweitern Ihrer lokalen Subnetze in Azure mithilfe von Azure Extended Network

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

## <a name="overview"></a>Überblick

Azure Extended Network ermöglicht Ihnen das Strecken eines lokalen Subnetzes in Azure, damit lokale virtuelle Computer Ihre ursprünglichen lokalen privaten IP-Adressen bei der Migration zu Azure aufbewahren können.

Das Netzwerk wird mit einem bidirektionalen vxlan-Tunnel zwischen zwei Windows Server 2019-VMS erweitert, die als virtuelle Geräte fungieren, von denen eine lokal ausgeführt wird und die andere in Azure ausgeführt wird, wobei jede auch mit dem Subnetz verbunden ist, das erweitert werden soll.
Jedes Subnetz, das Sie erweitern möchten, erfordert ein paar von Geräten. Mehrere Subnetze können mithilfe mehrerer Paare erweitert werden.

> [!NOTE]
> Azure Extended Network sollte nur für Computer verwendet werden, deren IP-Adresse bei der Migration zu Azure nicht geändert werden kann. Es ist immer besser, die IP-Adresse zu ändern und mit einem Subnetz zu verbinden, das vollständig in Azure vorhanden ist, wenn dies eine Option ist.

## <a name="planning"></a>Planung

Zum Vorbereiten der Verwendung von Azure Extended Network müssen Sie das Subnetz, das Sie Strecken möchten, ermitteln und dann die folgenden Schritte ausführen:

### <a name="capacity-planning"></a>Kapazitätsplanung

Sie können bis zu 250 IP-Adressen mit erweitertem Azure-Netzwerk erweitern. Sie können einen aggregierten Durchsatz von ca. 700 Mbit/s erwarten. Dies hängt von der CPU-Geschwindigkeit der virtuellen Azure-Geräte für erweiterte Netzwerke ab.

### <a name="configuration-in-azure"></a>Konfiguration in Azure

Vor der Verwendung des Windows Admin Centers müssen Sie die folgenden Schritte im Azure-Portal ausführen:

1. Erstellen Sie ein virtuelles Netzwerk in Azure, das mindestens zwei Subnetze enthält, zusätzlich zu den Subnetzen, die für Ihre Gatewayverbindung erforderlich sind. Eines der Subnetze, das Sie erstellen, muss die gleiche Subnetz-CIDR wie das lokale Subnetz verwenden, das Sie erweitern möchten. Das Subnetz muss innerhalb ihrer Routing Domäne eindeutig sein, damit es sich nicht mit lokalen Subnetzen überlappt.

2. Konfigurieren Sie ein virtuelles Netzwerk Gateway für die Verwendung einer Site-to-Site-oder expressroute-Verbindung, um das virtuelle Netzwerk mit Ihrem lokalen Netzwerk zu verbinden.

3. Erstellen Sie einen virtuellen Windows Server 2019-Computer in Azure, der die Netzwerkvirtualisierung ausführen kann. Dies ist eines der beiden virtuellen Geräte. Verbinden Sie die primäre Netzwerkschnittstelle mit dem Routing fähigen Subnetz und der zweiten Netzwerkschnittstelle mit dem erweiterten Subnetz.

4. Starten Sie den virtuellen Computer, aktivieren Sie die Hyper-V-Rolle, und starten Sie neu. Beispiel:

    ```powershell
    Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
    ```

5. Erstellen Sie zwei externe virtuelle Switches auf dem virtuellen Computer, und stellen Sie eine Verbindung mit den einzelnen Netzwerkschnittstellen her. Beispiel:

    ```powershell
    New-VMSwitch -Name "External" -AllowManagementOS $true -NetAdapterName "Ethernet"
    New-VMSwitch -Name "Extended" -AllowManagementOS $true -NetAdapterName "Ethernet 2"
    ```

### <a name="on-premises-configuration"></a>Lokale Konfiguration

Außerdem müssen Sie eine manuelle Konfiguration in Ihrer lokalen Infrastruktur ausführen, einschließlich der Erstellung eines virtuellen Computers, der als lokales virtuelles Gerät fungiert:

1. Stellen Sie sicher, dass die Subnetze auf dem physischen Computer verfügbar sind, auf dem Sie die lokale VM (virtuelles Gerät) bereitstellen. Dies umfasst das Subnetz, das Sie erweitern möchten, und ein zweites Subnetz, das eindeutig ist und sich nicht mit Subnetzen im virtuellen Azure-Netzwerk überschneidet.

2. Erstellen Sie einen virtuellen Windows Server 2019-Computer auf jedem Hypervisor, der die Netzwerkvirtualisierung unterstützt. Dies ist das lokale virtuelle Gerät. Es wird empfohlen, dass Sie diese als hoch verfügbare VM in einem Cluster erstellen. Verbinden Sie einen virtuellen Netzwerkadapter mit dem Routing fähigen Subnetz und einem zweiten virtuellen Netzwerkadapter mit dem erweiterten Subnetz.

3. Starten Sie den virtuellen Computer, führen Sie diesen Befehl in einer PowerShell-Sitzung auf dem virtuellen Computer aus, um die Hyper-V-Rolle zu aktivieren, und starten Sie den virtuellen Computer neu

    ```powershell
    Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
    ```

4. Führen Sie die folgenden Befehle in einer PowerShell-Sitzung auf dem virtuellen Computer aus, um zwei externe virtuelle Switches auf dem virtuellen Computer zu erstellen und eine Verbindung mit den einzelnen Netzwerkschnittstellen herzustellen:

    ```powershell
    New-VMSwitch -Name "External" -AllowManagementOS $true -NetAdapterName "Ethernet"
    New-VMSwitch -Name "Extended" -AllowManagementOS $true -NetAdapterName "Ethernet 2"
    ```

### <a name="additional-prerequisites"></a>Zusätzliche Voraussetzungen

Wenn Sie über eine Firewall zwischen Ihrem lokalen Netzwerk und Azure verfügen, müssen Sie diese so konfigurieren, dass Sie asymmetrisches Routing zulässt. Dies kann Schritte zum Deaktivieren der zufälligen Sequenznummern und zum Aktivieren der TCP-Status Umgehung einschließen. Diese Schritte finden Sie in der Dokumentation Ihres Firewall-Herstellers.

## <a name="deploy"></a>Bereitstellen

Die Bereitstellung wird über das Windows Admin Center gesteuert.

### <a name="install-and-configure-windows-admin-center"></a>Installieren und Konfigurieren des Windows Admin Centers

1. [Laden Sie Windows Admin Center herunter, und installieren](../understand/windows-admin-center.md) Sie es auf jedem Computer, auf dem Windows Admin Center ausgeführt werden kann, und nicht auf den beiden zuvor erstellten virtuellen Geräten.

2. Wählen Sie im Windows Admin Center die Option **Einstellungen** (in der oberen rechten Ecke der Seite) > **Erweiterungen** aus. Wählen Sie dann **Erweiterungen** aus:

    ![Screenshot der Registerkarte "verfügbare Erweiterungen" der Einstellungen](../media/azure-extended-network/installed-extensions.png)

3. Wählen Sie auf der Registerkarte **Verfügbare Erweiterungen** die Option **Azure Extended Network** aus, und klicken Sie dann auf **Installieren**.

    Nach wenigen Sekunden sollte eine Meldung angezeigt werden, die auf eine erfolgreiche Installation hinweist.

4. [Verbinden Sie das Windows Admin Center mit Azure](azure-integration.md), falls Sie dies noch nicht getan haben. Wenn Sie diesen Schritt jetzt überspringen, werden Sie später in diesem Prozess aufgefordert, dies zu tun.

5. Wechseln Sie im Windows Admin Center zu **alle Verbindungen**  >  **Hinzufügen** , und wählen Sie dann in der **Windows Server** -Kachel **Hinzufügen** aus. Geben Sie den Servernamen (und ggf. die Anmelde Informationen) für das lokale virtuelle Gerät ein.

    ![Screenshot des Windows Admin Centers mit dem erweiterten Azure-Netzwerk Tool in Server-Manager auf dem lokalen virtuellen Gerät](../media/azure-extended-network/azure-extended-network.png).

6. Klicken Sie auf **Azure Extended Network** , um zu beginnen. Wenn Sie das erste Mal eine Übersicht und eine Setup Schaltfläche angezeigt werden:

    ![Bild](../media/azure-extended-network/azure-extended-network-intro.png)

### <a name="deploy-azure-extended-network"></a>Azure Extended Network bereitstellen

1. Klicken Sie auf **Einrichten** , um die Konfiguration zu starten.

2. Klicken Sie auf **weiter** , um mit der Übersicht fortzufahren.

3. Im Bereich **Paket hochladen** müssen Sie das Azure Extended Network Agent-Paket herunterladen und auf das virtuelle Gerät hochladen. Befolgen Sie die Anweisungen im Bereich.

    > [!IMPORTANT]
    > Scrollen Sie bei Bedarf nach unten, und klicken Sie auf **hochladen** , bevor Sie auf **Weiter klicken: Extended-Network Setup**.

4. Wählen Sie die Subnetz-CIDR für das lokale Netzwerk aus, das Sie erweitern möchten. Die Liste der Subnetze wird vom virtuellen Gerät eingelesen. Wenn Sie das virtuelle Gerät nicht mit der richtigen Gruppe von Subnetzen verbunden haben, wird die gewünschte Subnetz-CIDR in dieser Liste nicht angezeigt.

5. Klicken Sie auf **weiter** , nachdem Sie das Subnetz CIDR ausgewählt haben.

6. Wählen Sie das Abonnement, die Ressourcengruppe und das virtuelle Netzwerk aus, in das Sie sich erweitern:

    ![Azure-Netzwerk](../media/azure-extended-network/azure-network.png)

    Die Region (Azure-Standort) und das Subnetz werden automatisch ausgewählt. Wählen Sie weiter: Extended-Network Gateway-Setup aus, um fortzufahren.

7. Nun konfigurieren Sie die virtuellen Geräte. Die Informationen für das lokale Gateway sollten automatisch aufgefüllt werden:

    ![lokales Netzwerk Gateway](../media/azure-extended-network/on-premises-network-gateway.png)

    Wenn es korrekt aussieht, können Sie auf **weiter** klicken.

8. Für das virtuelle Azure-Gerät müssen Sie die Ressourcengruppe und die VM auswählen, die verwendet werden sollen:

    ![Azure-Netzwerk Gateway](../media/azure-extended-network/azure-network-gateway.png)

9. Nachdem Sie den virtuellen Computer ausgewählt haben, müssen Sie auch die Azure Extended-Network-gatewaysubnetz-CIDR auswählen. Klicken Sie dann auf **Weiter:** bereitstellen.

10. Überprüfen Sie die Zusammenfassungs **Informationen, und** klicken Sie dann auf bereitstellen, um mit der Die Bereitstellung dauert ungefähr 5-10 Minuten. Wenn die Bereitstellung fertiggestellt ist, wird der folgende Bereich zum Verwalten der erweiterten IP-Adressen angezeigt, und der Status sollte " **OK** " lauten:

    ![Installation ist beendet](../media/azure-extended-network/installation-complete.png)

## <a name="manage"></a>Verwalten

Alle IP-Adressen, die über das erweiterte Netzwerk erreichbar sein sollen, müssen konfiguriert werden. Sie können bis zu 250 Adressen für die Erweiterung konfigurieren.
So erweitern Sie eine Adresse

1. Klicken Sie auf **IPv4-Adressen hinzufügen** :

    ![Fügen von IPv4-Adressen](../media/azure-extended-network/add-ipv4-addresses.png)

2. Das Flyout **neue IPv4-Adressen hinzufügen** wird auf der rechten Seite angezeigt:

    ![Bereich für IPv4-Adressen hinzufügen](../media/azure-extended-network/add-ipv4-addresses-panel.png)

3. Verwenden Sie die Schaltfläche **Hinzufügen** , um eine Adresse manuell hinzuzufügen. Adressen, die Sie lokal hinzufügen, sind für die Azure-Adressen erreichbar, die Sie der Azure-Adressliste hinzufügen, und umgekehrt.

4. Azure Extended Network scannt das Netzwerk, um IP-Adressen zu ermitteln, und füllt die Vorschlags Listen basierend auf diesem Scan auf. Um diese Adressen zu erweitern, müssen Sie die Dropdown Liste verwenden und das Kontrollkästchen neben der ermittelten Adresse aktivieren. Nicht alle Adressen werden ermittelt. Verwenden Sie optional die Schaltfläche **Hinzufügen** , um Adressen manuell hinzuzufügen, die nicht automatisch erkannt werden.

    ![Bereich für IPv4-Adressen mit Informationen hinzufügen](../media/azure-extended-network/add-ipv4-addresses-panel-filled.png)

5. Klicken Sie nach Abschluss auf **Absenden** . Sie sehen, dass die Statusänderung auf " **Aktualisieren** ", " **Fortschreiten** " und " **OK** " zurückgeht, wenn die Konfiguration beendet ist.

    Ihre Adressen sind nun erweitert. Verwenden Sie die Schaltfläche IPv4-Adressen hinzufügen, um jederzeit weitere Adressen hinzuzufügen. Wenn eine IP-Adresse am Ende des erweiterten Netzwerks nicht mehr verwendet wird, aktivieren Sie das Kontrollkästchen daneben, und wählen Sie IPv4-Adressen entfernen aus.

Wenn Sie Azure Extended Network nicht mehr verwenden möchten, klicken Sie auf die Schaltfläche **Azure Extended-Network entfernen** . Dadurch wird der Agent aus den beiden virtuellen Geräten deinstalliert und die erweiterten IP-Adressen entfernt. Das Netzwerk wird nicht mehr erweitert. Sie müssen das Setup erneut ausführen, nachdem Sie es entfernt haben, wenn Sie das erweiterte Netzwerk erneut verwenden möchten.

## <a name="troubleshooting"></a>Problembehandlung

Wenn Sie während der Bereitstellung von Azure Extended Network einen Fehler erhalten, führen Sie die folgenden Schritte aus:

1. Vergewissern Sie sich, dass beide virtuellen Geräte Windows Server 2019 verwenden.

2. Vergewissern Sie sich, dass Sie Windows Admin Center nicht auf einem der virtuellen Geräte ausführen. Es wird empfohlen, das Windows Admin Center über ein lokales Netzwerk auszuführen.

3. Stellen Sie sicher, dass Sie über das Windows Admin Center-Gateway mithilfe von eine Remote Verbindung mit dem lokalen virtuellen Computer herstellen können `enter-pssession` .

4. Wenn eine Firewall zwischen Azure und dem lokalen Standort vorhanden ist, vergewissern Sie sich, dass Sie so konfiguriert ist, dass Sie UDP-Datenverkehr am ausgewählten Port zulässt (standardmäßig 4789). Verwenden Sie ein Tool wie "ctstraffic", um einen Listener und einen Absender zu konfigurieren. Überprüfen Sie, ob der Datenverkehr in beide Richtungen an den angegebenen Port gesendet werden kann.

5. Verwenden Sie pktmon, um zu überprüfen, ob die Pakete erwartungsgemäß gesendet und empfangen werden. Führen Sie pktmon auf jedem virtuellen Gerät aus:

    ```powershell
    Pktmon start –etw
    ```

6. Führen Sie die erweiterte Azure-Netzwerkkonfiguration aus, und starten Sie dann die Ablauf Verfolgung:

    ```powershell
    Pktmon stop
    Netsh trace convert input=<path to pktmon etl file>
    ```

7. Öffnen Sie die Textdatei, die von jedem virtuellen Gerät erstellt wird, und suchen Sie am angegebenen Port nach UDP-Datenverkehr (standardmäßig 4789). Wenn Datenverkehr vom lokalen virtuellen Gerät, aber nicht von der Azure Virtual Appliance-Instanz gesendet wird, müssen Sie das Routing und die Firewall zwischen den Geräten überprüfen. Wenn Sie Datenverkehr aus der lokalen Umgebung in Azure senden, sollten Sie sehen, dass das virtuelle Azure-Gerät ein Paket als Antwort sendet. Wenn dieses Paket nie vom lokalen virtuellen Gerät empfangen wird, müssen Sie sicherstellen, dass das Routing korrekt ist und dass keine Firewall zwischen dem Datenverkehr blockiert.

### <a name="diagnosing-the-data-path-after-initial-configuration"></a>Diagnostizieren des Daten Pfads nach der Erstkonfiguration

Nachdem Azure Extended Network konfiguriert wurde, treten möglicherweise weitere Probleme auf, die auftreten können, wenn Firewalls den Datenverkehr blockieren, oder die MTU überschreitet, wenn der Fehler zeitweilig auftritt.

1. Stellen Sie sicher, dass beide virtuellen Geräte in Betrieb sind und ausgeführt werden.

2. Vergewissern Sie sich, dass der erweiterte Azure-Netzwerk-Agent auf den einzelnen virtuellen Geräten ausgeführt wird:

    ```powershell
    get-service extnwagent
    ```

3. Wenn der Status nicht ausgeführt wird, können Sie ihn wie folgt starten:

    ```powershell
    start-service extnwagent
    ```

4. Verwenden Sie packetmon, wie in Schritt 5 oben beschrieben, während Datenverkehr zwischen zwei VMS im erweiterten Netzwerk gesendet wird, um zu überprüfen, ob der Datenverkehr von den virtuellen Geräten empfangen, über den konfigurierten UDP-Port gesendet und dann vom anderen virtuellen Gerät empfangen und weitergeleitet wird.
