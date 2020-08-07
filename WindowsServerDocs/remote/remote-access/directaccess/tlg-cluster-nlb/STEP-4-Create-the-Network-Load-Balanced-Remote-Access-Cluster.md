---
title: Schritt 4 Erstellen des Remote Zugriffs Clusters mit Netzwerk Lastenausgleich
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 509eaa08-c49d-448d-a71e-c1c45519ccd5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b18531c3704d9240ecfa2c3d411158a7ef7a97df
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971707"
---
# <a name="step-4-create-the-network-load-balanced-remote-access-cluster"></a>Schritt 4 Erstellen des Remote Zugriffs Clusters mit Netzwerk Lastenausgleich

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

 Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ermöglichen Ihnen das Erstellen von Clustern von Remote Zugriffs Servern. Ein Cluster fungiert als einzelner logischer Server und ermöglicht eine zentralisierte Konfiguration und Verwaltung der Server im Cluster. Bei Verwendung des Netzwerk Lastenausgleichs (Network Load Balancing, NLB) wird die Unterstützung für bis zu 8 Remote Zugriffs Mitglieder in einem einzelnen Cluster unterstützt. RAS-Cluster bieten Hochverfügbarkeit und Lastenausgleich von Verbindungen zwischen DirectAccess-Clients und dem internen Netzwerk.

Die folgenden Prozeduren ermöglichen es Ihnen, einen Remote Zugriffs Cluster zu erstellen und zu testen:

1. Installieren Sie das Feature für den Netzwerk Lastenausgleich auf Edge1 und EDGE2. Vor dem Aktivieren des Lasten Ausgleichs müssen Sie das Feature für den Netzwerk Lastenausgleich sowohl auf Edge1 als auch auf EDGE2 installieren.

2. Aktivieren Sie den Lastenausgleich auf Edge1. Edge1 wurde ursprünglich im Einzel Server Modus installiert. Um den Lastenausgleich zu aktivieren, konfigurieren Sie neue externe und interne dedizierte IP-Adressen (Dips) für Edge1. Die vorherigen Dips auf Edge1 werden automatisch als virtuelle IP-Adressen (VIPs) für den Cluster konfiguriert. Die neue externe DIP ist z 131.107.0.10, die neue interne IPv4-DIP ist 10.0.0.10, die neue interne IPv6-DIP ist 2001: db8:1:: 10. Die Cluster-VIPs lauten 131.107.0.2 und 131.107.0.2 (extern), 10.0.0.2 und 2001: db8:1:: 2 (intern).

3. Fügen Sie dem Cluster mit Lastenausgleich EDGE2 hinzu. Nachdem Sie den Lastenausgleich aktiviert haben, können Sie dem Cluster jetzt EDGE2 hinzufügen, um einen Lastenausgleich und hohe Verfügbarkeit für DirectAccess-Clientverbindungen bereitzustellen.

## <a name="prerequisites"></a>Voraussetzungen

Wenn Sie diese Testumgebung auf virtuellen Computern erstellen, müssen Sie das Spoofing von Mac-Adressen auf Edge1 und EDGE2 aktivieren.

### <a name="enable-mac-address-spoofing-on-edge1-and-edge2"></a>Aktivieren des Spoofing von Mac-Adressen auf Edge1 und EDGE2

1.  Führen Sie ein ordnungsgemäßes Herunterfahren auf Edge1 und EDGE2 aus.

2.  Klicken Sie auf dem Computer, auf dem Ihre virtuellen Computer gehostet werden, im **Hyper-V-Manager**mit der rechten Maustaste auf Edge1, und klicken Sie dann auf **Einstellungen**

3.  Klicken Sie im Dialogfeld **Einstellungen** in der Liste **Hardware** auf den Netzwerkadapter, der mit dem Unternehmensnetzwerk verbunden ist, und aktivieren Sie dann im Detailbereich das Kontrollkästchen **Spoofing von Mac-Adressen aktivieren** .

4.  Klicken Sie in der Liste **Hardware** auf den Netzwerkadapter, der mit dem Internet verbunden ist, und aktivieren Sie dann im Detailbereich das Kontrollkästchen **Spoofing von Mac-Adressen aktivieren** .

5.  Klicken Sie im Dialogfeld **Einstellungen** auf **OK**.

6.  Wiederholen Sie diesen Vorgang aus Schritt 2 auf EDGE2.

## <a name="install-the-network-load-balancing-feature-on-edge1-and-edge2"></a>Installieren des Netzwerk Lastenausgleichs-Features auf Edge1 und EDGE2
Wenn Sie Edge1 und EDGE2 in einem Cluster konfigurieren möchten, müssen Sie das Feature für den Netzwerk Lastenausgleich sowohl für Edge1 als auch für EDGE2 installieren.

### <a name="to-install-network-load-balancing"></a>So installieren Sie den Netzwerk Lastenausgleich

1.  Klicken Sie auf Edge1 in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.

2.  Klicken Sie viermal auf **weiter** , um zum Bildschirm für die Server Funktionsauswahl zu gelangen.

3.  Klicken Sie im Dialogfeld **Features auswählen** auf **Netzwerk Lastenausgleich**, klicken Sie auf **Features hinzufügen**, klicken Sie auf **weiter**, und klicken Sie dann auf **Installieren**.

4.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.

5.  Wiederholen Sie diesen Vorgang auf EDGE2.

