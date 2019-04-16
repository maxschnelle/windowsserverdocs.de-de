---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: "AD DS-Installation und Seitenbeschreibung für den Assistenten zum Entfernen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fa023398822e79ca8c3e93d44bb1e87fc9190cee
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>AD DS-Installation und Seitenbeschreibung für den Assistenten zum Entfernen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält eine Beschreibung der Steuerelemente auf die folgenden Seiten des Assistenten, die die AD DS-Serverrolle und die Deinstallation im Server-Manager umfassen.  
  
-   [Bereitstellungskonfiguration](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)  
  
-   [Domänencontroller-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)  
  
-   [DNS-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)  
  
-   [RODC-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)  
  
-   [Weitere Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)  
  
-   [Pfade](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)  
  
-   [Vorbereitungsoptionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)  
  
-   [Optionen prüfen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)  
  
-   [Prüfung der erforderlichen Komponenten](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)  
  
-   [Ergebnisse](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)  
  
-   [Rolle Entfernungsanmeldeinformationen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)  
  
-   [Optionen zum Entfernen von AD DS und Warnungen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)  
  
-   [Neues Administratorkennwort](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)  
  
-   [Rolle Entfernungsauswahl bestätigen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)  
  
## <a name="BKMK_DepConfigPage"></a>Bereitstellungskonfiguration  
Server-Manager beginnt jede Domänencontrollerinstallation mit der **Bereitstellungskonfiguration** Seite. Ändern die restlichen Optionen und erforderlichen Feldern auf dieser Seite und den darauf folgenden Seiten, je nachdem, welcher, die Bereitstellungsvorgang Sie wählen. Wenn Sie eine neue Gesamtstruktur erstellen, z.B. die **Vorbereitungsoptionen** Seite wird nicht angezeigt, doch dies geschieht, wenn Sie den ersten Domänencontroller installieren, die Windows Server2012 in einer vorhandenen Gesamtstruktur oder Domäne ausgeführt wird.  
  
Einige Tests Überprüfungen werden auf dieser Seite und später im Rahmen der voraussetzungsüberprüfungen ausgeführt. Beispielsweise, wenn Sie versuchen, den ersten Windows Server2012-Domänencontroller in einer Gesamtstruktur, die Windows2000-Funktionsebene zu installieren, wird ein Fehler auf dieser Seite.  
  
