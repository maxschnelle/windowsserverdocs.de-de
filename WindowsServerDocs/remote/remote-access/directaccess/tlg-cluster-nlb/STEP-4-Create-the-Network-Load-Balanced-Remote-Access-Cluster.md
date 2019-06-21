---
title: Schritt 4 erstellen, das Netzwerk Load Remotezugriffsclusters mit Netzwerklastenausgleich
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 509eaa08-c49d-448d-a71e-c1c45519ccd5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b8e6defc6cc8579f18df2f9636383c65c9a18eb
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281609"
---
# <a name="step-4-create-the-network-load-balanced-remote-access-cluster"></a>Schritt 4 erstellen, das Netzwerk Load Remotezugriffsclusters mit Netzwerklastenausgleich

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

 Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ermöglichen Ihnen die Erstellung von Clustern mit RAS-Server. Ein Cluster fungiert als ein logischer Server und bietet zentralisierte Konfiguration und Verwaltung für die Server im Cluster. Bei Verwendung der Netzwerklastenausgleich (Network Load Balancing, NLB) wird unterstützt, für bis zu 8-RAS-Elemente in einem einzigen Cluster. Access-Remotecluster sorgen für hochverfügbarkeit und Lastenausgleich für Verbindungen von DirectAccess-Clients mit dem internen Netzwerk.  
  
Die folgenden Verfahren können Sie zum Erstellen und testen eine Testumgebungsbereitstellung eines remotezugriffsclusters:  
  
1. Installieren Sie das Feature Netzwerklastenausgleich auf EDGE1 und EDGE2 an. Vor dem Aktivieren des Lastenausgleichs, müssen Sie das Feature Network Load Balancing auf EDGE1 und EDGE2 installieren.
  
2. Aktivieren Sie den Lastenausgleich auf EDGE1. EDGE1 wurde ursprünglich im einzelnen Servermodus installiert. Um den Lastenausgleich zu aktivieren, konfigurieren Sie die neue externe und interne dedizierte IP-Adressen (DIPs) für EDGE1. Der vorherige DIPs auf EDGE1 werden automatisch als virtuelle IP-Adressen (VIPs) für den Cluster konfiguriert. Die neue externe DIP ist 131.107.0.10, die neue interne DIP-IPv4-Adresse 10.0.0.10 ist die neue interne IPv6-DIP ist 2001:db8:1::10. Die Cluster-VIPs sind 131.107.0.2 "und" 131.107.0.3 (extern), "und" 10.0.0.2 "und" 2001:db8:1::2 (intern).
  
3. Die Load-Clusters mit Lastenausgleich wird von EDGE2 hinzugefügt. Nach der Aktivierung des Lastenausgleichs, können Sie jetzt von EDGE2 an den Cluster zu Lastausgleich und hoher Verfügbarkeit für DirectAccess-Client-Verbindungen hinzufügen.

## <a name="prerequisites"></a>Vorraussetzungen

Wenn Sie diese testumgebung auf virtuellen Computern erstellen, müssen Sie auf EDGE1 und EDGE2 spoofing von MAC-aktivieren.  
  
### <a name="enable-mac-address-spoofing-on-edge1-and-edge2"></a>Aktivieren Sie auf EDGE1 und EDGE2 spoofing von MAC-  
  
1.  Führen Sie ein ordnungsgemäßes Herunterfahren auf EDGE1 und EDGE2 an.  
  
2.  Auf dem Computer mit Ihren virtuellen Computern **Hyper-V-Manager**mit der rechten Maustaste auf EDGE1, und klicken Sie dann auf **Einstellungen**.  
  
3.  Auf der **Einstellungen** Dialogfeld die **Hardware** auflisten, klicken Sie auf den Netzwerkadapter mit dem Corpnet-Netzwerk verbunden, und wählen Sie dann im Detailbereich die **spoofing von MAC-Adressen zu aktivieren**  Kontrollkästchen.  
  
4.  In der **Hardware** auflisten, klicken Sie auf den Netzwerkadapter mit dem Internet-Netzwerk verbunden, und wählen Sie dann im Detailbereich die **aktivieren, spoofing von MAC-Adressen** Kontrollkästchen.  
  
5.  Auf der **Einstellungen** Dialogfeld klicken Sie auf **OK**.  
  
6.  Wiederholen Sie diesen Vorgang aus Schritt 2 auf EDGE2 aus.  
  
## <a name="install-the-network-load-balancing-feature-on-edge1-and-edge2"></a>Installieren Sie den Netzwerklastenausgleich-Funktion auf EDGE1 und EDGE2  
Zum Konfigurieren von EDGE1 und EDGE2 in einem Cluster müssen Sie die Funktion des Netzwerklastenausgleichs auf EDGE1 und EDGE2 installieren.  
  
### <a name="to-install-network-load-balancing"></a>So installieren Sie den Netzwerklastenausgleich  
  
1.  Auf EDGE1, in der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie auf **Weiter** viermal, um Server Funktionsauswahl-Bildschirm zu erhalten.  
  
3.  Auf der **Funktionen auswählen** die Option **Netzwerklastenausgleich**, klicken Sie auf **Features hinzufügen**, klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
4.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
5.  Wiederholen Sie dieses Verfahren auf EDGE2 aus.  
  
