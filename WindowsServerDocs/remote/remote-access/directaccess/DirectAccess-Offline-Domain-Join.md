---
title: DirectAccess-Offline-Domänenbeitritt
description: In diesem Handbuch werden die Schritte zum Ausführen eines Offline-Domänen Beitritts mit DirectAccess in Windows Server 2016 erläutert.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 55528736-6c19-40bd-99e8-5668169ef3c7
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 43f0c606f16af00797f0325b793d476e6c2892f8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815663"
---
# <a name="directaccess-offline-domain-join"></a>DirectAccess-Offline-Domänenbeitritt

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Handbuch werden die Schritte zum Ausführen eines Offline-Domänen Beitritts mit DirectAccess erläutert. Während eines Offline-Domänen Beitritts ist ein Computer so konfiguriert, dass er einer Domäne ohne physische oder VPN-Verbindung Beitritt.  
  
Das Handbuch umfasst folgende Abschnitte:  
  
- Übersicht über den Offline Domänen Beitritt  
  
- Anforderungen an den Offline-Domänen Beitritt
  
- Offline-Domänen Beitrittsprozess
  
- Schritte zum Durchführen eines Offline-Domänen Beitritts  
  
## <a name="offline-domain-join-overview"></a>Übersicht über den Offline Domänen Beitritt  
Die in Windows Server 2008 R2 eingeführten Domänen Controller enthalten ein Feature namens Offline-Domänen Beitritt. Mit dem Befehlszeilen-Hilfsprogramm Djoin. exe können Sie einen Computer einer Domäne hinzufügen, ohne physisch einen Domänen Controller zu kontaktieren, während der Domänen Beitritts Vorgang abgeschlossen ist. Die allgemeinen Schritte zur Verwendung von "Djoin. exe" lauten wie folgt:  
  
1.  Führen Sie **Djoin/Provision** aus, um die Metadaten des Computer Kontos zu erstellen. Bei der Ausgabe dieses Befehls handelt es sich um eine txt-Datei, die ein Base-64-codiertes BLOB enthält.  
  
2.  Führen Sie **Djoin/requestODJ** aus, um die Computer Konto Metadaten aus der txt-Datei in das Windows-Verzeichnis des Ziel Computers einzufügen.  
  
3.  Starten Sie den Zielcomputer neu, und der Computer wird der Domäne hinzugefügt.  
  
### <a name="offline-domain-join-with-directaccess-policies-scenario-overview"></a><a name="BKMK_ODJOverview"></a>Szenario "Offline-Domänen Beitritt mit DirectAccess-Richtlinien"  
Der DirectAccess-Offline-Domänen Beitritt ist ein Prozess, mit dem Computer, auf denen Windows Server 2016, Windows Server 2012, Windows 10 oder Windows 8 ausgeführt wird, einer Domäne beitreten können, ohne dass Sie physisch mit dem Unternehmensnetzwerk verbunden oder über VPN verbunden ist. Dadurch ist es möglich, Computer einer Domäne von Orten aus hinzuzufügen, an denen keine Verbindung mit einem Unternehmensnetzwerk besteht. Der Offline-Domänen Beitritt für DirectAccess bietet Clients DirectAccess-Richtlinien, um die Remote Bereitstellung zuzulassen.  
  
Bei einem Domänen Beitritt wird ein Computer Konto erstellt und eine Vertrauensstellung zwischen einem Computer mit einem Windows-Betriebssystem und einer Active Directory Domäne hergestellt.  
  
## <a name="prepare-for-offline-domain-join"></a><a name="BKMK_ODJRequirements"></a>Vorbereiten des Offline-Domänen Beitritts  
  
1.  Erstellen Sie das Computer Konto.  
  
2.  Inventarisieren Sie die Mitgliedschaft aller Sicherheitsgruppen, zu denen das Computer Konto gehört.  
  
3.  Erfassen Sie die erforderlichen Computer Zertifikate, Gruppenrichtlinien und Gruppenrichtlinien Objekte, die auf die neuen Clients angewendet werden sollen.  
  
. In den folgenden Abschnitten werden die Anforderungen an das Betriebssystem und die Anmelde Informationen für die Ausführung eines DirectAccess-Offline-Domänen Beitritts mithilfe von Djoin. exe erläutert  
  
### <a name="operating-system-requirements"></a>Anforderungen an das Betriebssystem  
Sie können Djoin. exe nur für DirectAccess auf Computern ausführen, auf denen Windows Server 2016, Windows Server 2012 oder Windows 8 ausgeführt wird. Auf dem Computer, auf dem Sie Djoin. exe ausführen, um Computer Kontodaten in AD DS bereitzustellen, muss Windows Server 2016, Windows 10, Windows Server 2012 oder Windows 8 ausgeführt werden. Auf dem Computer, den Sie der Domäne hinzufügen möchten, muss auch Windows Server 2016, Windows 10, Windows Server 2012 oder Windows 8 ausgeführt werden.  
  