Die folgenden Optionen angezeigt, wenn Sie eine neue Gesamtstruktur erstellen.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
-   Wenn Sie eine neue Gesamtstruktur erstellen, müssen Sie einen Namen für die Gesamtstruktur-Stammdomäne angeben. Name der Stammdomäne der Gesamtstruktur nicht möglich, einzelnen Bezeichnung bestehen (z.B. es muss "contoso.com" anstatt "Contoso"). Es muss zulässige DNS-domänennamenskonventionen verwenden. Sie können eine Internationalized Domain Name (IDN) angeben. Weitere Informationen zu DNS-domänennamenskonventionen finden Sie unter [KB 909264](https://support.microsoft.com/kb/909264).  
  
-   Erstellen Sie keine neue Active Directory-Gesamtstrukturen mit dem gleichen Namen wie Ihr externer DNS-Name. Wenn Ihre Internet-DNS-URL http://contoso.com ist, müssen Sie einen anderen Namen für Ihre interne Gesamtstruktur um künftige Kompatibilitätsprobleme zu vermeiden auswählen. Der Name sollte eindeutig und für Datenverkehr im Web, z.B. corp.contoso.com unwahrscheinlich sein.  
  
-   Sie müssen ein Mitglied der Gruppe "Administratoren" auf dem Server sein, in dem Sie eine neue Gesamtstruktur erstellen möchten.  
  
Weitere Informationen zur Vorgehensweise beim Erstellen einer Gesamtstruktur finden Sie unter [Installieren einer neuen Windows Server2012 Active Directory-Gesamtstruktur & 40; Level200 & 41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
Die folgenden Optionen angezeigt, wenn Sie eine neue Domäne erstellen.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)  
  
> [!NOTE]  
> Wenn Sie eine neue Domänenstruktur erstellen, müssen Sie den Namen der Stammdomäne der Gesamtstruktur anstelle der übergeordneten Domäne angeben, aber die restlichen Assistentenseiten und Optionen sind identisch.  
  
-   Klicken Sie auf **wählen**, navigieren Sie zu der übergeordneten Domäne oder der Active Directory-Struktur, oder geben Sie einen gültige übergeordnete Domäne oder einen Gesamtstrukturnamen ein. Geben Sie den Namen der neuen Domäne in **Name der neuen Domäne**.  
  
-   Strukturdomäne: Geben Sie einen gültigen, vollqualifizierten Stammdomänennamen an; der Name nicht möglich, einzelnen Bezeichnung bestehen und DNS-Namen domänenanforderungen verwenden muss.  
  
-   Untergeordnete Domäne: Geben Sie einen gültigen, einteilige untergeordneten Stammdomänennamen an; der Name muss DNS-Domäne Namen Anforderungen verwenden.  
  
-   Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten fordert Sie Anmeldeinformationen für die Domäne, wenn Ihre aktuellen Anmeldeinformationen nicht aus der Domäne sind. Klicken Sie auf **ändern** um Domänenanmeldeinformationen anzugeben.  
  
Weitere Informationen zum Erstellen einer Domäne finden Sie unter [Installieren einer neuen Windows Server2012 untergeordneten Active Directory oder Gesamtstrukturdomäne & 40; Level200 & 41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
Die folgenden Optionen angezeigt, wenn Sie einen neuen Domänencontroller zu einer vorhandenen Domäne hinzufügen.  
  
![AD DS-Installation](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)  
  
-   Klicken Sie auf **wählen**, navigieren Sie zu der Domäne, oder geben Sie einen gültigen Domänennamen ein.  
  
-   Server-Manager fordert Sie gültige Anmeldeinformationen bei Bedarf. Installieren eines zusätzlichen Domänencontrollers müssen Sie Mitglied der Gruppe "Domänen-Admins".  
  
    Darüber hinaus erfordert die Installation von des ersten Domänencontrollers, der Windows Server2012 in einer Gesamtstruktur ausgeführt wird, Anmeldeinformationen, die Gruppenmitgliedschaften in den Gruppen "Organisations-Admins" und "Schema-Admins umfassen. Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten fordert Sie später vor, wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften verfügen.  
  
Weitere Informationen zur Vorgehensweise beim Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne finden Sie unter [installieren Sie einen Windows Server2012-Domänencontrollerreplikats in einer vorhandenen Domäne & 40; Level200 & 41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_DCOptionsPage"></a>Domänencontroller-Optionen  
Wenn Sie eine neue Gesamtstruktur erstellen, hat die Domänencontroller-Optionen Seite dieser Optionen:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)  
  
-   Die Funktionsebenen der Gesamtstruktur und Domäne werden auf Windows Server2012 standardmäßig festgelegt.  
  
    Ein neues Feature zur Verfügung steht auf der Domänenfunktionsebene Windows Server2012: die Unterstützung für dynamische Zugriffssteuerung und Kerberos Armoring KDC-Richtlinie für administrative Vorlagen sind zwei Einstellungen (immer Ansprüche bereitstellen und Authentifizierungsanfragen), für die Windows Server2012 als Domänenfunktionsebene erforderlich. Weitere Informationen finden Sie unter "Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-Schutz" in [Neuigkeiten in Kerberos-Authentifizierung](https://technet.microsoft.com/library/hh831747.aspx).    
    Die Gesamtstrukturfunktionsebene Windows Server2012 bietet neuen Funktionen, aber es wird sichergestellt, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf die Domänenfunktionsebene Windows Server2012. Die Domänenfunktionsebene Windows Server2012 bietet keine neue weitere Funktionen außer der Unterstützung für dynamische Zugriffssteuerung und Kerberos Armoring, aber es wird sichergestellt, dass alle Domänencontroller in der Domäne mit Windows Server2012 ausgeführt wird. Weitere Informationen zu anderen Features, die auf verschiedenen Funktionsebenen verfügbar sind, finden Sie unter [Grundlegendes zur Active Directory-Domänendienste (AD DS) Functional Levels](../active-directory-functional-levels.md).  
  
    Neben den Funktionsebenen bietet ein Domänencontroller mit Windows Server2012 zusätzliche Features, die nicht auf einem Domänencontroller verfügbar sind, die eine frühere Version von Windows Server ausgeführt wird. Ein Domänencontroller mit Windows Server2012 kann z.B. für das Klonen virtueller Domänencontroller, verwendet werden, während ein Domänencontroller mit einer früheren Version von Windows Server kann nicht.  
  
-   DNS-Server ist standardmäßig ausgewählt, wenn Sie eine neue Gesamtstruktur erstellen. Der erste Domänencontroller in der Gesamtstruktur muss ein globaler Katalogserver (GC), und es nicht möglich, eine schreibgeschützte nur Domänencontroller (RODC).  
  
-   Das Kennwort des Directory Services-Wiederherstellungsmodus (DSRM) ist erforderlich, um zu einem Domänencontroller melden Sie sich bei dem AD DS nicht ausgeführt wird. Das Kennwort ein, das Sie angeben, muss die Kennwortrichtlinie auf dem Server, der standardmäßig nicht über ein sicheres Kennwort erfordert erfüllen; nur ein nicht leeres Kennwort. Wählen Sie immer ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase. Informationen zur Vorgehensweise beim Synchronisieren des DSRM-Kennworts mit dem Kennwort eines Domänenbenutzerkontos finden Sie unter [KB 961320](https://support.microsoft.com/kb/961320).  
  
Weitere Informationen zur Vorgehensweise beim Erstellen einer Gesamtstruktur finden Sie unter [Installieren einer neuen Windows Server2012 Active Directory-Gesamtstruktur & 40; Level200 & 41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
Wenn Sie eine untergeordnete Domäne erstellen, hat die Domänencontroller-Optionen Seite dieser Optionen:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)  
  
-   Die Standardeinstellung für der Domänenfunktionsebene ist Windows Server2012. Sie können einen anderen Wert angeben, der mindestens der Wert der Gesamtstrukturfunktionsebene oder höher ist.  
  
-   Die konfigurierbaren Domänencontrolleroptionen lauten **DNS-Server** und **globalen Katalog**; Sie können keine schreibgeschützten Domänencontroller als den ersten Domänencontroller in einer neuen Domäne konfigurieren.  
  
    Microsoft empfiehlt, dass alle Domänencontroller DNS und globale Katalogdienste für hohe Verfügbarkeit in verteilten Umgebungen, weshalb der Assistent diese Optionen standardmäßig aktiviert, die beim Erstellen einer neuen Domäne bieten.  
  
-   Die **Domänencontrolleroptionen** auf der Seite können Sie auswählen, die entsprechenden logischen Active Directory auch **Standortname** aus der Gesamtstrukturkonfiguration. Standardmäßig wird die Website mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, werden diesem Standort automatisch ausgewählt.  
  
    > [!IMPORTANT]  
    > Wenn der Server nicht zu einer Active Directory-Subnetz gehört und mehr als ein Standort vorhanden ist, wird keine Auswahl getroffen, und die **Weiter** Schaltfläche ist nicht verfügbar, bis Sie eine Website aus der Liste auswählen.  
  
Weitere Informationen zum Erstellen einer Domäne finden Sie unter [Installieren einer neuen Windows Server2012 untergeordneten Active Directory oder Gesamtstrukturdomäne & 40; Level200 & 41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
Wenn Sie einen Domänencontroller einer Domäne hinzufügen, hat die Domänencontroller-Optionen Seite dieser Optionen:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)  
  
-   Die konfigurierbaren Domänencontrolleroptionen lauten **DNS-Server** und **globalen Katalog**, und **Read-only-Domänencontroller**.  
  
    Microsoft empfiehlt, dass alle Domänencontroller bereitstellen, DNS und globale Katalogdienste für hohe Verfügbarkeit in verteilten Umgebungen, weshalb der Assistent diese Optionen standardmäßig aktiviert. Weitere Informationen zum Bereitstellen von RODCs finden Sie unter [Read-Only Domain Controller Planning and Deployment Guide](https://technet.microsoft.com/library/cc771744(v=WS.10).aspx).  
  
Weitere Informationen zur Vorgehensweise beim Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne finden Sie unter [installieren Sie einen Windows Server2012-Domänencontrollerreplikats in einer vorhandenen Domäne & 40; Level200 & 41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_DNSOptionsPage"></a>DNS-Optionen  
Wenn Sie die folgenden DNS-Server installieren **DNS-Optionen** Seite wird angezeigt:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)  
  
Bei der Installation von DNS-Server sollten Delegierungseinträge, die auf dem DNS-Server als autorisierend für die Zone verweisen, in der übergeordneten Domain Name System (DNS) Zone erstellt werden. Delegierungseinträge übertragen, und geben Sie die richtigen Verweise auf andere DNS-Server und Clients der neue Server, die für die neue Zone autorisierend vorgenommen werden. Diesen Ressourceneinträgen gehören die folgenden:  
  
-   Ein Namenserver (NS)-Ressourceneintrag für die Delegierung. Dieser Ressourceneintrag gibt bekannt, dass der Server mit dem Namen ns1.na.example.microsoft.com ein autorisierender Server für die delegierte untergeordnete Domäne ist.  
  
-   Einen Hostressourceneintrag (A oder AAAA) muss auch als Verbindungseintrag vorhanden sein, den Namen des Servers aufzulösen, die in der Namenserver (NS)-Ressourceneintrag seiner IP-Adresse angegeben wird. Der Prozess zur Auflösung des Hostnamens in diesem Ressourceneintrag dem delegierten DNS-Server in der Namenserver (NS)-Ressourceneintrag wird auch bezeichnet als "lieben kleben."  
  
Sie können das Active Directory Konfigurations-Assistenten Domänendienste automatisch erstellt haben. Der Assistent überprüft, dass die entsprechenden Einträge in der übergeordneten DNS-Zone vorhanden sind, klicken Sie auf **Weiter** auf die **Domänencontrolleroptionen** Seite. Wenn der Assistent nicht überprüfen kann, dass die Einträge in der übergeordneten Domäne vorhanden sind, wird der Assistent bietet Ihnen automatisch mit der Option zum Erstellen einer neuen DNS-Delegierung für eine neue Domäne (oder aktualisieren die vorhandene Delegierung), und fahren Sie mit der Installation des neuen Domänencontrollers.  
  
Alternativ können Sie diese DNS-Delegierungseinträge erstellen, bevor Sie die DNS-Server installieren. Öffnen Sie zum Erstellen einer zonendelegierung **DNS-Manager**mit der rechten Maustaste auf die übergeordnete Domäne, und klicken Sie dann auf **neue Delegierung**. Führen Sie die Schritteim Assistenten für neue Delegierung auf die Delegierung zu erstellen.  
  
Der Installationsvorgang versucht, erstellen die Delegierung, um sicherzustellen, dass Computer in anderen Domänen DNS-Abfragen für Hosts, einschließlich Domänencontrollern und Mitgliedscomputern in der DNS-Unterdomäne auflösen können. Beachten Sie, dass die Delegierungseinträge nur auf Microsoft DNS-Servern automatisch erstellt werden können. Wenn die übergeordnete DNS-Domänenzone auf Drittanbieter-DNS-Server wie BIND befindet, wird eine Warnung über einen Fehler beim Erstellen der DNS-Delegierungseinträge auf der Seite Voraussetzungen prüfen angezeigt. Weitere Informationen zu der Warnung finden Sie unter [bekannte Probleme beim Installieren von AD DS](https://technet.microsoft.com/library/cc754463(v=WS.10).aspx).  
  
Delegierungen zwischen der übergeordneten Domäne und der Unterdomäne, die höher gestuft können erstellt und vor oder nach der Installation überprüft werden. Es gibt keinen Grund, die Installation eines neuen Domänencontrollers zu verzögern, da Sie nicht erstellen oder die DNS-Delegierung aktualisieren.  
  
Weitere Informationen zur Delegierung finden Sie unter [Understanding Zone Delegation](https://go.microsoft.com/fwlink/?LinkId=164773) (https://go.microsoft.com/fwlink/?LinkId=164773). Wenn zonendelegierung nicht in Ihrer Situation möglich ist, sollten Sie andere Methoden zur Bereitstellung der Namensauflösung aus anderen Domänen auf den Hosts in der Domäne. Beispielsweise kann der DNS-Administrator einer anderen Domäne konfigurieren, bedingte Weiterleitung, Stubzonen oder sekundäre Zonen, um Namen in der Domäne zu beheben. Weitere Informationen finden Sie unter den folgenden Themen:  
  
-   [Grundlegendes zu Zonentypen](https://go.microsoft.com/fwlink/?LinkID=157399) (https://go.microsoft.com/fwlink/?LinkID=157399)  
  
-   [Grundlegendes zu Stubzonen](https://go.microsoft.com/fwlink/?LinkId=164776) (https://go.microsoft.com/fwlink/?LinkId=164776)  
  
-   [Grundlegendes zu Weiterleitungen](https://go.microsoft.com/fwlink/?LinkId=164778) (https://go.microsoft.com/fwlink/?LinkId=164778)  
  
## <a name="BKMK_RODCOptionsPage"></a>RODC-Optionen  
Die folgenden Optionen angezeigt, wenn Sie einen schreibgeschützten Domänencontroller (RODC) installieren.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)  
  
-   Delegierte Administratorkonten erhalten lokale Administratorberechtigungen auf den RODC. Diese Benutzer können mit den Berechtigungen des lokalen Computers Gruppe "Administratoren" ausgeführt werden. Sie sind keine Mitglieder der Domänen-Admins "oder" die Domäne integrierten Gruppe Administratoren. Diese Option ist nützlich für zweigstellenverwaltung ohne Vergabe von Administratorberechtigungen für die Domäne. Konfigurieren der Delegierung von Verwaltung ist nicht erforderlich. Weitere Informationen finden Sie unter [Administratorrollentrennung](https://technet.microsoft.com/library/cc753170(v=WS.10).aspx).  
  
-   Die Kennwortreplikationsrichtlinie fungiert als eine Zugriffssteuerungsliste (ACL). Es bestimmt, ob ein Kennwort von einem RODC zwischengespeichert werden sollen. Nachdem der RODC authentifizierte Benutzer oder Computer Anmeldung Anforderung empfängt, bezeichnet die Kennwortreplikationsrichtlinie bestimmt, ob das Kennwort für das Konto zwischengespeichert werden sollen. Das gleiche Konto können Sie effizienter darauf folgenden Anmeldungen ausführen.  
  
    Kennwort Replikation Richtlinie (PRP) werden die Konten, deren Kennwörter zwischengespeichert werden dürfen, und Konten, deren Kennwörter zwischengespeichert werden, explizit verweigert werden. Die Liste der Benutzer- und Computerkonten, die zwischengespeichert werden dürfen bedeutet nicht, dass die Kennwörter für diese Konten unbedingt in der RODC zwischengespeichert wurden. Ein Administrator kann, beispielsweise vorab die Konten angeben, die einem RODC zwischengespeichert werden. Auf diese Weise kann der RODC diese Konten authentifizieren, selbst wenn die WAN-Verbindung mit der nebenstandort offline ist.  
  
    Benutzer oder Computer, die nicht gestattet (auch implizit) oder abgelehnte ihr Kennwort nicht zwischenspeichern. Wenn diese Benutzer oder Computer nicht über Zugriff auf einen beschreibbaren Domänencontroller verfügen, können nicht sie AD DS bereitgestellte Ressourcen oder Funktionalitäten zugreifen. Weitere Informationen zur PRP finden Sie unter [Kennwortreplikationsrichtlinie](https://technet.microsoft.com/library/cc730883(v=ws.10).aspx). Weitere Informationen zum Verwalten der PRP finden Sie unter [Verwalten der Kennwortreplikationsrichtlinie](https://technet.microsoft.com/library/rodc-guidance-for-administering-the-password-replication-policy(v=ws.10).aspx).  
  
Weitere Informationen zum Installieren von RODCs finden Sie unter [Installieren von Windows Server2012 Active Directory Read-Only Domänencontroller & 40; RODC & 41; & 40; Level200 & 41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md).  
  
## <a name="BKMK_AdditionalOptionsPage"></a>Weitere Optionen  
Die folgende Option angezeigt wird, auf die **zusätzliche Optionen** Seite, wenn Sie eine neue Domäne erstellen:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)  
  
Die folgenden Optionen angezeigt, auf die **zusätzliche Optionen** Seite, wenn Sie einen zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)  
  
-   Sie können entweder einen Domänencontroller als Replikationsquelle angeben oder lassen Sie den Assistenten einen beliebigen Domänencontroller als Replikationsquelle auswählen.  
  
-   Sie können auch auswählen, installieren Sie den Domänencontroller mithilfe gesicherter Medien Installieren von Medium (IFM)-Option. Wenn das Installationsmedium lokal gespeichert ist die **Installieren von Medium** Option ermöglicht es Ihnen, um den Speicherort der Datei zu suchen. Die Option zum Durchsuchen ist nicht für eine Remote-Installation verfügbar. Klicken Sie auf **überprüfen, ob** um sicherzustellen, dass der angegebene Pfad gültiges Medium. Von der IFM-Option verwendete Medien müssen von einem anderen vorhandenen Windows Server2012-Computer nur mit Windows Server-Sicherung oder mit Ntdsutil.exe erstellt werden. Sie können ein Windows Server2008 R2 oder früheren Betriebssystem Erstellen von Medien für einen Windows Server2012-Domänencontroller. Wenn die Medien mit einem Systemschlüssel (Syskey) geschützt ist, fordert Server-Manager-Kennworts für das Abbild während der Überprüfung.  
  
Weitere Informationen zum Erstellen einer Domäne finden Sie unter [Installieren einer neuen Windows Server2012 untergeordneten Active Directory oder Gesamtstrukturdomäne & 40; Level200 & 41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md). Weitere Informationen zur Vorgehensweise beim Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne finden Sie unter [installieren Sie einen Windows Server2012-Domänencontrollerreplikats in einer vorhandenen Domäne & 40; Level200 & 41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_Paths"></a>Pfade  
Die folgenden Optionen angezeigt, auf die **Pfade** Seite.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)  
  
-   Die **Pfade** Seite können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle außer Kraft setzen und der SYSVOL-Freigabe. Die Standardspeicherorte befinden sich grundsätzlich in SystemRoot%.  
  
Geben Sie den Speicherort für die AD DS-Datenbank (NTDS.DIT), Protokolldateien und SYSVOL. Für eine lokale Installation können Sie zu dem Speicherort navigieren, in dem die Dateien gespeichert werden sollen.  
  
## <a name="BKMK_AdprepCreds"></a>Vorbereitungsoptionen  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)  
  
Wenn Sie nicht mit ausreichenden Berechtigungen zum Ausführen von adprep.exe-Befehle angemeldet sind und Adprep zum Abschließen der AD DS-Installation ausführen muss, werden Sie aufgefordert, Anmeldeinformationen zum Ausführen von adprep.exe anzugeben. Adprep muss ausführen, um den ersten Domänencontroller hinzufügen, der zu einer vorhandenen Domäne oder Gesamtstruktur Windows Server2012 ausgeführt wird. Genauer gesagt:  
  
-   Adprep /forestprep ausgeführt werden müssen, um den ersten Domänencontroller hinzufügen, die zu einer vorhandenen Gesamtstruktur Windows Server2012 ausgeführt wird. Dieser Befehl muss von einem Mitglied der Gruppe Organisations-Admins, der Gruppe Schema-Admins und Domänen-Admins der Domäne, die den Schemamaster hostet ausgeführt werden. Für diesen Befehl erfolgreich abgeschlossen muss Konnektivität zwischen dem Computer, in dem Sie den Befehl ausführen, und den Schemamaster für die Gesamtstruktur vorhanden sein.  
  
-   Adprep /domainprep ausgeführt werden müssen, um den ersten Domänencontroller hinzufügen, die Windows Server2012 zu einer vorhandenen Domäne ausgeführt wird. Dieser Befehl muss von einem Mitglied der Gruppe Domänen-Admins der Domäne ausgeführt werden, auf dem Sie den Domänencontroller installieren, der Windows Server2012 ausgeführt wird. Für diesen Befehl erfolgreich abgeschlossen muss Konnektivität zwischen dem Computer, in dem Sie den Befehl ausführen, und dem Infrastrukturmaster für die Domäne vorhanden sein.  
  
-   Adprep /rodcprep ausgeführt werden müssen, um den ersten RODC zu einer vorhandenen Gesamtstruktur hinzufügen. Dieser Befehl muss von einem Mitglied der Gruppe Organisations-Admins ausgeführt werden. Für diesen Befehl erfolgreich abgeschlossen muss Konnektivität zwischen dem Computer, in dem Sie den Befehl ausführen, und dem Infrastrukturmaster für jede Anwendungsverzeichnispartition in der Gesamtstruktur vorhanden sein.  
  
Weitere Informationen zu Adprep.exe finden Sie unter [Adprep.exe Integration](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep) und [Running Adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx).  
  
## <a name="BKMK_ViewInstallOptionsPage"></a>Optionen prüfen  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)  
  
-   Die **Optionen prüfen** Seite können Sie Ihre Einstellungen überprüfen und sicherstellen, dass sie Ihren Anforderungen entsprechen, bevor Sie die Installation zu starten. Dies ist nicht die letzte Gelegenheit, um die Installation mit Server-Manager zu beenden. Auf dieser Seite können einfach überprüfen und bestätigen Ihre Einstellungen, bevor Sie die Konfiguration fortsetzen.  
  
-   Die **Optionen prüfen** im Server-Manager bietet auch einen optionalen **Skript anzeigen**, um eine Unicode-Textdatei zu erstellen, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dadurch können Sie die Benutzeroberfläche des Server-Manager als Studio ein Windows PowerShell-Bereitstellung verwenden. Verwenden Sie die Dienste Konfigurations-Assistenten von Active Directory-Domäne, um Optionen konfigurieren, exportieren Sie die Konfiguration und den Assistenten abbrechen. Dieser Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt.  
  
## <a name="BKMK_PrerqCheckPage"></a>Prüfung der erforderlichen Komponenten  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)  
  
Die Warnungen, die auf dieser Seite angezeigt werden unter anderem:  
  
-   Domänencontroller, die Windows Server2008 oder höher ist die Standardeinstellung für "Kompatible Kryptografiealgorithmen zulassen mit Windows NT 4", die schwächere Kryptografiealgorithmen verhindert, beim Einrichten des sicheren Kanals Sitzungen dass. Weitere Informationen zu den möglichen Auswirkungen und dieses Problem zu umgehen, finden Sie im KB-Artikel [942564](https://support.microsoft.com/kb/942564).  
  
-   DNS-Delegierung konnte nicht erstellt oder aktualisiert werden. Weitere Informationen finden Sie unter [DNS-Optionen](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage).  
  
-   Die voraussetzungsüberprüfung sind WMI-Aufrufe erforderlich. Sie können fehlschlagen, wenn sie blockiert Regeln blockieren und einen RPC-Server zurücksenden nicht verfügbar Fehler.  
  
Weitere Informationen zu den spezifischen voraussetzungsprüfungen, die für die AD DS-Installation ausgeführt werden, finden Sie unter [Voraussetzungsüberprüfungen](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests).  
  
## <a name="BKMK_Results"></a>Ergebnisse  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)  
  
Auf dieser Seite können Sie die Ergebnisse der Installation überprüfen.  
  
Sie können auch auswählen, auf den Zielserver neu starten, nachdem der Assistent abgeschlossen ist, jedoch ist die Installation erfolgreich, des Servers immer Neustart erfolgt unabhängig davon, ob Sie diese Option auswählen. In einigen Fällen nach Abschluss des Assistenten auf einem Zielserver, die nicht der Domäne vor der Installation hinzugefügt wurde, kann der Systemstatus des Zielservers den Server nicht erreichbar ist im Netzwerk oder der Systemstatus kann verhindern, dass Sie über Berechtigungen zum Verwalten des Remoteservers verfügen.  
  
Wenn der Zielserver nicht in diesem Fall neu starten, müssen Sie manuell starten. Tools wie shutdown.exe oder Windows PowerShell können nicht neu. Sie können Remote Desktop Services anmelden und den Zielserver per Remoteverbindung Herunterfahren.  
  
## <a name="BKMK_RemovalCredsPage"></a>Rolle Entfernungsanmeldeinformationen  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)  
  
Herabstufungsoptionen konfiguriert ist, auf die **Anmeldeinformationen** Seite. Geben Sie die Anmeldeinformationen, die zum Durchführen der Herabstufung aus der folgenden Liste:  
  
-   Für die Herabstufung eines zusätzlichen Domänencontrollers sind Domänenadministrator-Anmeldeinformationen erforderlich. Auswählen von **Entfernen des Domänencontrollers erzwingen** stuft die Domänencontroller ohne die Metadaten des Domänencontrollerobjekts aus Active Directory zu entfernen.  
  
    > [!IMPORTANT]  
    > Wählen Sie diese Option, wenn der Domänencontroller keine mit anderen Domänencontrollern Verbindung kann und es ist nicht *keine angemessene Möglichkeit* zum Beheben dieses Netzwerkproblems. Erzwungene Herabstufung verbleibt der restlichen Domänencontroller in der Gesamtstruktur verwaiste Metadaten in Active Directory. Darüber hinaus sind für immer alle nicht replizierte Änderungen auf diesem Domänencontroller, z.B. Kennwörter oder neue Benutzerkonten, verloren. Verwaiste Metadaten sind die Hauptursache in einem erheblichen Prozentsatz der Microsoft kundendienstfälle für AD DS, Exchange, SQL und andere Software. Wenn Sie einen Domänencontroller zwangsweise herabstufen Sie *müssen* manuelle Metadatenbereinigung sofort ausführen. Überprüfen Sie die Schritte, [Bereinigen von Servermetadaten](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  
  
-   Organisations-Admins der Gruppenmitgliedschaft für die Herabstufung des letzten Domänencontrollers in einer Domäne erforderlich werden, da dies die Domäne selbst entfernt (Wenn dies die letzte Domäne in der Gesamtstruktur ist, wird dabei die Gesamtstruktur). Server-Manager darüber informiert, wenn der aktuelle Domänencontroller der letzte Domänencontroller in der Domäne ist. Wählen Sie **letzter Domänencontroller in der Domäne** zu bestätigen, dass Domänencontroller der letzte Domänencontroller in der Domäne ist.  
  
Weitere Informationen zum Entfernen von AD DS finden Sie unter [Entfernen von Active Directory-Domänendienste (Stufe 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) und [Herabstufen von Domänencontrollern und Domänen & 40; Level200 & 41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_RemovalOptionsPage"></a>Optionen zum Entfernen von AD DS und Warnungen  
Wenn Sie der Seite "Prüfung" Hilfe benötigen, finden Sie unter Optionen prüfen  
  
Wenn der Domänencontroller zusätzliche Rollen, wie z.B. DNS-Serverrolle oder globalen Katalogserver gehostet wird die folgende Warnseite angezeigt:  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)  
  
Klicken Sie auf **Entfernung fortsetzen** um zu bestätigen, dass die zusätzlichen Rollen nicht mehr verfügbar ist, bevor Sie klicken können **Weiter** um den Vorgang fortzusetzen.  
  
Wenn Sie das Entfernen eines Domänencontrollers erzwingen, werden alle Änderungen an Active Directory-Objekt, die nicht auf andere Domänencontroller in der Domäne repliziert wurden gelöscht. Darüber hinaus, wenn der Domänencontroller Betriebsmasterrollen, den globalen Katalog oder DNS-Serverrolle hostet, können wichtige Vorgänge in der Domäne und Gesamtstruktur wie folgt beeinträchtigt werden. Bevor Sie einen Domänencontroller, der eine beliebige Betriebsmasterrolle hostet entfernen, versuchen Sie, die Rolle auf einen anderen Domänencontroller zu übertragen. Ist dies nicht möglich, die Rolle nicht übertragen, entfernen Sie zuerst die Active Directory-Domänendienste von diesem Computer, und dann verwenden Sie Ntdsutil.exe, um die Rolle zu übernehmen. Verwenden Sie Ntdsutil, auf dem Domänencontroller, dem die Funktion übernommen werden sollen. Verwenden Sie möglichst einen aktuellen Replikationspartner am selben Standort wie dieser Domänencontroller befindet. Weitere Informationen zu übertragen und übernehmen von Betriebsmasterrollen finden Sie unter [Artikel 255504](https://go.microsoft.com/fwlink/?LinkId=80395) in der Microsoft Knowledge Base. Wenn der Assistent nicht bestimmen kann, wenn der Domänencontroller eine Betriebsmasterrolle hostet, führen Sie netdom.exe-Befehl, um zu bestimmen, ob dieser Domänencontroller Betriebsmasterrollen ausführt.  
  
-   Globaler Katalog: Möglicherweise müssen die Benutzer Probleme bei der Anmeldung bei Domänen in der Gesamtstruktur. Bevor Sie einen globaler Katalogserver entfernen, stellen Sie sicher, dass genügend globale Katalogserver in dieser Gesamtstruktur und der Standort zum Verarbeiten der benutzeranmeldungen befinden. Bei Bedarf einen weiteren globalen Katalogserver festlegen, und Aktualisieren von Clients und Anwendungen mit den neuen Informationen.  
  
-   DNS-Server: alle DNS-Daten, die in Active Directory-integrierte Zonen gespeichert werden, gehen verloren. Nach dem Entfernen von AD DS, DNS-Server nicht Namensauflösung für den DNS-Zonen ausführen, die Active Directory-integriert sind. Aus diesem Grund empfehlen wir, dass Sie die DNS-Konfiguration aller Computer aktualisieren, die derzeit auf die IP-Adresse des DNS-Server für die Namensauflösung der IP-Adresse eines neuen DNS-Server verweisen.  
  
-   Infrastrukturmaster: Clients in der Domäne haben möglicherweise Schwierigkeiten Objekte in anderen Domänen. Bevor Sie fortfahren, übertragen Sie die Infrastrukturmasterrolle auf einen Domänencontroller, der kein globaler Katalogserver ist.  
  
-   RID-Master: möglicherweise Probleme beim Erstellen neuer Benutzerkonten, Computerkonten und Sicherheitsgruppen. Bevor Sie fortfahren, übertragen Sie die RID-Masterrolle auf einen Domänencontroller in derselben Domäne wie dieser Domänencontroller befindet.  
  
-   Emulator des primären Domänencontrollers (PDC): Vorgänge, die vom PDC-Emulator ausgeführt werden, z.B. gruppenrichtlinienaktualisierungen und für Nicht-AD DS-Konten Kennwortzurücksetzungen nicht ordnungsgemäß funktionieren. Bevor Sie fortfahren, übertragen Sie die PDC-Emulatormasterrolle auf einen Domänencontroller, der in der gleichen Domäne wie dieser Domänencontroller ist.  
  
-   Schemamaster: Sie werden nicht mehr ändern des Schemas für diese Gesamtstruktur. Bevor Sie fortfahren, übertragen Sie die Schemamasterrolle auf einen Domänencontroller in der Stammdomäne der Gesamtstruktur.  
  
-   Domänennamenmaster: Sie werden nicht mehr in der Domänen hinzufügen oder Entfernen von Domänen aus dieser Gesamtstruktur können. Bevor Sie den Vorgang fortsetzen, übertragen Sie die Domänennamen-Masterrolle auf einen Domänencontroller in der Stammdomäne der Gesamtstruktur.  
  
-   Alle Anwendungsverzeichnispartitionen auf diesem Active Directory-Domänencontroller werden entfernt. Wenn ein Domänencontroller das letzte Replikat eine oder mehrere Anwendungsverzeichnispartitionen enthält nach Abschluss des Entfernungsvorgangs, ist diese Partitionen nicht mehr vorhanden.  
  
Beachten Sie, dass die Domäne nach der Deinstallation von Active Directory-Domänendienste vom letzten Domänencontroller in der Domäne nicht mehr vorhanden ist.  
  
Wenn der Domänencontroller ein DNS-Server, der zum Hosten der DNS-Zone delegiert wird ist, stellt die folgende Seite die Option zum Entfernen des DNS-Servers aus der DNS-zonendelegierung bereit.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)  
  
Weitere Informationen zum Entfernen von AD DS finden Sie unter [Entfernen von Active Directory-Domänendienste (Stufe 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) und [Herabstufen von Domänencontrollern und Domänen & 40; Level200 & 41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_NewAdminPwdPage"></a>Neues Administratorkennwort  
Die **Neues Administratorkennwort** Seite müssen Sie ein Kennwort für das integrierte lokale Administratorkonto des Computers, bereitstellen, nachdem die Herabstufung abgeschlossen und der Computer ein Domänenmitgliedsserver oder Arbeitsgruppencomputer ist.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)  
  
Weitere Informationen zum Entfernen von AD DS finden Sie unter [Entfernen von Active Directory-Domänendienste (Stufe 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) und [Herabstufen von Domänencontrollern und Domänen & 40; Level200 & 41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_ConfirmRoleRemovalPage"></a>Optionen prüfen  
Die **Optionen prüfen** Seite bietet Ihnen die Möglichkeit, die Konfigurationseinstellungen für die Herabstufung in ein Windows PowerShell-Skript exportieren, sodass Sie zusätzliche Herabstufungen automatisieren können. Klicken Sie auf **tiefer stufen** zum Entfernen von AD DS.  
  
![AD DS-Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)  
  