## <a name="enable-load-balancing-on-edge1"></a>Aktivieren des Lasten Ausgleichs auf Edge1
Verwenden Sie dieses Verfahren, um den Lastenausgleich zu aktivieren und die neuen Dips auf Edge1 zu konfigurieren.

### <a name="enable-load-balancing"></a>Aktivieren des Lastenausgleichs

1.  Klicken Sie auf Edge1 auf **Start**, geben Sie **RAMgmtUI.exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

2.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole im linken Bereich auf **Konfiguration**, und klicken Sie dann im Bereich **Tasks** auf **Lastenausgleich aktivieren**.

3.  Klicken Sie im Assistenten zum Aktivieren des Lasten Ausgleichs auf **weiter**.

4.  Klicken Sie auf der Seite **Lasten Ausgleichs Methode** auf **Windows-Netzwerk Lastenausgleich (NLB) verwenden**, und klicken Sie dann auf **weiter**.

5.  Geben Sie auf der Seite **externe dedizierte IP-Adressen** im Feld **IPv4-Adresse** **z 131.107.0.10**im Feld **Subnetzmaske** ein, vergewissern Sie sich, dass das Subnetzpräfix **255.255.255.0**lautet, und klicken Sie dann auf **weiter**.

6.  Führen Sie auf der Seite **interne dedizierte IP-Adressen** die folgenden Schritte aus, und klicken Sie dann auf **weiter**:

    1.  Geben Sie im Feld **IPv4** -Adresse **10.0.0.10** ein, und vergewissern Sie sich, dass im Feld **Subnetzmaske** das Subnetzpräfix **255.255.255.0**lautet.

    2.  Geben Sie im Feld **IPv6-Adresse** den Wert **2001: db8:1:: 10** ein, und überprüfen Sie in der Länge des Subnetzpräfixes, ob der Wert **64**lautet.

7.  Klicken Sie auf der Seite **Zusammenfassung** auf **Commit**.

8.  Klicken Sie im Dialogfeld **Lastenausgleich aktivieren** auf **Schließen**.

9. Klicken Sie im Assistenten zum Aktivieren des Lasten Ausgleichs auf **Schließen**.

## <a name="add-edge2-to-the-load-balanced-cluster"></a>Hinzufügen von EDGE2 zum Cluster mit Lastenausgleich
Verwenden Sie dieses Verfahren, um dem NLB-Cluster EDGE2 hinzuzufügen.

> [!NOTE]
> Warten Sie zwei Minuten, nachdem Sie die vorherigen Schritte abgeschlossen haben, bevor Sie fortfahren. Nachdem der Netzwerk Lastenausgleich aktiviert wurde, wird der Befehl "raconfigtask" ausgeführt und konfiguriert den Computer mit NLB-Einstellungen. Dieser Vorgang kann einige Minuten in Anspruch nehmen, und wenn der Administrator eine weitere NLB-bezogene Konfiguration ausführt, bevor der Task beendet wird, tritt bei dieser Konfiguration ein Fehler auf.

### <a name="add-edge2-to-the-cluster"></a>Hinzufügen von EDGE2 zum Cluster

1.  Klicken Sie auf dem Computer Edge1 oder Virtual Machine in der Remote Zugriffs-Verwaltungskonsole im Bereich **Tasks** unter **Cluster mit Lasten**Ausgleich auf **Server hinzufügen oder entfernen**.

2.  Klicken Sie im Dialogfeld **Server hinzufügen oder entfernen** auf **Server hinzufügen**.

3.  Geben Sie im Assistenten zum **Hinzufügen eines Servers** auf der Seite **Server auswählen** den Namen **EDGE2**ein, und klicken Sie dann auf **weiter**.

4.  Vergewissern Sie sich, dass auf der Seite **Netzwerkadapter** unter **externer Adapter**die Option **Internet** ausgewählt ist, und stellen Sie im **internen Adapter**sicher, dass **Corpnet** ausgewählt ist. Klicken Sie im Dialogfeld **Windows-Sicherheit** auf **Durchsuchen**, stellen Sie sicher, dass **IP-HTTPS-Zertifikat** ausgewählt ist, klicken Sie auf **OK**, und klicken Sie dann auf **weiter**.

5.  Klicken Sie auf der Seite **Zusammenfassung** auf **Hinzufügen**.

6.  Klicken Sie auf der Seite **Abschluss des Vorgangs** auf **Schließen**.

7.  Klicken Sie im Dialogfeld **Server hinzufügen oder entfernen** auf **Commit**.

8.  Klicken Sie im Dialogfeld zum **Hinzufügen und Entfernen von Servern** auf **Schließen**.

9. Geben Sie auf dem **Start** Bildschirm**nlbmgr.exe**ein, und drücken Sie die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

10. Klicken Sie im **Netzwerk Lastenausgleich-Manager**auf **interner da-Cluster**. Stellen Sie im Detailbereich sicher, dass sowohl **Edge1 (Corpnet)** als auch **EDGE2 (Corpnet)** den Status **konvergiert**haben.

11. Wenn ein Server nicht **konvergiert**ist, klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Server, zeigen Sie auf **Host steuern**, und klicken Sie dann auf **starten**.

12. Klicken Sie im **Netzwerk Lastenausgleich-Manager**auf **Internet-da-Cluster**. Stellen Sie sicher, dass im Detailbereich sowohl **Edge1 (Internet)** als auch **EDGE2 (Internet)** den Status **konvergiert**aufweisen.

13. Wenn ein Server nicht **konvergiert**ist, klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Server, zeigen Sie auf **Host steuern**, und klicken Sie dann auf **starten**.