### <a name="credential-requirements"></a>Anforderungen bezüglich der Anmeldeinformationen  
Zum Ausführen eines Offline-Domänen Beitritts müssen Sie über die erforderlichen Rechte zum Verknüpfen von Arbeitsstationen zur Domäne verfügen. Mitglieder der Gruppe "Domänen-Admins" verfügen standardmäßig über diese Rechte. Wenn Sie kein Mitglied der Gruppe "Domänen-Admins" sind, muss ein Mitglied der Gruppe "Domänen-Admins" eine der folgenden Aktionen ausführen, damit Sie Arbeitsstationen zur Domäne hinzufügen können:  
  
-   Verwenden Sie Gruppenrichtlinie, um die erforderlichen Benutzerrechte zu erteilen. Mit dieser Methode können Sie Computer im Container Standard Computer und in jeder Organisationseinheit erstellen, die später erstellt wird (wenn keine Zugriffs Steuerungs Einträge (ACEs) hinzugefügt werden).  
  
-   Bearbeiten Sie die Zugriffs Steuerungs Liste (ACL) des Containers "Standard Computer" für die Domäne, um Ihnen die richtigen Berechtigungen zu delegieren.  
  
-   Erstellen Sie eine Organisationseinheit, und bearbeiten Sie die ACL für diese Organisationseinheit, um Ihnen die Berechtigung zum **Erstellen** von untergeordneten Elementen zu erteilen Übergeben Sie den **/machineOU** -Parameter an den **Djoin/Provision** -Befehl.  
  
In den folgenden Verfahren wird gezeigt, wie Sie den Benutzerberechtigungen für Gruppenrichtlinie erteilen und wie Sie die richtigen Berechtigungen delegieren.  
  
