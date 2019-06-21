---
title: DirectAccess-Offline-Domänenbeitritt
description: Dieser Leitfaden erläutert die Schritte, um eine offline-Domänenbeitritt mit DirectAccess in Windows Server 2016 ausführen.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55528736-6c19-40bd-99e8-5668169ef3c7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 59b5933a81c7021e58ea14e6ea4c4da374ce35cb
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283660"
---
# <a name="directaccess-offline-domain-join"></a>DirectAccess-Offline-Domänenbeitritt

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieser Leitfaden erläutert die Schritte zum Ausführen einer offline-Domänenbeitritt mit DirectAccess. Während ein offline-Domänenbeitritt ist ein Computer Beitritt zu einer Domäne ohne physische oder VPN-Verbindung konfiguriert.  
  
Das Handbuch umfasst folgende Abschnitte:  
  
- Offline-Domain-Join – Übersicht  
  
- Anforderungen für die offline-Domänenbeitritt
  
- Offline-Domänenbeitritt
  
- Schritte zum Ausführen einer offline-Domänenbeitritt  
  
## <a name="offline-domain-join-overview"></a>Offline-Domain-Join – Übersicht  
In Windows Server 2008 R2 eingeführt wurden, zählen Domänencontroller, ein Feature namens Offline-Domänenbeitritt auf. Ein Befehlszeilenprogramm, mit dem Namen Djoin.exe können Sie einen Computer in eine Domäne einbinden, ohne physisch wenden Sie sich beim Abschließen des Domänenbeitritts an einem Domänencontroller. Die allgemeinen Schritte für die Verwendung von Djoin.exe sind:  
  
1.  Führen Sie **Djoin /provision** um Metadaten für den Computer zu erstellen. Die Ausgabe dieses Befehls ist eine TXT-Datei, die einen Base64-codierten Blob enthält.  
  
2.  Führen Sie **Djoin /requestODJ** zum Einfügen von Metadaten für den Computer aus der TXT-Datei in das Windows-Verzeichnis des Zielcomputers.  
  
3.  Starten Sie den Zielcomputer neu, und der Computer wird mit der Domäne angehören.  
  
### <a name="BKMK_ODJOverview"></a>Offline-Domänenbeitritt mit DirectAccess-Richtlinien-Szenario (Übersicht)  
DirectAccess-offline-Domänenbeitritt ist ein Prozess, den Computer mit Windows Server 2016, Windows Server 2012, Windows 10 und Windows 8 können Sie einer Domäne beitreten, ohne physisch mit dem Unternehmensnetzwerk verknüpft wird, oder VPN-Verbindung. Dadurch kann zum Hinzufügen von Computern zu einer Domäne von Standorten, wenn keine Verbindung mit einem Unternehmensnetzwerk vorhanden ist. Offline-Domänenbeitritt für DirectAccess bietet DirectAccess-Richtlinien auf Clients, um remote-Bereitstellung zu ermöglichen.  
  
Ein Domänenbeitritt ein Computerkonto erstellt und richtet eine Vertrauensstellung zwischen einem Computer unter einem Windows-Betriebssystem und Active Directory-Domäne.  
  
## <a name="BKMK_ODJRequirements"></a>Vorbereitung des offline-Domänenbeitritt  
  
1.  Erstellen Sie das Computerkonto.  
  
2.  Erstellen Sie die Mitgliedschaft in der alle, die Sicherheitsgruppen, der das Computerkonto gehört.  
  
3.  Sammeln Sie die erforderliche Zertifikate, Gruppenrichtlinien und Gruppenrichtlinienobjekte, die auf den neuen Clients angewendet werden.  
  
. In den folgenden Abschnitten wird erläutert, den Anforderungen des Betriebssystems und Anforderungen an die Anmeldeinformationen für die Durchführung eines DirectAccess offline-Domänenbeitritts Verwendung von Djoin.exe.  
  
### <a name="operating-system-requirements"></a>Betriebssystemanforderungen  
Sie können den Djoin.exe für DirectAccess nur auf Computern ausführen, auf denen Windows Server 2016, Windows Server 2012 oder Windows 8 ausgeführt. Der Computer, auf dem Djoin.exe auf Daten der Bereitstellung des Computers-Konto in AD DS ausgeführt, wird, muss Windows Server 2016, Windows 10, Windows Server 2012 oder Windows 8 ausgeführt werden. Der Computer, den Sie mit der Domäne beitreten möchten muss auch Windows Server 2016, Windows 10, Windows Server 2012 oder Windows 8 ausgeführt werden.  
  
