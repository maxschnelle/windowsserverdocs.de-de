---
title: Schritt 7 installieren und Konfigurieren von 2-APP1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cc0abc6-be4d-4cbe-bd0c-cc448bf294f6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8b0f91b4d2b876cb7b22dc8614e7ea5dcce6da2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833561"
---
# <a name="step-7-install-and-configure-2-app1"></a>Schritt 7 installieren und Konfigurieren von 2-APP1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

2-APP1 bietet Web- und Dateifreigabedienste. 2-APP1-Konfiguration umfasst Folgendes:  
  
- Installieren des Betriebssystems auf 2-APP1  
  
- Konfigurieren von TCP/IP-Eigenschaften  
  
- Fügen Sie der Domäne CORP2 2-APP1  
  
- Installieren Sie die Rolle Webserver (IIS) auf 2-APP1  
  
- Erstellen eines freigegebenen Ordners auf 2-APP1 
  
## <a name="bkmk_InstallOS"></a>Installieren des Betriebssystems auf 2-APP1  
Installieren Sie zunächst Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
#### <a name="to-install-the-operating-system-on-2-app1"></a>So installieren Sie das Betriebssystem auf 2-APP1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation).  
  
2.  Folgen Sie den Installationsanweisungen, und legen Sie ein sicheres Kennwort für das lokale Administratorkonto fest. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  2-APP1-Verbindung mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows-Update, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
4.  Verbinden Sie 2-APP1, mit dem 2-Corpnet-Subnetz.  
  
## <a name="bkmk_TCP"></a>Konfigurieren Sie TCP/IP-Eigenschaften  
Konfigurieren Sie TCP/IP-Eigenschaften auf 2-APP1 an.  
  
#### <a name="to-configure-tcpip-properties"></a>So konfigurieren Sie die TCP/IP-Eigenschaften  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  In der **Netzwerkverbindungen** Fenster mit der rechten Maustaste **verkabelte Ethernetverbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **10.2.0.3**. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein. In **Standardgateway**, Typ **10.2.0.254**.  
  
5.  Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. In **Bevorzugter DNS-Server**, Typ **10.2.0.1**.  
  
6.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**. In **DNS-Suffix für diese Verbindung**, Typ **corp2.corp.contoso.com**, und klicken Sie auf **OK** zweimal.  
  
7.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
8.  Klicken Sie auf **verwenden Sie die folgende IPv6-Adresse**. In **IPv6-Adresse**, Typ **2001:db8:2::3**. In **Subnetzpräfixlänge**, Typ **64**. In **Standardgateway**, Typ **2001:db8:2::fe**. Klicken Sie auf **verwenden Sie die folgenden DNS-Serveradressen**, und klicken Sie in **Bevorzugter DNS-Server**, Typ **2001:db8:2::1**.  
  
9. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
10. In **DNS-Suffix für diese Verbindung**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK** zweimal.  
  
11. Auf der **Verbindungseigenschaften von Ethernetkabelverbindung** Dialogfeld auf **schließen**.  
  
12. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="bkmk_JoinDomain"></a>Fügen Sie der Domäne CORP2 2-APP1  
Fügen Sie der Domäne corp2.corp.contoso.com 2-APP1.  
  
#### <a name="to-join-2-app1-to-the-corp2-domain"></a>2-APP1 der CORP2-Domäne beitreten  
  
1.  In der Server-Manager-Konsole in **lokalen Server**in die **Eigenschaften** Bereich, der neben **Computername**, klicken Sie auf den Link.  
  
2.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
3.  In **Computername**, Typ **2-APP1**. In **Mitglied**, klicken Sie auf **Domäne**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie für einen Benutzernamen und Kennwort aufgefordert werden, geben Sie **Administrator** und dessen Kennwort und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie ein Dialogfeld, das Begrüßungsdialogfeld für die Domäne corp2.corp.contoso.com sehen, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Klicken Sie nach dem Neustart des Computers auf **Benutzer wechseln**, und klicken Sie dann auf **anderer Benutzer** und melden Sie sich bei der CORP2-Domäne mit dem Administratorkonto an.  
  
## <a name="bkmk_IIS"></a>Installieren Sie die Rolle Webserver (IIS) auf 2-APP1  
Installieren Sie die Rolle Webserver (IIS), um 2-APP1 einen Webserver zu machen.  
  
#### <a name="to-install-the-web-server-iis-role"></a>Die Rolle "Webserver (IIS)" installiert  
  
1.  In der Server-Manager-Konsole auf die **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie auf **Weiter** dreimal, um dem Auswahlbildschirm des Server-Rolle zu erhalten  
  
3.  Auf der **Serverrollen auswählen** Seite **Webserver (IIS)**, und klicken Sie dann auf **Weiter** viermal.  
  
4.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
5.  Stellen Sie sicher, dass die Installation erfolgreich war, und klicken Sie dann auf **schließen**.  
  
## <a name="bkmk_Share"></a>Erstellen eines freigegebenen Ordners auf 2-APP1  
Erstellen Sie einen freigegebenen Ordner und eine Textdatei im Ordner auf 2-APP1 an.  
  
#### <a name="to-create-a-shared-folder"></a>Zum Erstellen eines freigegebenen Ordners  
  
1.  Auf der **starten** geben**explorer.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **Computer**, doppelklicken Sie dann auf **Lokaler Datenträger (c)**.  
  
3.  Klicken Sie auf **neuer Ordner**, Typ **Dateien**, und drücken Sie dann die EINGABETASTE. Lassen Sie die **lokalen Datenträger** Fenster geöffnet.  
  
4.  Auf der **starten** geben**notepad.exe**, mit der rechten Maustaste **Editor**, klicken Sie auf **erweitert**, und klicken Sie dann auf **Ausführen als Administrator**.  
  
5.  In der **Unbenannt - Editor** geben **Dies ist eine freigegebene Datei auf 2-APP1**.  
  
6.  Klicken Sie auf **Datei**, klicken Sie auf **speichern**, klicken Sie auf **Computer**, doppelklicken Sie auf **Lokaler Datenträger (c)**, und doppelklicken Sie dann auf die **Dateien**  Ordner.  
  
7.  In **Dateiname**, Typ **example.txt**, und klicken Sie dann auf **speichern**. Schließen Sie Editor.  
  
8.  In der **lokalen Datenträger** Fenster mit der rechten Maustaste die **Dateien** Ordner, zeigen Sie auf **freigeben**, und klicken Sie dann auf **bestimmte Personen**.  
  
9. Auf der **Dateifreigabe** klicken Sie im Dialogfeld, in der Dropdown-Liste **jeder**, und klicken Sie dann auf **hinzufügen**. In **Berechtigungsebene** für **jeder**, klicken Sie auf **Lese-/Schreibzugriff**.  
  
10. Klicken Sie auf **Freigabe**, und klicken Sie dann auf **Fertig**.  
  
11. Schließen der **lokalen Datenträger** Fenster.  
  