#### <a name="granting-user-rights-to-join-workstations-to-the-domain"></a>Erteilen von Benutzerrechten zum Hinzufügen von Arbeitsstationen zur Domäne  
Mit dem Gruppenrichtlinien-Verwaltungskonsole (GPMC) können Sie die Domänen Richtlinie ändern oder eine neue Richtlinie mit Einstellungen erstellen, mit denen dem Benutzerrechte zum Hinzufügen von Arbeitsstationen zu einer Domäne erteilt werden.  
  
Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**oder einer entsprechenden Gruppe sein, um Benutzerrechte gewähren zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) (https://go.microsoft.com/fwlink/?LinkId=83477).   
  
###### <a name="to-grant-rights-to-join-workstations-to-a-domain"></a>So erteilen Sie Rechte zum Verknüpfen von Arbeitsstationen mit einer Domäne  
  
1.  Klicken Sie auf **Start**, dann auf **Verwaltung** und anschließend auf **Gruppenrichtlinienverwaltung**.  
  
2.  Doppelklicken Sie auf den Namen der Gesamtstruktur, doppelklicken Sie auf **Domänen**, doppelklicken Sie auf den Namen der Domäne, der Sie einen Computer hinzufügen möchten, klicken Sie mit der rechten Maustaste auf **Standard Domänen Richtlinie**, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Doppelklicken Sie in der Konsolen Struktur auf **Computer Konfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Windows-Einstellungen**, doppelklicken Sie auf **Sicherheitseinstellungen**, doppelklicken Sie auf **lokale Richtlinien**, und doppelklicken Sie dann auf Zuweisen von **Benutzerrechten**.  
  
4.  Doppelklicken Sie im Detail **Bereich auf Arbeitsstationen zur Domäne hinzufügen**.  
  
5.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinien Einstellungen definieren** , und klicken Sie dann auf **Benutzer oder Gruppe hinzufügen**.  
  
6.  Geben Sie den Namen des Kontos ein, für das Sie dem Benutzerrechte erteilen möchten, und klicken Sie dann zweimal auf **OK** .  
  
## <a name="offline-domain-join-process"></a><a name="BKMK_ODKSxS"></a>Offline-Domänen Beitrittsprozess  
Führen Sie Djoin. exe an einer Eingabeaufforderung mit erhöhten Rechten aus, um die Computer Konto Metadaten bereitzustellen. Wenn Sie den Bereitstellungs Befehl ausführen, werden die Metadaten des Computer Kontos in einer Binärdatei erstellt, die Sie als Teil des Befehls angeben.  
  
Weitere Informationen zur NetProvisionComputerAccount-Funktion, die zum Bereitstellen des Computer Kontos während eines Offline-Domänen Beitritts verwendet wird, finden Sie unter [NetProvisionComputerAccount-Funktion](https://go.microsoft.com/fwlink/?LinkId=162426) (https://go.microsoft.com/fwlink/?LinkId=162426). Weitere Informationen zur Funktion "nettrequestofflinedomainjoin", die lokal auf dem Zielcomputer ausgeführt wird, finden Sie unter " [nettrequestofflinedomainjoin](https://go.microsoft.com/fwlink/?LinkId=162427) "-Funktion (https://go.microsoft.com/fwlink/?LinkId=162427).  
  
## <a name="steps-for-performing-a-directaccess-offline-domain-join"></a><a name="BKMK_ODJSteps"></a>Schritte zum Durchführen eines DirectAccess-Offline-Domänen Beitritts  
Der Offline-Domänen Beitrittsprozess umfasst die folgenden Schritte:  
  
1.  Erstellen Sie ein neues Computer Konto für jeden der Remote Clients, und generieren Sie mithilfe des Befehls Djoin. exe von einem bereits in eine Domäne eingebundener Computer im Unternehmensnetzwerk ein Bereitstellungs Paket.  
  
2.  Hinzufügen des Client Computers zur Sicherheitsgruppe "directaccessclients"  
  
3.  Übertragen Sie das Bereitstellungs Paket sicher auf die Remote Computer, die der Domäne beitreten werden.  
  
4.  Wenden Sie das Bereitstellungs Paket an, und fügen Sie den Client der Domäne hinzu.  
  
5.  Starten Sie den Client neu, um den Domänen Beitritt abzuschließen und eine Verbindung herzustellen.  
  
Beim Erstellen des Bereitstellungs Pakets für den Client sind zwei Optionen zu beachten. Wenn Sie den Assistenten für die ersten Schritte zum Installieren von DirectAccess ohne PKI verwendet haben, sollten Sie unten Option 1 verwenden. Wenn Sie den erweiterten Setup-Assistenten zum Installieren von DirectAccess mit PKI verwendet haben, sollten Sie unten Option 2 verwenden.  
  
Führen Sie die folgenden Schritte aus, um den Offline-Domänen Beitritt auszuführen:  
  
##### <a name="option1-create-a-provisioning-package-for-the-client-without-pki"></a>Option1: Erstellen eines Bereitstellungs Pakets für den Client ohne PKI  
  
1.  Geben Sie an einer Eingabeaufforderung des Remote Zugriffs Servers den folgenden Befehl ein, um das Computer Konto bereitzustellen:  
  
    ```  
    Djoin /provision /domain <your domain name> /machine <remote machine name> /policynames DA Client GPO name /rootcacerts /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="option2-create-a-provisioning-package-for-the-client-with-pki"></a>Option2: Erstellen eines Bereitstellungs Pakets für den Client mit PKI  
  
1.  Geben Sie an einer Eingabeaufforderung des Remote Zugriffs Servers den folgenden Befehl ein, um das Computer Konto bereitzustellen:  
  
    ```  
    Djoin /provision /machine <remote machine name> /domain <Your Domain name> /policynames <DA Client GPO name> /certtemplate <Name of client computer cert template> /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="add-the-client-computer-to-the-directaccessclients-security-group"></a>Hinzufügen des Client Computers zur Sicherheitsgruppe "directaccessclients"  
  
1.  Geben Sie auf dem Domänen Controller auf dem Bildschirm **Start** den Wert **aktiv** ein, und wählen Sie **Active Directory Benutzer und Computer** von **apps** aus.  
  
2.  Erweitern Sie die Struktur unter Ihrer Domäne, und wählen Sie den Container **Benutzer** aus.  
  
3.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **directaccessclients**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
5.  Klicken Sie auf **Objekttypen**, wählen Sie **Computer** aus, und klicken Sie dann auf **OK**.  
  
6.  Geben Sie den hinzu zufügenden Client Namen ein, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie auf **OK** , um das Eigenschaften Dialogfeld von **directaccessclients** zu schließen, und schließen Sie dann **Active Directory Benutzer und Computer**.  
  
##### <a name="copy-and-then-apply-the-provisioning-package-to-the-client-computer"></a>Kopieren Sie das Bereitstellungs Paket, und wenden Sie es auf den Client Computer an.  
  
1.  Kopieren Sie das Bereitstellungs Paket aus c:\files\provision.txt auf dem Remote Zugriffs Server, auf dem es gespeichert wurde, auf dem Client Computer unter "c:\provision\provision.txt".  
  
2.  Öffnen Sie auf dem Client Computer eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie dann den folgenden Befehl ein, um den Domänen Beitritt anzufordern:  
  
    ```  
    Djoin /requestodj /loadfile C:\provision\provision.txt /windowspath %windir% /localos  
    ```  
  
3.  Starten Sie den Client Computer neu. Der Computer wird der Domäne hinzugefügt. Nach dem Neustart wird der Client der Domäne hinzugefügt und verfügt über eine Verbindung mit dem Unternehmensnetzwerk mit DirectAccess.  
  
## <a name="see-also"></a>Weitere Informationen  
[NetProvisionComputerAccount-Funktion](https://go.microsoft.com/fwlink/?LinkId=162426)  
[Nettrequestofflinedomainjoin-Funktion](https://go.microsoft.com/fwlink/?LinkId=162427)  
  