## <a name="enable-load-balancing-on-edge1"></a>Aktivieren Sie den Lastenausgleich auf EDGE1  
Verwenden Sie dieses Verfahren, um den Lastenausgleich auf Aktivieren und Konfigurieren der neuen DIPs EDGE1.  
  
### <a name="enable-load-balancing"></a>Aktivieren des Lastenausgleichs  
  
1.  Klicken Sie auf EDGE1, auf **starten**, Typ **RAMgmtUI.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole, klicken Sie im linken Bereich auf **Konfiguration**, und klicken Sie dann in der **Aufgaben** Bereich, klicken Sie auf **Lastenausgleich aktivieren**.  
  
3.  Klicken Sie in der Load Balancing Assistent zum Aktivieren, auf **Weiter**.  
  
4.  Auf der **Load Balancing-Methode** auf **verwenden Windows Network Load Balancing (NLB)** , und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **externen dedizierte IP-Adressen** auf der Seite die **IPv4-Adresse** geben **131.107.0.10**in die **Subnetzmaske** überprüfen Sie, ob die Subnetzpräfix ist **255.255.255.0**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **internen dedizierte IP-Adressen** Seite gehen Sie folgendermaßen vor, und klicken Sie dann auf **Weiter**:  
  
    1.  In der **IPv4-Adresse** geben **10.0.0.10** und klicken Sie in der **Subnetzmaske** überprüfen Sie, ob das Subnetzpräfix ist **255.255.255.0**.  
  
    2.  In der **IPv6-Adresse** geben **2001:db8:1::10** und in die Subnetzpräfixlänge, überprüfen Sie, ob der Wert **64**.  
  
7.  Auf der **Zusammenfassung** auf **Commit**.  
  
8.  Auf der **Lastenausgleich aktivieren** Dialogfeld klicken Sie auf **schließen**.  
  
9. Klicken Sie in der Load Balancing Assistent zum Aktivieren, auf **schließen**.  
  
## <a name="add-edge2-to-the-load-balanced-cluster"></a>Hinzufügen von EDGE2 die Load-Clusters mit Lastenausgleich  
Verwenden Sie dieses Verfahren, um von EDGE2 zum NLB-Cluster hinzuzufügen.  
  
> [!NOTE]  
> Sie sollten zwei Minuten nach Abschluss der vorherigen Schritte vor dem Fortfahren warten. Nach der Aktivierung von NLB, die RAConfigTask und konfiguriert den Computer mit NLB-Einstellungen. Dies kann einige Minuten dauern, und die Konfiguration schlägt fehl, wenn der Administrator einer anderen verknüpften NLB-Konfiguration vor dem Ende der Task ausgeführt wird.  
  
### <a name="add-edge2-to-the-cluster"></a>Hinzufügen von EDGE2 zum cluster  
  
1.  Auf EDGE1-Computer oder virtuellen Computer in der Remotezugriffs-Verwaltungskonsole in der **Aufgaben** Bereich unter **Load Balanced Cluster**, klicken Sie auf **hinzufügen oder Entfernen von Servern**.  
  
2.  Auf der **hinzufügen oder Entfernen von Servern** Dialogfeld klicken Sie auf **-Server hinzufügen**.  
  
3.  Auf der **Hinzufügen eines Servers** Assistenten, auf die **Server auswählen** geben **EDGE2**, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Netzwerkadapter** auf der Seite **externen Adapter**, stellen Sie sicher, dass **Internet** ausgewählt ist, und klicken Sie in **des internen Adapters**, stellen Sie sicher, dass **"Corpnet"** ausgewählt ist. Klicken Sie auf **Durchsuchen**auf die **Windows-Sicherheit** Dialogfeld Feld, stellen Sie sicher, dass **IP-HTTPS-Zertifikat** wird ausgewählt, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Zusammenfassung** auf **hinzufügen**.  
  
6.  Klicken Sie auf der Seite **Abschluss des Vorgangs** auf **Schließen**.  
  
7.  Auf der **hinzufügen oder Entfernen von Servern** Dialogfeld klicken Sie auf **Commit**.  
  
8.  Auf der **hinzufügen und Entfernen von Servern** Dialogfeld klicken Sie auf **schließen**.  
  
9. Auf der **starten** geben**nlbmgr.exe**, und drücken Sie die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
10. In der **Netzwerklastenausgleich-Manager**, klicken Sie auf **interne DA Cluster**. Stellen Sie im Detailbereich sicher, dass beide **EDGE1(Corpnet)** und **EDGE2(Corpnet)** haben den Status **zusammengeführten**.  
  
11. Wenn kein Server ist **zusammengeführten**mit der rechten Maustaste auf den Server, in der Konsolenstruktur, zeigen Sie auf **Steuerelementhost**, und klicken Sie dann auf **starten**.  
  
12. In der **Netzwerklastenausgleich-Manager**, klicken Sie auf **Internet DA Cluster**. Stellen Sie sicher, die im Bereich "Details", beide **EDGE1(Internet)** und **EDGE2(Internet)** haben den Status **zusammengeführten**.  
  
13. Wenn kein Server ist **zusammengeführten**mit der rechten Maustaste auf den Server, in der Konsolenstruktur, zeigen Sie auf **Steuerelementhost**, und klicken Sie dann auf **starten**.