### <a name="credential-requirements"></a>Anforderungen bezüglich der Anmeldeinformationen  
Um eine offline-Domänenbeitritt auszuführen, müssen Sie die Rechte verfügen, die zum Hinzufügen von Arbeitsstationen zur Domäne erforderlich sind. Mitglieder der Gruppe "Domänen-Admins" verfügen über diese Rechte standardmäßig. Wenn Sie nicht Mitglied der Gruppe der Domänenadministratoren sind, muss Mitglied der Gruppe "Domänen-Admins" einen der folgenden Aktionen aus, die Ihnen ermöglichen, Hinzufügen von Arbeitsstationen zur Domäne ausführen:  
  
-   Verwenden Sie die Gruppenrichtlinie, um die erforderlichen Benutzerrechte gewähren. Diese Methode ermöglicht Ihnen die Erstellung von Computern in den standardcomputercontainern und in jede Organisationseinheit (OU), die später erstellt wird (sofern keine verweigern Zugriffssteuerungseinträge (ACEs) hinzugefügt werden).  
  
-   Bearbeiten Sie die Zugriffssteuerungsliste (ACL) der Standardcontainer für die Domäne, die richtigen Berechtigungen für Sie zu delegieren.  
  
-   Erstellen Sie eine Organisationseinheit, und bearbeiten die ACL für diese Organisationseinheit gewähren Sie der **Erstellen untergeordneter - ermöglichen** Berechtigung. Übergeben Sie die **/machineOU** Parameter, um die **Djoin /provision** Befehl.  
  
Die folgenden Verfahren zeigen, wie Sie die Benutzerrechte, mit der Gruppenrichtlinie zu gewähren und wie Sie die richtigen Berechtigungen zu delegieren.  
  
