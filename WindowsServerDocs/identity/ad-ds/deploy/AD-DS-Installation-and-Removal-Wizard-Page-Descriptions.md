---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: Seitenbeschreibungen für den Assistenten zum Installieren und Entfernen von AD DS
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 39d41b605db94931731f29aa25990672332c8056
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959428"
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>Seitenbeschreibungen für den Assistenten zum Installieren und Entfernen von AD DS

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält Beschreibungen zu den Steuerelementen auf den folgenden Assistentenseiten, die die Installation und das Entfernen der AD DS-Serverrolle in Server Manager umfassen.

-   [Bereitstellungskonfiguration](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)

-   [Domänencontrolleroptionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)

-   [DNS-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)

-   [RODC-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)

-   [Zusätzliche Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)

-   [Pfade](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)

-   [Vorbereitungsoptionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)

-   [Überprüfungs Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)

-   [Prüfung der erforderlichen Komponenten](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)

-   [Ergebnisse](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)

-   [Anmeldeinformationen zum Entfernen von Rollen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)

-   [Optionen und Warnungen zum Entfernen von AD DS](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)

-   [Neues Administratorkennwort](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)

-   [Auswahl zum Entfernen von Rollen bestätigen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)

## <a name="deployment-configuration"></a><a name="BKMK_DepConfigPage"></a>Bereitstellungs Konfiguration
In Server-Manager beginnt jede Domänencontrollerinstallation auf der Seite **Bereitstellungskonfiguration**. Die restlichen Optionen und erforderlichen Felder auf dieser Seite und den folgenden Seiten variieren in Abhängigkeit von dem von Ihnen ausgewählten Bereitstellungsvorgang. Wenn Sie z. b. eine neue Gesamtstruktur erstellen, wird die Seite **Vorbereitungs Optionen** nicht angezeigt. Dies geschieht jedoch, wenn Sie den ersten Domänen Controller installieren, auf dem Windows Server 2012 in einer vorhandenen Gesamtstruktur oder Domäne ausgeführt wird.

Auf dieser Seite werden einige Validierungstests ausgeführt. Diese Tests werden später im Rahmen der Voraussetzungsüberprüfungen wiederholt. Wenn Sie z. b. versuchen, den ersten Windows Server 2012-Domänen Controller in einer Gesamtstruktur mit Windows 2000-Funktionsebene zu installieren, wird ein Fehler auf dieser Seite angezeigt.

Beim Erstellen einer neuen Gesamtstruktur werden die folgenden Optionen angezeigt.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)