#### <a name="granting-user-rights-to-join-workstations-to-the-domain"></a>Erteilen von Benutzerrechten zum Hinzufügen von Arbeitsstationen zur Domäne  
Sie können die Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC) verwenden, ändern Sie die Domänenrichtlinie, oder erstellen eine neue Richtlinie mit Einstellungen, die die Benutzerrechte zum Hinzufügen von Arbeitsstationen zu einer Domäne zu erteilen.  
  
Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe sein, um Benutzerrechte erteilen.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) (https://go.microsoft.com/fwlink/?LinkId=83477).   
  
###### <a name="to-grant-rights-to-join-workstations-to-a-domain"></a>Zum Gewähren der Berechtigung für Arbeitsstationen mit einer Domäne verknüpfen.  
  
1.  Klicken Sie auf **Start**, dann auf **Verwaltung** und anschließend auf **Gruppenrichtlinienverwaltung**.  
  
2.  Doppelklicken Sie auf den Namen der Gesamtstruktur, doppelklicken Sie auf **Domänen**, doppelklicken Sie auf den Namen der Domäne, in dem Sie möchten Hinzufügen eines Computers, mit der rechten Maustaste **Default Domain Policy**, und klicken Sie dann auf  **Bearbeiten Sie**.  
  
3.  Doppelklicken Sie in der Konsolenstruktur auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Windows-Einstellungen**, doppelklicken Sie auf **Sicherheit Einstellungen**, doppelklicken Sie auf **lokale Richtlinien**, und doppelklicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
4.  Doppelklicken Sie im Detailbereich auf **Hinzufügen von Arbeitsstationen zur Domäne**.  
  
5.  Wählen Sie die **diese Richtlinieneinstellungen definieren** , und klicken Sie dann auf **Benutzer oder Gruppe hinzufügen**.  
  
6.  Geben Sie den Namen des Kontos, das Sie verwenden möchten, erteilen der Benutzerrechte in, und klicken Sie dann auf **OK** zweimal.  
  
## <a name="BKMK_ODKSxS"></a>Offline-Domänenbeitritt  
Führen Sie Djoin.exe an einer Eingabeaufforderung mit erhöhten Rechten, die Metadaten für Computer bereitstellen. Wenn Sie den Bereitstellungsbefehl ausführen, wird die Metadaten für Computer in einer Binärdatei erstellt, die Sie als Teil des Befehls angeben.  
  
Weitere Informationen zu den NetProvisionComputerAccount-Funktion, die verwendet wird, um das Computerkonto während einer offline-Domänenbeitritt bereitzustellen, finden Sie unter [NetProvisionComputerAccount Funktion](https://go.microsoft.com/fwlink/?LinkId=162426) (https://go.microsoft.com/fwlink/?LinkId=162426). Weitere Informationen zu den NetRequestOfflineDomainJoin-Funktion, die lokal auf dem Zielcomputer ausgeführt wird, finden Sie unter [NetRequestOfflineDomainJoin Funktion](https://go.microsoft.com/fwlink/?LinkId=162427) (https://go.microsoft.com/fwlink/?LinkId=162427).  
  
## <a name="BKMK_ODJSteps"></a>Schritte zum Ausführen eines DirectAccess-offline-Domänenbeitritts  
Die offline-Domänenbeitritt umfasst die folgenden Schritte aus:  
  
1.  Erstellen Sie ein neues Computerkonto für jeden der RAS-Clients und generieren Sie ein Bereitstellungspaket mithilfe des Befehls "Djoin.exe" von einer bereits-Domäne eingebundener Computer im Unternehmensnetzwerk.  
  
2.  Den Client-Computer zur Sicherheitsgruppe DirectAccessClients hinzufügen  
  
3.  Übertragen Sie das Paket sicher auf den Remotecomputern (s), die die Domäne beitritt.  
  
4.  Wenden Sie das Paket, und verknüpfen Sie den Client mit der Domäne.  
  
5.  Neustart des Clients für den Domänenbeitritt abzuschließen und die Verbindung herstellen.  
  
Es gibt zwei Optionen zur Erstellung der Bereitstellung Paket für den Client. Wenn Sie den Assistenten für erste Schritte zum Installieren von DirectAccess ohne PKI verwendet, sollten Sie Option 1 unten verwenden. Wenn Sie die erweiterten Setup-Assistenten zum Installieren von DirectAccess mit PKI verwendet, sollten Sie Option 2 unten verwenden.  
  
Führen Sie die folgenden Schritte aus, um die offline-Domänenbeitritt durchzuführen:  
  
##### <a name="option1-create-a-provisioning-package-for-the-client-without-pki"></a>Option 1: Erstellen eines Bereitstellungspakets für den Client ohne PKI  
  
1.  Geben Sie an einer Eingabeaufforderung Ihres RAS-Servers den folgenden Befehl aus, um das Computerkonto bereitzustellen:  
  
    ```  
    Djoin /provision /domain <your domain name> /machine <remote machine name> /policynames DA Client GPO name /rootcacerts /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="option2-create-a-provisioning-package-for-the-client-with-pki"></a>Option2: Erstellen eines Bereitstellungspakets für den Client mit der PKI  
  
1.  Geben Sie an einer Eingabeaufforderung Ihres RAS-Servers den folgenden Befehl aus, um das Computerkonto bereitzustellen:  
  
    ```  
    Djoin /provision /machine <remote machine name> /domain <Your Domain name> /policynames <DA Client GPO name> /certtemplate <Name of client computer cert template> /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="add-the-client-computer-to-the-directaccessclients-security-group"></a>Den Client-Computer zur Sicherheitsgruppe DirectAccessClients hinzufügen  
  
1.  Auf Ihrem Domänencontroller aus **starten** geben **Active** , und wählen Sie **Active Directory-Benutzer und-Computer** aus **Apps** Bildschirm .  
  
2.  Erweitern Sie die Struktur unter der Domäne, und wählen die **Benutzer** Container.  
  
3.  Klicken Sie im Detailbereich mit der Maustaste **DirectAccessClients**, und klicken Sie auf **Eigenschaften**.  
  
4.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
5.  Klicken Sie auf **Objekttypen**, wählen Sie **Computer** aus, und klicken Sie dann auf **OK**.  
  
6.  Geben Sie den Clientnamen hinzufügen, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie auf **OK** schließen die **DirectAccessClients** Dialogfeld "Eigenschaften", und schließen Sie **Active Directory-Benutzer und-Computer**.  
  
##### <a name="copy-and-then-apply-the-provisioning-package-to-the-client-computer"></a>Kopieren Sie aus, und klicken Sie dann wenden das Bereitstellungspaket auf den Clientcomputer an  
  
1.  Kopieren Sie das Paket, aus c:\files\provision.txt auf RAS-Servers an, an dem sie, um c:\provision\provision.txt auf dem Clientcomputer gespeichert wurde.  
  
2.  Klicken Sie auf dem Clientcomputer öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie dann den folgenden Befehl zum Hinzufügen zur Domäne anfordern:  
  
    ```  
    Djoin /requestodj /loadfile C:\provision\provision.txt /windowspath %windir% /localos  
    ```  
  
3.  Starten Sie den Clientcomputer neu. Der Computer wird mit der Domäne hinzugefügt werden. Nach dem Neustart wird der Client wird in die Domäne eingebunden sein und über eine Verbindung mit dem Unternehmensnetzwerk mit DirectAccess verfügen.  
  
## <a name="see-also"></a>Siehe auch  
[NetProvisionComputerAccount-Funktion](https://go.microsoft.com/fwlink/?LinkId=162426)  
[NetRequestOfflineDomainJoin-Funktion](https://go.microsoft.com/fwlink/?LinkId=162427)  
  