-   Beim Erstellen einer neuen Gesamtstruktur müssen Sie einen Namen für die Stammdomäne der Gesamtstruktur angeben. Der Name der Gesamtstruktur-Stamm Domäne kann nicht mit einer einzelnen Bezeichnung (z. b. "contoso.com" anstelle von "" in "") versehen werden. Es müssen zulässige DNS-Domänennamenskonventionen verwendet werden. Sie können einen internationalen Domänennamen (IDN) angeben. Weitere Informationen zu DNS-Domänennamenskonventionen finden Sie im [KB-Artikel 909264](https://support.microsoft.com/kb/909264).

-   Erstellen Sie keine neuen Active Directory-Gesamtstrukturen, die denselben Namen haben wie Ihr externer DNS-Name. Wenn Ihre Internet-DNS-URL beispielsweise "http: \/ /contoso.com" lautet, müssen Sie einen anderen Namen für die interne Gesamtstruktur auswählen, um zukünftige Kompatibilitätsprobleme zu vermeiden. Der Name sollte eindeutig und seine Verwendung für den Webdatenverkehr unwahrscheinlich sein, beispielsweise %%amp;quot;corp.contoso.com%%amp;quot;.

-   Auf dem Server, auf dem Sie eine neue Gesamtstruktur erstellen möchten, müssen Sie Mitglied der Administratorgruppe sein.

Weitere Informationen zum Erstellen einer Gesamtstruktur finden Sie unter [install a New Windows Server 2012 Active Directory Forest &#40;Level 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).

Beim Erstellen einer neuen Domäne werden die folgenden Optionen angezeigt.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)

> [!NOTE]
> Beim Erstellen einer neuen Gesamtstrukturdomäne müssen Sie anstelle der übergeordneten Domäne den Namen der Stammdomäne für die Gesamtstruktur angeben. Die restlichen Assistentenseiten und Optionen sind jedoch identisch.

-   Klicken Sie auf **Auswählen**, um zur übergeordneten Domäne oder zur Active Directory-Gesamtstruktur zu navigieren, oder geben Sie eine gültige übergeordnete Domäne oder einen Gesamtstrukturnamen ein. Geben Sie dann unter **Neuer Domänename** den Namen der neuen Domäne ein.

-   Strukturdomäne: geben Sie einen gültigen, vollqualifizierten Stammdomänennamen an; der Name darf nicht aus einer einzelnen Bezeichnung bestehen und muss die Anforderungen an den DNS-Domänennamen erfüllen.

-   Untergeordnete Domäne: geben Sie einen gültigen Namen für die untergeordnete Domäne an, der aus einer einzelnen Bezeichnung besteht; der Name muss die Anforderungen an den DNS-Domänennamen erfüllen.

-   Der Konfigurations-Assistent für die Active Directory-Domänendienste fordert Sie zur Eingabe der Domänenanmeldeinformationen auf, wenn Ihre aktuellen Anmeldeinformationen nicht zu der Domäne gehören. Klicken Sie auf **Ändern**, um Domänenanmeldeinformationen anzugeben.

Weitere Informationen zum Erstellen einer Domäne finden Sie unter [install a New Windows Server 2012 Active Directory child or Tree Domain &#40;Level 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).

Beim Hinzufügen eines neuen Domänencontrollers zu einer vorhandenen Domäne werden die folgenden Optionen angezeigt.

![AD DS Installation](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)

-   Klicken Sie auf **Auswählen**, um zu der Domäne zu navigieren, oder geben Sie einen gültigen Domänennamen ein.

-   Server-Manager fordert Sie ggf. zur Eingabe gültiger Anmeldeinformationen auf. Für das Installieren eines zusätzlichen Domänencontrollers ist die Mitgliedschaft in der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; erforderlich.

    Außerdem sind für die Installation des ersten Domänen Controllers, auf dem Windows Server 2012 in einer Gesamtstruktur ausgeführt wird, Anmelde Informationen erforderlich, die Gruppenmitgliedschaften in den Gruppen Organisations-Admins und Schema-Admins enthalten. Wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften aufweisen, wird später vom Konfigurations-Assistenten für die Active Directory-Domänendienste eine Eingabeaufforderung ausgegeben.

Weitere Informationen zum Hinzufügen eines Domänen Controllers zu einer vorhandenen Domäne finden Sie unter [Installieren eines Windows Server 2012-Replikat Domänen Controllers in einer vorhandenen Domäne &#40;Ebene 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).

## <a name="domain-controller-options"></a><a name="BKMK_DCOptionsPage"></a>Domänen Controller Optionen
Wenn Sie eine neue Gesamtstruktur erstellen, werden auf der Seite %%amp;quot;Domänencontrolleroptionen%%amp;quot; die folgenden Optionen angezeigt:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)

-   Die Gesamtstruktur-und Domänen Funktionsebenen werden standardmäßig auf Windows Server 2012 festgelegt.

    Auf der Windows Server 2012-Domänen Funktionsebene ist ein neues Feature verfügbar: die Unterstützung für dynamische Access Control und die Kerberos armoring-Richtlinie für administrative Vorlagen für virtuelle KDC-Vorlagen verfügt über zwei Einstellungen (immer Ansprüche bereitstellen und nicht hochgerüstete Authentifizierungsanforderungen fehlschlagen), für die die Domänen Funktionsebene 2012 Windows Weitere Informationen finden Sie unter "Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring" unter [Neuerungen bei der Kerberos-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11)).
    Die Windows Server 2012-Gesamtstruktur Funktionsebene bietet keine neuen Features, stellt jedoch sicher, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf der Domänen Funktionsebene von Windows Server 2012 ausgeführt werden. Die Domänen Funktionsebene Windows Server 2012 bietet neben der Unterstützung für dynamische Access Control und Kerberos armoring keine neuen anderen Features, stellt jedoch sicher, dass alle Domänen Controller in der Domäne Windows Server 2012 ausführen. Weitere Informationen zu weiteren Features, die auf verschiedenen Funktionsebenen verfügbar sind, finden Sie unter [Understanding Active Directory Domain Services (AD DS) Functional Levels](../active-directory-functional-levels.md).

    Neben Funktionsebenen bietet ein Domänen Controller, auf dem Windows Server 2012 ausgeführt wird, zusätzliche Features, die auf einem Domänen Controller, auf dem eine frühere Version von Windows Server ausgeführt wird, nicht verfügbar sind. Beispielsweise kann ein Domänen Controller mit Windows Server 2012 zum Klonen virtueller Domänen Controller verwendet werden, während ein Domänen Controller, auf dem eine frühere Version von Windows Server ausgeführt wird, nicht ausgeführt werden kann.

-   Beim Erstellen einer neuen Gesamtstruktur ist standardmäßig DNS-Server ausgewählt. Bei dem ersten Domänencontroller in der Gesamtstruktur muss es sich um einen globalen Katalogserver handeln. Schreibgeschützte Domänencontroller (Read Only Domain Controller, RODC) sind dabei nicht zulässig.

-   Für die Anmeldung bei einem Domänencontroller, auf dem AD DS nicht ausgeführt wird, ist das Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) erforderlich. Das von Ihnen angegebene Kennwort muss der auf den Server angewendeten Kennwortrichtlinie entsprechen, laut der standardmäßig kein sicheres, sondern lediglich ein nicht leeres Kennwort erforderlich ist. Wählen Sie stets ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase aus. Informationen zum Synchronisieren des DSRM-Kennworts mit dem Kennwort eines Domänenbenutzerkontos finden Sie im [KB-Artikel 961320](https://support.microsoft.com/kb/961320).

Weitere Informationen zum Erstellen einer Gesamtstruktur finden Sie unter [install a New Windows Server 2012 Active Directory Forest &#40;Level 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).

Wenn Sie eine untergeordnete Domäne erstellen, werden auf der Seite %%amp;quot;Domänencontrolleroptionen%%amp;quot; die folgenden Optionen angezeigt:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)

-   Die Domänen Funktionsebene wird standardmäßig auf Windows Server 2012 festgelegt. Sie können einen beliebigen anderen Wert angeben, der mindestens dem Wert der Gesamtstrukturfunktionsebene oder höher entspricht.

-   Die konfigurierbaren Domänencontrolleroptionen lauten **DNS-Server** und **Globaler Katalog**. Das Konfigurieren eines schreibgeschützten Domänencontrollers als ersten Domänencontroller in einer neuen Domäne ist nicht möglich.

    Für eine hohe Verfügbarkeit in verteilten Umgebungen empfiehlt Microsoft, dass alle Domänencontroller DNS und globale Katalogdienste bereitstellen. Dies ist die Ursache dafür, dass der Assistent diese Optionen beim Erstellen einer neuen Domäne standardmäßig aktiviert.

-   Auf der Seite **Domänencontrolleroptionen** können Sie unter **Standortname** den entsprechenden logischen Standortnamen für Active Directory in der Gesamtstrukturkonfiguration auswählen. Standardmäßig ist der Standortname mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, wird dieser automatisch ausgewählt.

    > [!IMPORTANT]
    > Wenn der Server zu keinem Active Directory-Subnetz gehört und mehrere Standorte vorhanden sind, wird keine Auswahl getroffen, und die Schaltfläche **Weiter** ist erst wieder verfügbar, nachdem Sie in der Liste einen Standort ausgewählt haben.

Weitere Informationen zum Erstellen einer Domäne finden Sie unter [install a New Windows Server 2012 Active Directory child or Tree Domain &#40;Level 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).

Wenn Sie einer Domäne einen Domänencontroller hinzufügen, werden auf der Seite %%amp;quot;Domänencontrolleroptionen%%amp;quot; die folgenden Optionen angezeigt:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)

-   Die konfigurierbaren Domänencontrolleroptionen lauten **DNS-Server** und **Globaler Katalog** und **Schreibgeschützter Domänencontroller**.

    Für eine hohe Verfügbarkeit in verteilten Umgebungen empfiehlt Microsoft, dass alle Domänencontroller DNS und globale Katalogdienste bereitstellen. Dies ist die Ursache dafür, dass der Assistent diese Optionen standardmäßig aktiviert. Weitere Informationen zum Bereitstellen von RODCs finden Sie im [Planungs- und Bereitstellungshandbuch für schreibgeschützte Domänencontroller](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771744(v=ws.10)).

Weitere Informationen zum Hinzufügen eines Domänen Controllers zu einer vorhandenen Domäne finden Sie unter [Installieren eines Windows Server 2012-Replikat Domänen Controllers in einer vorhandenen Domäne &#40;Ebene 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).

## <a name="dns-options"></a><a name="BKMK_DNSOptionsPage"></a>DNS-Optionen
Wenn Sie DNS-Server installieren, wird die folgende Seite mit **DNS-Optionen** angezeigt:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)

Beim Installieren von DNS-Server sollten Delegierungseinträge, die auf den DNS-Server als autorisierend für die Zone verweisen, in der übergeordneten DNS-Zone (Domain Name System) erstellt werden. Delegierungseinträge übertragen die Namensauflösungsautorität und stellen richtige Verweise auf andere DNS-Server und die Clients der neuen Server bereit, die als autorisierende Server für die neue Zone verwendet werden. Zu diesen Ressourceneinträgen gehören die Folgenden:

-   Ein Namenserver-Ressourceneintrag (NS) zur Ausführung der Delegierung. Dieser Ressourceneintrag gibt bekannt, dass der Server ns1.na.example.microsoft.com ein autorisierender Server für die delegierte untergeordnete Domäne ist.

-   Ein Host-(A-oder AAAA)-Ressourcen Daten Satz muss vorhanden sein, um den Namen des Servers aufzulösen, der im Ressourcen Daten Satz des Namen Servers (NS) für die zugehörige IP-Adresse angegeben ist. Der Prozess zur Auflösung des Hostnamens in diesem Ressourceneintrag für den delegierten DNS-Server im Namenserver-Ressourceneintrag (NS) wird manchmal auch als Verbindungsverfolgung bezeichnet.

Sie können auch die automatische Erstellung durch den Konfigurations-Assistenten für die Active Directory-Domänendienste festlegen. Nachdem Sie auf der Seite **Domänencontrolleroptionen** auf **Weiter** geklickt haben, überprüft der Assistent, ob die entsprechenden Einträge in der übergeordneten DNS-Zone vorhanden sind. Wenn der Assistent nicht überprüfen kann, ob die Einträge in der übergeordneten Domäne vorhanden sind, bietet er Ihnen die Möglichkeit, automatisch eine neue DNS-Delegierung für eine neue Domäne zu erstellen (oder die vorhandene Delegierung zu aktualisieren) und den Vorgang mit der Installation des neuen Domänencontrollers fortzusetzen.

Alternativ können Sie diese DNS-Delegierungseinträge vor dem Installieren von DNS-Server erstellen. Zum Erstellen einer Zonendelegierung öffnen Sie den **DNS-Manager**, klicken Sie mit der rechten Maustaste auf die übergeordnete Domäne, und klicken Sie dann auf **Neue Delegierung**. Folgen Sie den Schritten im Assistenten zum Erstellen neuer Delegierungen, um die Delegierung zu erstellen.

Der Installationsvorgang versucht, die Delegierung zu erstellen, um sicherzustellen, dass Computer in anderen Domänen DNS-Abfragen für Hosts in der DNS-Unterdomäne auflösen können, einschließlich Domänencontrollern und Mitgliedscomputern. Beachten Sie, dass die Delegierungseinträge nur auf Microsoft DNS-Servern automatisch erstellt werden können. Wenn sich die übergeordnete DNS-Domänenzone auf DNS-Servern von Drittanbietern wie BIND befindet, wird auf der Seite %%amp;quot; Voraussetzungsüberprüfung%%amp;quot; eine Warnung über einen Fehler beim Erstellen der DNS-Delegierungseinträge angezeigt. Weitere Informationen zu der Warnung finden Sie unter [Bekannte Probleme beim Installieren von AD DS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754463(v=ws.10)).

Delegierungen zwischen der übergeordneten Domäne und der Unterdomäne, die höher gestuft wird, können vor oder nach der Installation erstellt und überprüft werden. Es besteht kein Grund zur Verzögerung der Installation eines neuen Domänencontrollers, da Sie die DNS-Delegierung nicht erstellen oder aktualisieren können.

Weitere Informationen zur Delegierung finden Sie Untergrund Legendes zur [Zonen Delegierung](https://go.microsoft.com/fwlink/?LinkId=164773) ( https://go.microsoft.com/fwlink/?LinkId=164773) . Wenn in der momentanen Situation keine Zonendelegierung möglich ist, können Sie ggf. andere Methoden zur Bereitstellung der Namensauflösung von anderen Domänen zu den Hosts in der Domäne in Betracht ziehen. Der DNS-Administrator einer anderen Domäne kann z. B. bedingte Weiterleitung, Stubzonen oder sekundäre Zonen konfigurieren, um Namen in der Domäne aufzulösen. Weitere Informationen finden Sie unter den folgenden Themen:

-   Grundlegendes zu [Zonen Typen](https://go.microsoft.com/fwlink/?LinkID=157399) (https://go.microsoft.com/fwlink/?LinkID=157399)

-   Grundlegendes zu [Stub-Zonen](https://go.microsoft.com/fwlink/?LinkId=164776) (https://go.microsoft.com/fwlink/?LinkId=164776)

-   Grundlegendes zu weiter [Leitungen (](https://go.microsoft.com/fwlink/?LinkId=164778)https://go.microsoft.com/fwlink/?LinkId=164778)

## <a name="rodc-options"></a><a name="BKMK_RODCOptionsPage"></a>RODC-Optionen
Beim Installieren eines schreibgeschützten Domänencontrollers (Read-Only Domain Controller, RODC) werden die folgenden Optionen angezeigt.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)

-   Delegierte Administratorkonten erhalten für den RODC lokale Administratorberechtigungen. Diese Benutzer können mit rechten arbeiten, die der Administrator Gruppe des lokalen Computers entsprechen. Sie sind keine Mitglieder der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder der in die Domäne integrierten Gruppe %%amp;quot;Administratoren%%amp;quot;. Diese Option ist für die Delegierung der Zweigstellenverwaltung ohne Vergabe von Administratorberechtigungen für die Domäne hilfreich. Das Konfigurieren der Delegierung von Administratoren ist nicht erforderlich. Weitere Informationen finden Sie unter [Administratorrollentrennung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753170(v=ws.10)).

-   Die Kennwortreplikationsrichtlinie fungiert als Zugriffssteuerungsliste (Access Control List, ACL). Mit ihr wird bestimmt, ob ein Kennwort von einem RODC zwischengespeichert werden darf. Nachdem der RODC eine Anmeldeanforderung für einen authentifizierten Benutzer oder Computer empfangen hat, bezieht er sich auf die Kennwortreplikationsrichtlinie, um zu bestimmen, ob das Kennwort für das Konto zwischengespeichert werden soll. Anschließend können weitere Anmeldungen bei dem jeweiligen Konto effizienter ausgeführt werden.

    In der Kennwortreplikationsrichtlinie (Password Replication Policy, PRP) werden neben den Konten, deren Kennwörter zwischengespeichert werden dürfen, auch die Konten aufgelistet, für die das Zwischenspeichern der zugehörigen Kennwörter explizit verweigert wird. Die Liste der Benutzer- und Computerkonten, die zwischengespeichert werden dürfen, setzt nicht voraus, dass die Kennwörter zu diesen Konten zwingenderweise vom RODC zwischengespeichert wurden. Ein Administrator kann beispielsweise vorab die Konten angeben, die von einem RODC zwischengespeichert werden. Auf diese Art und Weise kann der RODC diese Konten auch dann authentifizieren, wenn der WAN-Link zu dem Nebenstandort offline ist.

    Benutzer oder Computer, denen der Vorgang nicht gestattet (auch implizit) oder sogar verweigert wird, können ihr Kennwort nicht zwischenspeichern. Wenn diese Benutzer oder Computer keinen Zugriff auf einen beschreibbaren Domänencontroller haben, können sie nicht auf von AD DS bereitgestellte Ressourcen oder Funktionalitäten zugreifen. Weitere Informationen zur PRP finden Sie unter [Kennwortreplikationsrichtlinie](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730883(v=ws.10)). Weitere Informationen zum Verwalten der PRP finden Sie unter [Verwalten der Kennwortreplikationsrichtlinie](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754646(v=ws.10)).

Weitere Informationen zum Installieren von RODCs finden [Sie unter Installieren eines Windows Server 2012 Active Directory schreibgeschützten Domänen Controllers &#40;RODC&#41; &#40;Ebene 200&#41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md).

## <a name="additional-options"></a><a name="BKMK_AdditionalOptionsPage"></a>Zusätzliche Optionen
Die folgende Option wird auf der Seite **Zusätzliche Optionen** angezeigt, wenn Sie eine neue Domäne erstellen:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)

Die folgenden Optionen werden auf der Seite **Zusätzliche Optionen** angezeigt, wenn Sie in einer vorhandenen Domäne einen zusätzlichen Domänencontroller installieren:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)

-   Sie können entweder einen Domänencontroller als Replikationsquelle angeben oder zulassen, dass der Assistent einen beliebigen Domänencontroller als Replikationsquelle auswählt.

-   Sie können auch festlegen, dass der Domänencontroller mithilfe gesicherter Medien und der Option %%amp;quot;Installieren von Medium%%amp;quot; (Install from Media, IFM) installiert wird. Wenn das Installationsmedium lokal gespeichert ist, können Sie mithilfe der Option **Installieren von Medium** zum Speicherort der Datei navigieren. Die Option zum Durchsuchen ist bei einer Remoteinstallation nicht verfügbar. Wenn Sie sicherstellen möchten, dass es sich bei dem angegebenen Pfad um ein gültiges Medium handelt, können Sie auf **Überprüfen** klicken. Medien, die von der IFM-Option verwendet werden, müssen mit Windows Server-Sicherung oder Ntdsutil.exe von einem anderen vorhandenen Windows Server 2012-Computer erstellt werden. zum Erstellen von Medien für einen Windows Server 2012-Domänen Controller können Sie kein Windows Server 2008 R2 oder ein früheres Betriebssystem verwenden. Wenn die Medien mit einem Systemschlüssel (SYSKEY) geschützt sind, werden Sie während der Überprüfung von Server-Manager zur Eingabe des Kennworts für das Abbild aufgefordert.

Weitere Informationen zum Erstellen einer Domäne finden Sie unter [install a New Windows Server 2012 Active Directory child or Tree Domain &#40;Level 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md). Weitere Informationen zum Hinzufügen eines Domänen Controllers zu einer vorhandenen Domäne finden Sie unter [Installieren eines Windows Server 2012-Replikat Domänen Controllers in einer vorhandenen Domäne &#40;Ebene 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).

## <a name="paths"></a><a name="BKMK_Paths"></a>Pfade
Auf der Seite **Pfade** werden die folgenden Optionen angezeigt.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)

-   Auf der Seite **Pfade** können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich unter %systemroot%.

Geben Sie den Speicherort für die AD DS-Datenbank (NTDS.DIT), die Protokolldateien und für SYSVOL an. Bei einer lokalen Installation können Sie zu dem Speicherort navigieren, unter dem Sie die Dateien speichern möchten.

## <a name="preparation-options"></a><a name="BKMK_AdprepCreds"></a>Vorbereitungsoptionen
![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)

Wenn Sie derzeit nicht mit den zum Ausführen von adprep.exe-Befehlen erforderlichen Anmeldeinformationen angemeldet sind und Adprep zum Abschließen der AD DS-Installation erforderlich ist, werden Sie zum Angeben von Anmeldeinformationen aufgefordert, mit denen %%amp;quot;adprep.exe%%amp;quot; ausgeführt werden kann. Zum Hinzufügen des ersten Domänen Controllers, auf dem Windows Server 2012 ausgeführt wird, zu einer vorhandenen Domäne oder Gesamtstruktur muss adprep ausgeführt werden. Dies gilt insbesondere in folgenden Fällen:

-   Adprep/forestprep muss ausgeführt werden, um den ersten Domänen Controller, auf dem Windows Server 2012 ausgeführt wird, einer vorhandenen Gesamtstruktur hinzuzufügen. Dieser Befehl muss von einem Mitglied der Gruppe %%amp;quot;Organisations-Admins%%amp;quot;, %%amp;quot;Schema-Admins%%amp;quot; und %%amp;quot;Domänen-Admins%%amp;quot; der Domäne ausgeführt werden, die den Schemamaster enthält. Damit dieser Befehl erfolgreich abgeschlossen werden kann, muss zwischen dem Computer, auf dem Sie den Befehl ausführen, und dem Schemamaster für die Gesamtstruktur eine Verbindung bestehen.

-   Adprep/domainprep muss ausgeführt werden, um den ersten Domänen Controller, auf dem Windows Server 2012 ausgeführt wird, einer vorhandenen Domäne hinzuzufügen. Dieser Befehl muss von einem Mitglied der Gruppe Domänen-Admins der Domäne ausgeführt werden, in der Sie den Domänen Controller installieren, auf dem Windows Server 2012 ausgeführt wird. Damit dieser Befehl erfolgreich abgeschlossen werden kann, muss zwischen dem Computer, auf dem Sie den Befehl ausführen, und dem Infrastrukturmaster für die Domäne eine Verbindung bestehen.

-   Zum Hinzufügen des ersten RODC zu einer vorhandenen Gesamtstruktur ist die Ausführung von adprep/rodcprep erforderlich. Dieser Befehl muss von einem Mitglied der Gruppe %%amp;quot;Organisation-Admins%%amp;quot; ausgeführt werden. Damit dieser Befehl erfolgreich abgeschlossen werden kann, muss zwischen dem Computer, auf dem Sie den Befehl ausführen, und dem Infrastrukturmaster für die einzelnen Anwendungsverzeichnispartitionen in der Gesamtstruktur eine Verbindung bestehen.

Weitere Informationen zu %%amp;quot;Adprep.exe%%amp;quot; finden Sie unter [Integration von %%amp;quot;Adprep.exe%%amp;quot;](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep) und [Ausführen von %%amp;quot;Adprep.exe%%amp;quot;](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)).

## <a name="review-options"></a><a name="BKMK_ViewInstallOptionsPage"></a>Überprüfungs Optionen
![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)

-   Auf der Seite **Optionen prüfen** können Sie vor dem Starten der Installation Ihre Einstellungen validieren und sicherstellen, dass Ihre Anforderungen erfüllt werden. Dies ist jedoch nicht die letzte Möglichkeit, um die Installation mit Server-Manager zu stoppen. Diese Seite ermöglicht Ihnen lediglich das Überprüfen und Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetzen.

-   Die Seite **Optionen prüfen** im Server-Manager bietet zudem die optionale Schaltfläche **Skript anzeigen** zum Erstellen einer Unicode-Textdatei, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dies ermöglicht Ihnen die Verwendung der grafischen Oberfläche von Server-Manager als Windows PowerShell-Bereitstellungsstudio. Mithilfe des Konfigurations-Assistenten für die Active Directory-Domänendienste können Sie Optionen konfigurieren, die Konfiguration exportieren und den Assistenten abbrechen. Bei diesem Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt.

## <a name="prerequisites-check"></a><a name="BKMK_PrerqCheckPage"></a>Voraussetzungs Prüfung
![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)

Einige der auf dieser Seite angezeigten Warnungen lauten wie folgt:

-   Domänen Controller, auf denen Windows Server 2008 oder höher ausgeführt wird, verfügen über eine Standardeinstellung für "mit Windows NT 4 kompatible Kryptografiealgorithmen zulassen", die schwächere Kryptografiealgorithmen beim Einrichten sicherer Kanal Sitzungen verhindert. Weitere Informationen zu den möglichen Auswirkungen und zu einem Workaround finden Sie im KB-Artikel [942564](https://support.microsoft.com/kb/942564).

-   Die DNS-Delegierung konnte nicht erstellt oder aktualisiert werden. Weitere Informationen finden Sie unter [DNS-Optionen](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage).

-   Für die Voraussetzungsüberprüfung sind WMI-Aufrufe erforderlich. Diese können erfolglos sein, wenn sie durch Firewallblockierungsregeln blockiert werden, und sie können eine Fehlermeldung mit dem Hinweis zurückgeben, dass der RPC-Server nicht verfügbar ist.

Weitere Informationen zu den für die AD DS-Installation spezifischen Voraussetzungsüberprüfungen finden Sie unter [Voraussetzungsüberprüfungen](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests).

## <a name="results"></a><a name="BKMK_Results"></a>Ergebnisse
![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)

Auf dieser Seite können Sie die Ergebnisse der Installation überprüfen.

Zudem können Sie festlegen, dass der Zielserver nach Abschluss des Assistenten neu gestartet wird. Bei erfolgreichem Abschluss der Installation wird der Server jedoch generell neu gestartet. Dabei ist es unerheblich, ob Sie diese Option auswählen oder nicht. Nach Abschluss des Assistenten auf einem Zielserver, der vor der Installation der Domäne nicht hinzugefügt wurde, kann der Systemstatus des Zielservers in einigen Fällen dazu führen, dass der Server im Netzwerk nicht erreichbar ist. Der Systemstatus kann auch verhindern, dass Sie über Berechtigungen zum Verwalten des Remoteservers verfügen.

Wenn der Neustart des Zielservers in diesem Fall nicht gelingt, müssen Sie ihn manuell neu starten. Ein Neustart mithilfe von Tools wie %%amp;quot;shutdown.exe%%amp;quot; oder Windows PowerShell ist nicht möglich. Über die Remotedesktopdienste können Sie sich anmelden und den Zielserver per Remoteverbindung herunterfahren.

## <a name="role-removal-credentials"></a><a name="BKMK_RemovalCredsPage"></a>Anmeldeinformationen zum Entfernen von Rollen
![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)

Auf der Seite **Anmeldeinformationen** werden Herabstufungsoptionen konfiguriert. Geben Sie in der folgenden Liste die zum Ausführen der Herabstufung erforderlichen Anmeldeinformationen an:

-   Für die Herabstufung eines zusätzlichen Domänencontrollers sind Domänenadministrator-Anmeldeinformationen erforderlich. Durch die Auswahl der Option **Entfernen des Domänen Controllers erzwingen** wird der Domänen Controller herabgestuft, ohne die Metadaten des Domänen Controller Objekts aus Active Directory zu entfernen.

    > [!IMPORTANT]
    > Wählen Sie diese Option nur dann aus, wenn der Domänencontroller keine andere Domänencontroller kontaktieren kann und zum Beheben dieses Netzwerkproblems *keine angemessene Möglichkeit* besteht. Bei der erzwungenen Herabstufung bleiben in Active Directory der restlichen Domänencontroller in der Gesamtstruktur verwaiste Metadaten zurück. Zudem gehen alle nicht replizierten Änderungen an diesem Domänencontroller, beispielsweise Kennwörter oder neue Benutzerkonten, für immer verloren. Verwaiste Metadaten stellen die Hauptursache in einem erheblichen Prozentsatz der Microsoft Kundendienstfälle für AD DS, Exchange, SQL und andere Software dar. Wenn Sie einen Domänencontroller zwangsweise herabstufen, *müssen* Sie sofort eine manuelle Metadatenbereinigung ausführen. Informationen zu den entsprechenden Schritten finden Sie unter [Bereinigen von Servermetadaten](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816907(v=ws.10)).

-   Für das Herabstufen des letzten Domänencontrollers in einer Domäne ist eine Mitgliedschaft in der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; erforderlich, da hierbei die Domäne selbst entfernt wird (wenn es sich um die letzte Domäne in der Gesamtstruktur handelt, wird dabei die Gesamtstruktur entfernt). Wenn der aktuelle Domänencontroller der letzte Domänencontroller in der Domäne ist, werden Sie von Server-Manager darüber informiert. Wählen Sie die Option **Letzter Domänencontroller in der Domäne** aus, um zu bestätigen, dass der Domänencontroller der letzte Domänencontroller in der Domäne ist.

Weitere Informationen zum Entfernen von AD DS finden Sie unter [Remove Active Directory Domain Services (Stufe 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) und herab [Stufen von Domänen Controllern und Domänen &#40;Ebene 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).

## <a name="ad-ds-removal-options-and-warnings"></a><a name="BKMK_RemovalOptionsPage"></a>Optionen und Warnungen zum Entfernen von AD DS
Hilfe zur Seite %%amp;quot;Optionen prüfen%%amp;quot; finden Sie unter %%amp;quot;Überprüfungsoptionen%%amp;quot;.

Wenn der Domänencontroller zusätzliche Rollen hostet (z. B. die DNS-Serverrolle oder den globalen Katalogserver) wird die folgende Warnseite angezeigt:

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)

Bevor Sie zum Fortsetzen des Vorgangs auf **Weiter** klicken können, müssen Sie auf **Entfernung fortsetzen** klicken, um zu bestätigen, dass die zusätzlichen Rollen nicht mehr verfügbar sein werden.

Wenn Sie das Entfernen eines Domänencontrollers erzwingen, gehen sämtliche Active Directory-Objektänderungen, die nicht auf andere Domänencontroller in der Domäne repliziert wurden, verloren. Falls der Domänencontroller zudem Betriebsmasterrollen, den globalen Katalog oder die DNS-Serverrolle hostet, kann sich dies wie folgt auf wichtige Vorgänge in der Domäne und Gesamtstruktur auswirken. Versuchen Sie vor dem Entfernen eines Domänencontrollers, der eine beliebige Betriebsmasterrolle hostet, die Rolle auf einen anderen Domänencontroller zu übertragen. Wenn die Rolle nicht übertragen werden kann, entfernen Sie zunächst die Active Directory-Domänendienste von diesem Computer, und übernehmen Sie dann die Rolle mithilfe von %%amp;quot;Ntdsutil.exe%%amp;quot;. Verwenden Sie Ntdsutil für den Domänencontroller, für den die Rolle übernommen werden soll. Verwenden Sie möglichst einen aktuellen Replikationspartner, der sich am gleichen Standort wie dieser Domänencontroller befindet. Weitere Informationen zum Übertragen und Übernehmen von Betriebsmasterrollen finden Sie in der Microsoft Knowledge Base in [Artikel 255504](https://go.microsoft.com/fwlink/?LinkId=80395). Wenn der Assistent nicht bestimmen kann, ob der Domänencontroller eine Betriebsmasterrolle hostet, führen Sie den Befehl %%amp;quot;netdom.exe%%amp;quot; aus. Somit können Sie feststellen, ob dieser Domänencontroller Betriebsmasterrollen ausführt.

-   Globaler Katalog: möglicherweise haben die Benutzer Probleme mit der Anmeldung bei Domänen in der Gesamtstruktur. Stellen Sie vor dem Entfernen eines globalen Katalogservers sicher, dass sich in der jeweiligen Gesamtstruktur und an dem jeweiligen Standort genügend globale Katalogserver zum Verarbeiten der Benutzeranmeldungen befinden. Weisen Sie bei Bedarf einen weiteren globalen Katalogserver zu, und aktualisieren Sie die Clients und Anwendungen mit den neuen Informationen.

-   DNS-Server: alle DNS-Daten, die in Active Directory-integrierten Zonen gespeichert werden, gehen verloren. Nachdem Sie AD DS entfernt haben, kann der jeweilige DNS-Server keine Namensauflösung für die in Active Directory integrierten DNS-Zonen ausführen. Daher wird empfohlen, für die Namensauflösung mit der IP-Adresse eines neuen DNS-Servers die DNS-Konfiguration aller Computer zu aktualisieren, die momentan auf die IP-Adresse dieses DNS-Servers verweisen.

-   Infrastrukturmaster: Clients in der Domäne haben möglicherweise Schwierigkeiten dabei, Objekte in anderen Domänen zu finden. Bevor Sie den Vorgang fortsetzen, übertragen Sie die Infrastrukturmasterrolle auf einen Domänencontroller, bei dem es sich nicht um einen globalen Katalogserver handelt.

-   RID-Master: möglicherweise haben Sie Probleme beim Erstellen neuer Benutzerkonten, Computerkonten und Sicherheitsgruppen. Bevor Sie den Vorgang fortsetzen, übertragen Sie die RID-Masterrolle auf einen Domänencontroller, der sich in derselben Domäne wie dieser Domänencontroller befindet.

-   Emulator für primären Domänencontroller (PDC): vom PDC-Emulator ausgeführte Vorgänge wie Gruppenrichtlinienaktualisierungen und Kennwortzurücksetzungen für Nicht-AD DS-Konten funktionieren nicht ordnungsgemäß. Bevor Sie den Vorgang fortsetzen, übertragen Sie die PDC-Emulatormasterrolle auf einen Domänencontroller, der sich in derselben Domäne wie dieser Domänencontroller befindet.

-   Schemamaster: Sie können das Schema für die jeweilige Gesamtstruktur nicht mehr ändern. Bevor Sie den Vorgang fortsetzen, übertragen Sie die Schemamasterrolle auf einen Domänencontroller in der Stammdomäne der Gesamtstruktur.

-   Domänennamenmaster: Sie können der jeweiligen Gesamtstruktur keine Domänen mehr hinzufügen und keine Domänen mehr daraus entfernen. Bevor Sie den Vorgang fortsetzen, übertragen Sie die Domänennamen-Masterrolle auf einen Domänencontroller in der Stammdomäne der Gesamtstruktur.

-   Dabei werden alle Anwendungsverzeichnispartitionen auf diesem Active Directory-Domänencontroller entfernt. Wenn ein Domänencontroller die aktuellste Replikation einer oder mehrerer Anwendungsverzeichnispartitionen enthält, sind diese Partitionen nach Abschluss des Entfernungsvorgangs nicht mehr vorhanden.

Beachten Sie, dass die Domäne nach dem Deinstallieren der Active Directory-Domänendienste vom letzten Domänencontroller in der Domäne nicht mehr vorhanden ist.

Wenn es sich bei dem Domänencontroller um einen DNS-Server handelt, der zum Hosten der DNS-Zone delegiert ist, haben Sie auf der folgenden Seite die Möglichkeit, den DNS-Server aus der DNS-Zonendelegierung zu entfernen.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)

Weitere Informationen zum Entfernen von AD DS finden Sie unter [Remove Active Directory Domain Services (Stufe 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) und herab [Stufen von Domänen Controllern und Domänen &#40;Ebene 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).

## <a name="new-administrator-password"></a><a name="BKMK_NewAdminPwdPage"></a>Neues Administratorkennwort
Auf der Seite **Neues Administrator Kennwort** müssen Sie ein Kennwort für das Administrator Konto des integrierten lokalen Computers angeben, nachdem die Herabstufung abgeschlossen und der Computer zu einem Domänen Mitglieds Server oder Arbeitsgruppen Computer wird.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)

Weitere Informationen zum Entfernen von AD DS finden Sie unter [Remove Active Directory Domain Services (Stufe 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) und herab [Stufen von Domänen Controllern und Domänen &#40;Ebene 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).

## <a name="review-options"></a><a name="BKMK_ConfirmRoleRemovalPage"></a>Überprüfungs Optionen
Auf der Seite **Optionen prüfen** können Sie die Konfigurationseinstellungen für die Herabstufung in ein Windows PowerShell-Skript exportieren, sodass Sie zusätzliche Herabstufungen automatisieren können. Klicken Sie auf **Tiefer stufen**, um AD DS zu entfernen.

![AD DS Installation](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)

