---
ms.assetid: e6fa9069-ec9c-4615-b266-957194b49e11
title: Aktualisieren von AD RMS auf Windows Server 2016
author: msmbaldwin
ms.author: esaggese
ms.date: 05/30/2019
ms.topic: article
ms.openlocfilehash: 8a2d0ec94619f74260f1fbc934e8e3328201ffa9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947210"
---
# <a name="upgrading-ad-rms-to-windows-server-2016"></a>Aktualisieren von AD RMS auf Windows Server 2016

## <a name="introduction"></a>Einführung

Active Directory Rights Management Services (AD RMS) ist ein Microsoft-Dienst, der sensible Dokumente und e-Mails schützt. Im Gegensatz zu herkömmlichen Schutzmethoden wie Firewalls und ACLs sind AD RMS Verschlüsselung und Schutz immer persistent, unabhängig davon, wo sich eine Datei befindet oder wie Sie transportiert wird.

Dieses Dokument enthält Anleitungen zum Migrieren von Windows Server 2012 R2 mit SQL Server 2012 zu Windows Server 2016 und SQL Server 2016. Der gleiche Prozess kann für die Migration von älteren, aber unterstützten Versionen von AD RMS verwendet werden.
Beachten Sie, dass sich Active Directory Rights Management Services nicht mehr in der aktiven Entwicklung befindet, und für die neuesten Funktionen sollten Kunden in Erwägung gezogen werden, zu [Azure Information Protection](https://azure.microsoft.com/services/information-protection/)zu migrieren, der einen weitaus umfassenderen Satz an Features bietet, bei denen die Geräte-und Anwendungsunterstützung vollständiger ist

Informationen zum Migrieren zu Azure Information Protection von AD RMS, ohne den Inhalt erneut schützen zu müssen, finden Sie in [der Dokumentation zur Azure Information Protection Migration](/azure/information-protection/migrate-from-ad-rms-to-azure-rms).

## <a name="about-the-environment-used-in-this-guide"></a>Informationen zur in diesem Handbuch verwendeten Umgebung

AD FS ist eine optionale Komponente einer AD RMS-Installation. In dieser Anleitung wird davon ausgegangen, dass ADFS verwendet wird. Wenn AD FS in Ihrer Umgebung nicht für die Unterstützung von AD RMS Benutzern verwendet wurde, können Sie alle Schritte überspringen, die auf ADFS verweisen.

In diesem Handbuch wird SQL Server auf SQL Server 2016 aktualisiert, indem eine parallele Installation durchgeführt und die Datenbanken über eine Sicherung verschoben werden.
Wenn Sie ein Upgrade Ihrer AD RMS-und ADFS-Datenbankserver auf SQL Server 2016 direkt durchführen können, können Sie mit dem nächsten Abschnitt in diesem Dokument fortfahren, ohne die Schritte in diesem Abschnitt ausführen zu müssen.

## <a name="installation"></a>Installation

### <a name="configuring-sql-server-2016"></a>Konfigurieren von SQL Server 2016

Im folgenden Abschnitt werden die Implementierungsaufgaben erläutert, die direkt mit der Konfiguration von SQL Server 2016 verknüpft sind. Dieser Leitfaden konzentriert sich auf die Verwendung der Server-Manager und des SQL Server Management Studio, um diese Aufgaben auszuführen.

Diese Schritte müssen bei einer SQL Server 2016-Installation ausgeführt werden. Installieren Sie SQL Server 2016 auf geeigneter Hardware gemäß den Standardverfahren und-Richtlinien Ihres Unternehmens.

#### <a name="preparing-the-sql-server"></a>Vorbereiten der SQL Server

Im folgenden Abschnitt wird erläutert, wie Sie die SQL Server so vorbereiten, dass Sie auf SQL Server 2016 aktualisiert werden kann, bevor Sie andere Dienste in der AD RMS Plattform für die Verwendung von Windows Server 2016 aktualisieren können.

##### <a name="adding-cname-for-sql-server-2016-to-dns"></a>Hinzufügen von CNAME für SQL Server 2016 zu DNS

Der CNAME wird verwendet, um sicherzustellen, dass das Windows Server 2016-Setup die entsprechenden Daten erhält, da auf den neuen SQL Server 2016 verwiesen wird. **Hinweis: Wenn Sie bereits einen CNAME-Dienst für den ADFS-und AD RMS-Dienst verwenden, können Sie mit den nächsten Schritten fortfahren.**


**So fügen Sie einen CNAME-Namen für SQL Server 2016 zu DNS hinzu**

1.  Melden Sie sich mit den Anmelde Informationen des Domänen Administrators beim Windows Server 2012 R2-Domänen Controller an.

2.  Öffnen Sie den Server-Manager.

3.  Klicken **Sie auf Extras und dann** auf **DNS** , um den DNS-Manager zu öffnen

4.  Erweitern Sie im linken Navigationsbereich den Domänen Controller, und öffnen Sie **Forward-Lookupzonen**.

5.  Öffnen Sie die entsprechenden Domänen Ressourcen, klicken Sie mit der rechten Maustaste in den rechten Ansichts Bereich, und wählen Sie **Neuer Alias (CNAME)** aus

6.  Geben Sie für den Aliasnamen einen logischen Namen ein, um ihn von anderen zu unterscheiden (z. Sqladrms oder sqladfs)

7.  Nachdem Sie den Namen eingegeben haben, geben Sie den voll qualifizierten Namen des Zielhosts an, der als neuer SQL Server 2016-Server verwendet wird. (Beispiel: SQL2016.contoso.com)

8.  Nachdem Sie alle Informationen eingegeben haben, klicken Sie auf **OK**.

##### <a name="backup-the-ad-rms-and-adfs-databases"></a>Sichern der AD RMS-und AD FS-Datenbanken

Die AD RMS-und ADFS-Datenbanken enthalten wichtige Informationen, die für die AD RMS erforderlich sind, wie z. b. den öffentlichen Schlüssel des Lizenzgebers des Servers, Rechte Richtlinien Vorlagen, ADFS-Konfigurationsdaten und Protokollierungs Informationen. Ohne diese Datenbanken können Clients keine Lizenzen ausstellen, um geschützte Inhalte zu nutzen.

Von den-Datenbanken wird die AD RMS Konfigurations Datenbank als wichtigste betrachtet, da Sie SLC, Rechte Richtlinien Vorlagen, Benutzerschlüssel und Konfigurationsinformationen speichert. Obwohl Sie die Sicherungskopie aller AD RMS-und AD FS-Datenbanken sorgfältig durchführen sollten, sollten Sie die Konfigurations Datenbank regelmäßig sichern.

Die Protokollierungs Datenbank speichert Informationen zu Benutzer Anforderungen an den AD RMS Cluster für Zertifikate und verwendet Lizenzen. Ihre Sicherungsstrategie für diese Datenbank sollte auf der Unternehmensrichtlinie basieren, um diese Art von Informationen beizubehalten.

Die Verzeichnisdienst Datenbank ist für AD RMS Funktionalität nicht entscheidend. wenn die neuesten Daten verloren gehen, wird die Datenbank erneut mit Informationen aufgefüllt, da der AD RMS Serveranforderungen für Zertifikate empfängt und Lizenzen verwendet. Sie müssen diese Datenbank nicht regelmäßig sichern, aber Sie benötigen mindestens eine Kopie der Datenbank, da Sie nach dem Bereitstellen von AD RMS ursprünglich konfiguriert wurde.

**So sichern Sie eine AD RMS-und/oder ADFS-Datenbank mit Microsoft SQL Server**

1.  Melden Sie sich mit SQL 2012 beim Windows Server 2012 R2 AD RMS-Daten Bank Server an.

2.  Klicken Sie im **Startmenü**auf **Alle Programme**, klicken Sie auf **Microsoft SQL Server**, und klicken Sie auf **SQL Server Management Studio**.

3.  Vergewissern Sie sich im Fenster **mit Server verbinden** , dass der Server **, auf dem**die AD RMS-Datenbanken gehostet wird, im Feld **Server Name** angezeigt wird, und klicken Sie

4.  Erweitern Sie **Datenbanken**. Klicken Sie mit der rechten Maustaste auf die entsprechende Datenbank (**DRMS** und **ADFS**), zeigen Sie auf **Tasks**, und wählen Sie **Sicherung**aus.

5.  Wiederholen Sie Schritt 4 für die verbleibenden Datenbanken.

6.  Stellen Sie sicher, dass auf die Sicherung der Datenbanken von anderen Computern im Netzwerk oder über ein Speichergerät zugegriffen werden kann, da diese für spätere Schritte während der Migration erforderlich sind.

Nun können Sie die Daten Bank Kopien an einem sicheren Speicherort speichern. Denken Sie daran, die Datenbanken häufig zu sichern.

##### <a name="adding-domain-admin-sql-ad-rms-andor-adfs-service-account-to-sql-server-2016"></a>Hinzufügen von Domänen Administrator-, SQL-, AD RMS-und/oder ADFS-Dienst Konten zu SQL Server 2016

In den folgenden Schritten wird erläutert, wie die verschiedenen Dienst Konten SQL Server 2016 hinzugefügt werden, um die Migration der Daten aus der Windows Server 2012 R2-Umgebung zu unterstützen. Dadurch erhalten Sie die richtigen Berechtigungen, wenn Sie versuchen, auf den Inhalt zuzugreifen und die Daten zu verarbeiten.

**So fügen Sie das Domänen Administrator-, SQL-, AD RMS-und/oder ADFS-Dienst Konto SQL Server**

1.  Melden Sie sich mit SQL Server 2016 als lokales Administrator Konto beim Server an.

2.  Klicken Sie im **Startmenü**auf **Alle Programme**, klicken Sie auf **Microsoft SQL Server**, und klicken Sie auf **SQL Server Management Studio**.

3.  Vergewissern Sie sich im Fenster **mit Server verbinden** , dass sich der Server, der die AD RMS Datenbanken gehostet, im Feld **Server Name** befindet, und klicken Sie dann zur Authentifizierung auf das Dropdown Menü, und wählen Sie **SQL Server Authentifizierung**aus.

4.  Geben Sie im Feld **Anmelde** Name den Namen des lokalen Administrator Kontos ein (Beispiel: LocalAdmin), geben Sie dann das entsprechende Kennwort ein, und klicken Sie auf **verbinden**.

5.  Erweitern Sie **Sicherheit** , und klicken Sie dann mit der rechten Maustaste auf **Anmeldungen** , und wählen Sie im angezeigten Kontextmenü die Option **neue Anmeldung** aus.

6.  Sobald das Fenster angezeigt wird, geben Sie im Feld **Anmelde Name den Namen** des Domänen Administrator Kontos ein (Beispiel: CONSO \\ conadsoadmin)

7.  Wählen Sie im linken Navigationsbereich **Server Rollen**aus.

8.  Markieren Sie dann das Kontrollkästchen für **sysadmin** unter den Server Rollen, und klicken Sie auf **OK**.

9.  Starten Sie **SQL Server Verwaltung**neu.

10. Vergewissern Sie sich im Fenster **mit Server verbinden** , dass sich der Server, der die AD RMS Datenbanken gehostet, im Feld **Server Name** befindet, und klicken Sie zur Authentifizierung auf das Dropdown Menü, und wählen Sie **Windows-Authentifizierung** **aus.**

##### <a name="restoring-the-ad-rms-and-adfs-databases-to-sql-server-2016"></a>Wiederherstellen der AD RMS-und ADFS-Datenbanken in SQL Server 2016

In den folgenden Schritten wird erläutert, wie die Daten aus der vorherigen SQL Server Instanz in der neuen 2016-Instanz wieder hergestellt werden. Dadurch kann das neue SQL die relevanten Konfigurationsdaten aus den vorherigen AD RMS-und AD FS-Datenbanken verwenden.

**So stellen Sie die Daten aus dem vorherigen SQL Server in der neuen SQL Server wieder her**

1.  Melden Sie sich mit dem entsprechenden Konto beim Server mit SQL Server 2016 an.

2.  Klicken Sie im linken Navigationsbereich mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen** , um den Wiederherstellungs Vorgang zu starten

3.  Wählen Sie unter **Quelle** die Option **Gerät** aus, und suchen Sie dann nach dem Speicherort der Datenbankdateien in den vorherigen Schritten.

4.  Nachdem Sie die Dateien ausgewählt haben, klicken Sie auf **OK**.

5.  Stellen Sie sicher, dass alle Datenbankdateien hinzugefügt wurden, und schließen Sie den Prozess ab, indem Sie auf **OK**

### <a name="configuring-windows-server-2016-active-directory-federation-services-ad-fs"></a>Konfigurieren von Windows Server 2016 Active Directory-Verbunddienste (AD FS) (AD FS)

AD FS wurde bereitgestellt, um Single Sign-on (SSO)-Zugriff auf AD RMS als Anwendung bereitzustellen. Es wurde auch mit der AD RMS-Mobile Geräte Erweiterung (MDE) konfiguriert, die die Unterstützung von Mac-und mobilen Geräten für Endbenutzer ermöglicht.

Die folgenden Abschnitte enthalten Anleitungen zu betrieblichen Aufgaben, die Sie möglicherweise für Ihre AD FS-Bereitstellung ausführen müssen.

#### <a name="adding-a-2016-ad-fs-server-to-the-farm"></a>Hinzufügen eines 2016-AD FS Servers zur Farm

Sie können zusätzliche AD FS Server bereitstellen, um die AD RMS Bereitstellung zu unterstützen. Sie können diese Aktion im Falle eines größeren Datenverkehrs an die AD RMS Server oder zusätzliche Anwendungen ausführen, oder wenn Sie einen der derzeit für AD FS verwendeten Server außer Kraft setzen müssen.

**So fügen Sie der Farm 2016 AD FS Server hinzu**

1.  Doppelklicken Sie auf dem Azure AD Connect Server auf das Symbol **Azure AD Connect** , um den Azure AD Connect-Assistenten zu starten.

2.  Klicken Sie auf der Willkommensseite auf **Konfigurieren**.

3.  Klicken Sie auf der Seite Weitere Aufgaben auf **zusätzlichen Verbund Server** bereitstellen, und klicken Sie dann auf **weiter**.

4.  Geben Sie auf der Seite mit Azure AD verbinden den Benutzernamen und das Kennwort eines Kontos mit globalen Administrator Berechtigungen ein, und klicken Sie dann auf **weiter**.

5.  Geben Sie auf der Seite Domänen Administrator-Anmelde Informationen den Benutzernamen und das Kennwort eines Kontos mit Domänen Administrator Berechtigungen ein, und klicken Sie auf **weiter**.

6.  Klicken Sie auf **Durchsuchen** , und wählen Sie die Zertifikat Datei aus, die beim Konfigurieren der AD FS Azure AD Connect Farm verwendet wurde.

7.  Klicken Sie zum Öffnen des Dialog Felds Zertifikat Kennwort auf **Kennwort eingeben** .

8.  Geben Sie im Feld Kennwort das Kennwort des Zertifikats ein, und klicken Sie dann auf **OK**.

9.  Klicken Sie auf **Weiter**.

10. Geben Sie auf der Seite AD FS Server den Namen oder die IP-Adresse des neuen AD FS Servers ein, und klicken Sie auf **Hinzufügen**.

11. Klicken Sie auf der Seite bereit zur Konfiguration auf **Installieren**.

12. Klicken Sie auf der Seite Installation ist fertig auf **Beenden**.

#### <a name="raising-the-adfs-farm-behavior-level"></a>Erhöhen der Verhaltens Stufe der AD FS-Farm

Wenn Sie einen AD FS-Server bereitstellen, der die aktuelle Umgebungs Ebene überschreitet, z. b. über einen ADFS unter Windows Server 2012 R2 und anschließendes Hinzufügen eines AD FS-Windows-Servers 2016, muss die Ebene des Farm Verhaltens erhöht werden. Dies ist erforderlich, um sicherzustellen, dass die Umgebung die aktuellsten Informationen und Funktionen verwendet.

**So erhöhen Sie die Verhaltensebene der AD FS-Farm**

1.  Navigieren Sie zu Windows Server 2016 ADFS.

2.  Öffnen Sie eine Administrator-PowerShell-Sitzung.

3.  Geben Sie den folgenden Befehl ein: " ** \$ Kred = Get-Credential** ".

4.  Ein Fenster wird angezeigt, in dem Sie zur Eingabe von Anmelde Informationen aufgefordert werden.

5.  Geben Sie dann den folgenden Befehl ein: " **aufrufen-adfsfarmverhalorlevelraise-Credential \$ ** ".

6.  Es wird eine Eingabeaufforderung mit der Frage angezeigt. möchten **Sie den Vorgang fortsetzen?** Geben Sie dann **ein ein** , um die Aufforderung zu akzeptieren.

7.  Nachdem der Befehl abgeschlossen wurde, wird die Farm Verhaltensebene eingerichtet und ist bereit.

#### <a name="enabling-mobile-device-extension-logging"></a>Aktivieren der Protokollierung der mobilen Geräte Erweiterung

Mit der Erweiterung für mobile Geräte können von Endbenutzer Geräten empfangene Anforderungen protokolliert werden. Die Protokollierung ist standardmäßig deaktiviert. es wird empfohlen, die Protokollierung nur in einem Problem Behandlungs Szenario zu aktivieren Alle Anforderungen von mobilen Geräten und Desktop Computern zum Bootstrapping oder zum Erwerb einer Endbenutzer Lizenz werden in der AD RMS Protokollierungs Datenbank oder im Azure Storage-Konto protokolliert. Die MDE-Protokollierung erstellt zwei zusätzliche Tabellen für die SQL Server, die von AD RMS verwendet werden: die Client-Debug-Protokoll Tabelle und die Client Leistungs Protokoll-Tabelle.

**So aktivieren Sie die Protokollierung mobiler Geräte**

1.  Öffnen Sie auf einem AD RMS Server Windows PowerShell als Administrator.

2.  Geben Sie den folgenden Befehl ein, und drücken **Sie die Eingabe**Taste: **Import-Module ADRMSADMIN** .

3.  Geben Sie den folgenden Befehl ein, und drücken **Sie die Eingabe**Taste: **New-PSDrive-Name adrmscluster-psprovider ADRMSADMIN-root https://localhost **

4.  Geben Sie den folgenden Befehl ein, und drücken **Sie die Eingabe**Taste: **Set-ItemProperty-Path adrmscluester: \\ -Name isloggingenabled-Value \$ true**

Wenn Sie die MDE-Protokollierung für die Problembehandlung verwenden, empfiehlt es sich, diese nach der Behebung des Problems zu deaktivieren.

**So deaktivieren Sie die Protokollierung der mobilen Geräte Erweiterung**

1.  Öffnen Sie auf einem AD RMS Server Windows PowerShell als Administrator.

2.  Geben Sie den folgenden Befehl ein, und drücken **Sie die Eingabe**Taste: **Import-Module ADRMSADMIN** .

3.  Geben Sie den folgenden Befehl ein, und drücken **Sie die Eingabe**Taste: **New-PSDrive-Name adrmscluster-psprovider ADRMSADMIN-root https://localhost **

4.  Geben Sie den folgenden Befehl ein, und drücken **Sie die Eingabe**Taste: **Set-ItemProperty-Path adrmscluester: \\ -Name isloggingenabled-Value \$ false**

### <a name="upgrading-ad-rms-to-windows-server-2016"></a>Aktualisieren von AD RMS auf Windows Server 2016

Die folgenden Abschnitte enthalten Anleitungen zum Hinzufügen eines Windows Server 2016-basierten AD RMS Servers zum aktuellen Windows Server 2012 R2-Cluster. Der Server wird dem Cluster hinzugefügt, und die Informationen werden darauf repliziert, sodass der vorherige AD RMS Server als veraltet markiert werden kann, um Ressourcen freizugeben.

Nachdem Sie einen Windows Server 2016-basierten AD RMS Server hinzugefügt haben, der dem AD RMS Cluster hinzugefügt wurde, werden alle Knoten, die auf älteren Versionen von Windows basieren, inaktiv. Anschließend können Sie die Bereitstellung dieser Server aufheben (z. b. Herunterfahren, neu zuweisen oder mit Windows Server 2016 neu installieren, um dem AD RMS Cluster beizutreten).

Sie können zusätzliche AD RMS Server für den Cluster bereitstellen, um die Auslastung Ihrer AD RMS-Bereitstellung zu unterstützen. Sie können diese Aktion auch ausführen, wenn Sie den Datenverkehr an die AD RMS Server erhöhen.

Dieses Handbuch behandelt nicht die Schritte, die zum Ändern der in Ihrer Umgebung verwendeten Lasten Ausgleichsmechanismen erforderlich sind, um die von Ihnen veralteten Server auszuschließen und diejenigen einzuschließen, die Sie dem Cluster hinzufügen.

#### <a name="adding-a-2016-ad-rms-server"></a>Hinzufügen eines 2016-AD RMS Servers

Wenn Ihr AD RMS Cluster ein Hardware Sicherheitsmodul anstelle eines zentral verwalteten Schlüssels für das Lizenzgeber Zertifikat eines Servers verwendet, müssen Sie die Software und andere HSM-Artefakte (z. b. Schlüssel-und Konfigurationsdateien) auf dem Server installieren, bevor Sie AD RMS installieren. Außerdem müssen Sie das HSM entweder physisch oder über die relevanten Netzwerkkonfigurationen mit dem Server verbinden. Befolgen Sie die Anleitung zum HSM für diese Schritte.

**So fügen Sie einen 2016-AD RMS Server hinzu**

1.  Installieren Sie die AD RMS Rolle auf der gewünschten Windows Server 2016-Bereitstellung.

2.  Nachdem die Installation abgeschlossen ist, klicken Sie auf den Link, um **zusätzliche Konfigurationen auszuführen**.

3.  Wählen Sie **vorhandenen AD RMS Cluster beitreten** aus, und klicken Sie auf **weiter**.

4.  Geben Sie auf der Seite **Konfigurations Datenbank auswählen** den in DNS für den 2016 SQL Server (vollständig) angegebenen CNAME-Namen ein.

5.  Klicken Sie in der zweiten Zeile auf Liste, und wählen Sie in der Dropdown **Liste** den **Eintrag defaultinstance** aus.

6.  Wählen Sie unter **Name der Konfigurations Datenbank**das Dropdown Menü aus, und wählen Sie die angezeigte DRMS-Konfiguration aus. Klicken Sie dann auf **Weiter**.

7.  Geben Sie auf der Seite **Datenbankinformationen** das Cluster Schlüssel Kennwort in das angegebene Feld ein. Klicken Sie danach auf **weiter**.

8.  Geben Sie auf der nächsten Seite des Assistenten das AD RMS Dienst Konto an, geben Sie das Kennwort für das Konto an, und klicken Sie dann auf **weiter** , sobald es überprüft wurde.

9.  Nachdem die Seite **Cluster Website** angezeigt wird, stellen Sie einfach sicher, dass die entsprechende Website ausgewählt ist, und klicken Sie auf **weiter**.

10. Wählen Sie auf der Seite **Server Authentifizierungszertifikat auswählen** das importierte SSL-Zertifikat aus, und klicken Sie auf **weiter**.

11. Klicken Sie auf **Installieren**, um die Installation zu starten.

12. Nachdem die Konfiguration abgeschlossen ist, müssen Sie sich ab-und wieder anmelden, um AD RMS zu verwalten.

13. Nachdem Sie sich wieder angemeldet haben, öffnen Sie **Server-Manager** **Tools** auswählen und **Active Directory Rights Management**. Das Fenster "Verwaltung" sollte angezeigt werden und angeben, dass der Cluster über den zusätzlichen Server im Cluster verfügt.

14. Wenn die AD RMS Mobile-Geräte Erweiterung im ursprünglichen AD RMS-Cluster installiert wurde, müssen Sie auch die MDE in den aktualisierten Cluster Knoten installieren. Befolgen Sie die Anweisungen in der MDE-Dokumentation, um MDE zu Ihrem AD RMS Cluster hinzuzufügen.
An diesem Punkt können Sie alle bereits vorhandenen Knoten wieder verwenden oder Sie auf Windows Server 2016 aktualisieren und mit dem oben beschriebenen Prozess erneut mit dem AD RMS Cluster verknüpfen.

### <a name="configuring-windows-server-2016-web-application-proxy-wap"></a>Konfigurieren von Windows Server 2016-webanwendungsproxy (WAP)

Die folgenden Abschnitte enthalten Anleitungen zu betrieblichen Aufgaben, die Sie möglicherweise für die Bereitstellung des webanwendungsproxys ausführen müssen. Dies ist ein optionaler Schritt, der nicht erforderlich ist, wenn Sie AD RMS über andere Mechanismen im Internet veröffentlichen.

#### <a name="adding-a-windows-server-2016-wap-server"></a>Hinzufügen eines Windows Server 2016-WAP-Servers

Sie können zusätzliche webanwendungsproxy-Server zur Unterstützung der AD RMS Bereitstellung bereitstellen Sie können diese Aktion im Falle eines größeren Datenverkehrs an die AD RMS Server ausführen, oder wenn Sie einen der derzeit für den webanwendungsproxy verwendeten Server außer Kraft setzen müssen.

**So fügen Sie einen 2016-webanwendungsproxy**

1.  Navigieren Sie auf dem Server, den Sie als webanwendungsproxy einrichten möchten, zur Server-Manager Konsole, und klicken Sie auf **Rollen und Features hinzufügen**.

2.  Klicken Sie im **Assistenten zum Hinzufügen von Rollen und Features**auf **weiter** , bis Sie zum Bildschirm Server Rollenauswahl gelangen.

3.  Wählen Sie auf dem Bildschirm Server Rollen auswählen die Option **Remote Zugriff**aus, und klicken Sie dann auf **weiter** , bis Sie sich wieder auf dem Bildschirm Server Rollen auswählen befinden.

4.  Wählen Sie im Bildschirm Server Rollen auswählen die Option **webanwendungsproxy**aus, klicken Sie auf **Features hinzufügen**und dann auf **weiter**.

5.  Klicken Sie auf dem Bildschirm Installationsauswahl bestätigen auf **Installieren**.

6.  Klicken Sie nach Abschluss der Installation auf **Schließen**.

7.  Nun ist es an der Zeit, den Server zu konfigurieren. Öffnen Sie hierzu die Remote Zugriffs-Verwaltungskonsole auf dem webanwendungsproxy-Server. Öffnen Sie das **Startmenü** , geben Sie **RAMgmtUI.exe**ein, und wählen Sie dann die Anwendung aus.

8.  Klicken Sie im Navigationsbereich auf **Webanwendungsproxy**.

9.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole auf **Assistent zum Konfigurieren des webanwendungsproxy ausführen**. Klicken Sie im Assistenten auf **weiter**.

10. Geben Sie auf dem Bildschirm Verbund Server den voll qualifizierten Domänen Namen des AD FS Servers ein (z. ADFS.contoso.com), und geben Sie dann Anmelde Informationen für einen Administrator auf dem AD FS Server ein.

11. Wählen Sie auf dem Bildschirm AD FS Proxy Zertifikat in der Liste der derzeit auf dem webanwendungsproxy-Server installierten Zertifikate ein Zertifikat aus, das vom webanwendungsproxy für AD FS Proxy verwendet werden soll, und klicken Sie dann auf **weiter**.

12. Überprüfen Sie auf dem Bestätigungsbildschirm die Einstellungen, und klicken Sie dann auf **Konfigurieren**.

13. Nachdem die Konfiguration abgeschlossen ist, klicken Sie auf **Schließen**.

#### <a name="dns-configuration-for-2016-wap-server"></a>DNS-Konfiguration für 2016-WAP-Server

Nachdem der Windows Server 2016-webanwendungsproxy-Server eingerichtet wurde, müssen einige DNS-Änderungen vorgenommen werden. Hierfür muss ein Dienst wie GoDaddy verwendet werden, um die AD FS-und AD RMS Dienste auf dem 2016-WAP-Server zu verweisen.

**So zeigen Sie den DNS auf dem WAP-Server an**

1.  Navigieren Sie zur Website Ihres Anbieters (z. GoDaddy).

2.  Wechseln Sie zur Domänen Verwaltung und dann zu DNS-Verwaltung.

3.  Suchen Sie nach den ADFS-und AD RMS Dienst, und ersetzen Sie die Punkte durch die öffentliche IP-Adresse des 2016 WAP-Servers, und **Speichern** **Sie Sie** .

4.  Die Weitergabe der Änderungen kann einige Zeit in Anspruch nehmen, aber sobald diese abgeschlossen ist, wird das Setup abgeschlossen.

#### <a name="enabling-debugging-logs"></a>Aktivieren von Debugprotokollen

Detaillierte Protokollierungs Informationen sind auf den webanwendungsproxy-Servern verfügbar. Sie können die Erweiterte Debugprotokollierung mithilfe des Ereignisanzeige konfigurieren. Weitere Einstellungen können auch für die Größe der Protokolle ausgewählt werden, um sicherzustellen, dass die Analyse für den Viewer hilfreich ist.

**Aktivieren von Debugprotokollen für webanwendungsproxy**

1.  Öffnen Sie die **Ereignisanzeige** -Konsole auf dem webanwendungsproxy.

2.  Erweitern Sie den Knoten **Microsoft** .

3.  Erweitern Sie den Knoten **Windows** .

4.  Öffnen Sie die **webanwendungsproxy** -Protokolle.

5.  Sie werden dann in der Lage sein, die **Administrator** Protokolle zu öffnen.

6.  Öffnen Sie das Menü **Aktion** in der oberen linken Ecke, und wählen Sie **Eigenschaften**aus.

7.  Wählen Sie auf der Registerkarte **Allgemein** die Option zum **Aktivieren der Protokollierung**aus.

8.  Schließlich können Sie die maximale Protokoll Größe anpassen und was passiert, wenn die maximale Ereignisprotokoll Größe erreicht wird.

### <a name="configuring-high-availability-for-windows-server-2016-services"></a>Konfigurieren von Hochverfügbarkeit für Windows Server 2016-Dienste

Die folgenden Abschnitte enthalten Anleitungen zu betrieblichen Aufgaben, die möglicherweise erforderlich sind, um Ihre Windows Server 2016-Umgebung in Hochverfügbarkeit einzurichten.

#### <a name="adding-a-2016-ad-rms-server-for-high-availability"></a>Hinzufügen eines 2016-AD RMS Servers für hohe Verfügbarkeit

Sie können zusätzliche AD RMS Server bereitstellen, um Hochverfügbarkeit einzurichten. Sie können diese Aktion im Fall von erhöhtem Datenverkehr zu den AD RMS Servern ausführen.

**So fügen Sie einen 2016-AD RMS Server für hohe Verfügbarkeit hinzu**

1.  Installieren Sie die AD RMS Rolle auf der gewünschten Windows Server 2016-Bereitstellung.

2.  Nachdem die Installation abgeschlossen ist, klicken Sie auf den Link, um **zusätzliche Konfigurationen auszuführen**.

3.  Wählen Sie **vorhandenen AD RMS Cluster beitreten** aus, und klicken Sie auf **weiter**.

4.  Geben Sie auf der Seite **Konfigurations Datenbank auswählen** den in DNS für den 2016 SQL Server (vollständig) angegebenen CNAME-Namen ein.

5.  Klicken Sie in der zweiten Zeile auf Liste, und wählen Sie in der Dropdown **Liste** den **Eintrag defaultinstance** aus.

6.  Wählen Sie unter **Name der Konfigurations Datenbank**das Dropdown Menü aus, und wählen Sie die angezeigte DRMS-Konfiguration aus. Klicken Sie dann auf **Weiter**.

7.  Geben Sie auf der Seite **Datenbankinformationen** das Cluster Schlüssel Kennwort in das angegebene Feld ein. Klicken Sie danach auf **weiter**.

8.  Geben Sie auf der nächsten Seite des Assistenten das AD RMS Dienst Konto an, geben Sie das Kennwort für das Konto an, und klicken Sie dann auf **weiter** , sobald es überprüft wurde.

9.  Nachdem die Seite **Cluster Website** angezeigt wird, stellen Sie einfach sicher, dass die entsprechende Website ausgewählt ist, und klicken Sie auf **weiter**.

10. Wählen Sie auf der Seite **Server Authentifizierungszertifikat auswählen** das importierte SSL-Zertifikat aus, und klicken Sie auf **weiter**.

11. Klicken Sie auf **Installieren**, um die Installation zu starten.

12. Nachdem die Konfiguration abgeschlossen ist, müssen Sie sich ab-und wieder anmelden, um AD RMS zu verwalten.

13. Nachdem Sie sich wieder angemeldet haben, öffnen Sie **Server-Manager** **Tools** auswählen und **Active Directory Rights Management**. Das Fenster "Verwaltung" sollte angezeigt werden und angeben, dass der Cluster über den zusätzlichen Server im Cluster verfügt.

14. Nachdem Sie die Server Einrichtung bestätigt haben, konfigurieren Sie den Lasten Ausgleichs Dienst, um die Last zwischen den verschiedenen AD RMS Servern im Cluster auszugleichen.

#### <a name="adding-a-windows-server-2016-ad-fs-server-for-high-availability"></a>Hinzufügen eines Windows Server 2016 AD FS-Servers für hohe Verfügbarkeit

Sie können zusätzliche AD FS Server bereitstellen, um Hochverfügbarkeit einzurichten. Sie können diese Aktion im Fall von erhöhtem Datenverkehr zu den AD FS Servern ausführen. **Hinweis: nach dem erhöhen der Farm Verhaltensebene wird ein neuer Datenbankeintrag in den SQL Server 2016 (ADFS Configv3) eingegeben, und die alte Konfigurations Datenbank muss gelöscht werden, bevor Sie mit diesen Schritten fortfahren können.**

**So fügen Sie Windows Server 2016 AD FS Server für hohe Verfügbarkeit hinzu**

1.  Installieren Sie die AD RMS Rolle auf der gewünschten Windows Server 2016-Bereitstellung.

2.  Nachdem die Installation abgeschlossen ist, wählen Sie den Link zum **Konfigurieren des Verbund Dienstanbieter auf diesem Server aus**.

3.  Wählen Sie im Abschnitt Willkommen des Assistenten die Option zum **Hinzufügen eines Verbund Servers zu einer Verbund Serverfarm** aus, und klicken Sie dann auf **weiter**.

4.  Geben Sie das richtige Administrator Konto an, und klicken Sie auf **weiter**.

5.  Wählen Sie auf der Seite **Farm angeben** den **Speicherort der Datenbank für eine vorhandene Farm mit aus SQL Server** geben Sie dann den CNAME für den SQL-Dienst für den Datenbank-Hostnamen an, und klicken Sie auf **weiter**.

6.  Geben Sie im Bereich **Dienst Konto angeben** des Assistenten die Anmelde Informationen für das AD FS Dienst Konto ein, und klicken Sie dann auf **weiter**.

7.  Klicken Sie unter **Überprüfungs Optionen**auf **weiter**.

8.  Klicken Sie auf **Konfigurieren** , wenn die Schaltfläche verfügbar wird.

9.  Starten Sie den Computer nach der Konfiguration neu.

10. Nachdem Sie die Server Einrichtung bestätigt haben, können Sie die AD FS Server nach Bedarf ausgleichen.

#### <a name="adding-a-windows-server-2016-wap-server-for-high-availability"></a>Hinzufügen eines Windows Server 2016-WAP-Servers für hohe Verfügbarkeit

Sie können zusätzliche WAP-Server zum Einrichten der Hochverfügbarkeit bereitstellen. Sie können diese Aktion im Fall von erhöhtem Datenverkehr zu den AD RMS Servern ausführen.

**So fügen Sie einen Windows Server 2016-webanwendungsproxy-Server hinzu**

1.  Navigieren Sie auf dem Server, den Sie als webanwendungsproxy einrichten möchten, zur Server-Manager Konsole, und klicken Sie auf **Rollen und Features hinzufügen**.

2.  Klicken Sie im **Assistenten zum Hinzufügen von Rollen und Features**auf **weiter** , bis Sie zum Bildschirm Server Rollenauswahl gelangen.

3.  Wählen Sie auf dem Bildschirm Server Rollen auswählen die Option **Remote Zugriff**aus, und klicken Sie dann auf **weiter** , bis Sie sich wieder auf dem Bildschirm Server Rollen auswählen befinden.

4.  Wählen Sie im Bildschirm Server Rollen auswählen die Option **webanwendungsproxy**aus, klicken Sie auf **Features hinzufügen**und dann auf **weiter**.

5.  Klicken Sie auf dem Bildschirm Installationsauswahl bestätigen auf **Installieren**.

6.  Klicken Sie nach Abschluss der Installation auf **Schließen**.

7.  Nun ist es an der Zeit, den Server zu konfigurieren. Öffnen Sie hierzu die Remote Zugriffs-Verwaltungskonsole auf dem webanwendungsproxy-Server. Öffnen Sie das **Startmenü** , geben Sie **RAMgmtUI.exe**ein, und wählen Sie dann die Anwendung aus.

8.  Klicken Sie im Navigationsbereich auf **Webanwendungsproxy**.

9.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole auf **Assistent zum Konfigurieren des webanwendungsproxy ausführen**. Klicken Sie im Assistenten auf **weiter**.

10. Geben Sie auf dem Bildschirm Verbund Server den voll qualifizierten Domänen Namen des AD FS Servers ein (z. ADFS.contoso.com), und geben Sie dann Anmelde Informationen für einen Administrator auf dem AD FS Server ein.

11. Wählen Sie auf dem Bildschirm AD FS Proxy Zertifikat in der Liste der derzeit auf dem webanwendungsproxy-Server installierten Zertifikate ein Zertifikat aus, das vom webanwendungsproxy für AD FS Proxy verwendet werden soll, und klicken Sie dann auf **weiter**.

12. Überprüfen Sie auf dem Bestätigungsbildschirm die Einstellungen, und klicken Sie dann auf **Konfigurieren**.

13. Nachdem die Konfiguration abgeschlossen ist, klicken Sie auf **Schließen**.

14. Nachdem Sie die Server Einrichtung bestätigt haben, verteilen Sie den Lastenausgleich für die WAP-Server in der DMZ.

#### <a name="adding-a-sql-server-2016-node-for-always-on-high-availability"></a>Hinzufügen eines Knotens "SQL Server 2016" für Always on Hochverfügbarkeit

Sie können zusätzliche SQL Server-Server bereitstellen, um Always on Hochverfügbarkeit einzurichten. Sie können diese Aktion im Fall von erhöhtem Datenverkehr zu den AD RMS Servern ausführen. **Hinweis: Stellen Sie sicher, dass für beide SQL Server der eingehende Port 5022 geöffnet ist.**

**So fügen Sie einen SQL Server 2016-Server für Always on Hochverfügbarkeit hinzu**

1.  Navigieren Sie auf dem Server, den Sie als zusätzlichen SQL Server 2016-Server einrichten möchten, zur Server-Manager Konsole, und klicken Sie auf **Rollen und Features hinzufügen**.

2.  Klicken Sie auf **weiter** , bis das Dialogfeld **Features auswählen** angezeigt wird.

3.  Aktivieren Sie das Kontrollkästchen **Failoverclustering** . **Hinweis: führen Sie diesen Schritt für den ursprünglichen SQL Server 2016-Server aus, damit beide SQL Server über das Failoverclustering-Feature verfügen.**

4.  Klicken Sie auf **Installieren** , um das Feature Failoverclustering zu installieren.

5.  Öffnen Sie jetzt **Server-Manager** , und **Tools** klicken Sie auf Extras und dann auf **Failovercluster-Manager**.

6.  Klicken Sie im linken Menübereich mit der rechten Maustaste auf **Failovercluster-Manager** , und wählen Sie **Cluster erstellen** aus.

7.  Der Clustererstellungs- **Assistent**wird geöffnet.

8.  Suchen Sie nach den SQL Server 2016-Servern, die für Always on Hochverfügbarkeit verwendet werden, und geben Sie Sie ein, und klicken Sie dann auf **weiter**.

9.  Sie erhalten eine Validierungs Warnung. Wählen Sie **Ja** aus, um die Cluster Knoten zu überprüfen, und klicken Sie auf **weiter**

10. Wählen Sie auf der Seite **Test Optionen** die Option **alle Tests ausführen** aus, und klicken Sie auf **Weiter.**

11. **Hinweis: der clusterüberprüfungs-Assistent gibt mehrere Warnmeldungen zurück, insbesondere dann, wenn Sie keinen freigegebenen Speicher verwenden werden. Wenn Sie Fehlermeldungen finden, müssen Sie diese vor dem Erstellen des Windows Server-Failoverclusters beheben**.

12. Geben Sie im Dialogfeld **Zugriffspunkt für die Cluster Verwaltung** den Cluster Namen und die virtuelle IP-Adresse für den Windows Server-Failovercluster ein, und klicken Sie dann auf **weiter**.

13. Überprüfen Sie, ob die Konfiguration erfolgreich war **, und klicken Sie auf** **Fertig**stellen.

14. Klicken Sie im **Failovercluster-Manager** mit der rechten Maustaste auf den Cluster, wählen Sie **Weitere Aktionen** aus, und wählen Sie dann **Cluster Quorum Einstellungen konfigurieren** aus.

15. Klicken Sie auf **weiter** , und wählen Sie dann die Option **Quorum Zeugen auswählen** aus, und klicken Sie dann erneut auf **weiter** .

16. Wählen Sie auf der Seite **Quorum Zeugen auswählen** die Option **Dateifreigabe Zeugen konfigurieren** aus. Klicken Sie dann auf **Weiter**.

17. Wählen Sie **Durchsuchen** aus, und suchen Sie im Dialogfeld Dateifreigabe Pfad den Pfad der Dateifreigabe, die Sie verwenden möchten. Klicken Sie auf **Weiter**.

18. Klicken Sie auf der Bestätigungsseite auf **Weiter**.

19. Klicken Sie auf der Zusammenfassungsseite auf **Fertig stellen**.

20. Öffnen Sie nun das **Startmenü** , und suchen Sie nach **SQL Server-Konfigurations-Manager**.

21. Klicken Sie mit der rechten Maustaste auf den SQL Server Namen, und wählen Sie **Eigenschaften**

22. Wählen Sie im Dialogfeld Eigenschaften die Registerkarte **hohe Verfügbarkeit (AlwaysOn** ) aus. Aktivieren Sie das Kontrollkästchen **AlwaysOn-Verfügbarkeitsgruppen aktivieren** . Klicken Sie auf **OK**. **Hinweis: führen Sie dies auf beiden SQL Server 2016-Servern aus.**

23. Starten Sie anschließend den SQL Server-Dienst neu.

24. Öffnen Sie nun das **Startmenü** , und suchen Sie nach **SQL Server Management Studio** **und klicken Sie**im linken Navigationsbereich mit der rechten Maustaste auf **Verfügbarkeits Gruppen** , und klicken Sie dann auf Assistent für **neue Verfügbarkeits** Gruppen.

25. Wählen Sie auf der Seite **Namen der Verfügbarkeits Gruppe angeben** einen Gruppennamen aus (z. b. SQLAvailabilityGroup2016). Klicken Sie dann auf **Weiter**.

26. Geben Sie im Abschnitt **Datenbanken auswählen** die Datenbanken an. Klicken Sie anschließend auf Weiter. **Hinweis: Einige Datenbanken müssen möglicherweise erneut gesichert oder in den vollständigen Wiederherstellungs Modus versetzt werden**.

27. Klicken Sie auf der Seite **Replikate angeben** auf die Schaltfläche **Replikat hinzufügen** , und wählen Sie die andere 2016-SQL Server

28. Klicken Sie nach dem Hinzufügen des anderen Servers auf die Kontrollkästchen, und legen Sie für den sekundären Server eine lesbare sekundäre Datenbank fest.

29. Navigieren Sie zur Registerkarte **Endpunkte** , und klicken Sie auf die Option **Aktualisieren** . Scrollen Sie auch hier zu, und stellen Sie sicher, dass sich das gleiche Dienst Konto auf dem primären und dem sekundären Knoten befindet.

30. Wählen Sie nun die Registerkarte **Sicherungs Einstellungen** aus, und wählen Sie die Option **Sekundär bevorzugen** aus.

31. Wechseln Sie zur Registerkarte **Listener** .

32. Geben Sie einen Namen an (z. SqlListener), stellen Sie sicher, dass der Port **1433** ist, und klicken Sie dann auf **weiter**.

33. Wählen Sie auf der Seite **anfängliche Datensynchronisierung auswählen** des Assistenten die Option **vollständig** aus, und geben Sie den für alle SQL Server verfügbaren Netzwerk Speicherort an. Klicken Sie dann auf **weiter**.

34. Klicken Sie abschließend auf **Fertig** stellen, damit der Vorgang abgeschlossen wird.

### <a name="decommission-windows-server-2012-r2-nodes"></a>Außerbetriebnahme von Windows Server 2012 R2-Knoten

Die folgenden Abschnitte enthalten Anleitungen zu Betriebs Aufgaben, die Sie möglicherweise benötigen, um Ihre Windows Server 2012 R2-Server zu entfernen, nachdem Sie das AD RMS-Cluster erfolgreich auf Windows Server 2016 aktualisiert haben.

#### <a name="removing-a-windows-server-2012-r2-ad-rms-server"></a>Entfernen eines Windows Server 2012 R2-AD RMS Servers

Nach einem Upgrade können Sie unnötige AD RMS Server entfernen. Sie können diese Aktion durchführen, wenn Sie für die Außerbetriebnahme von AD RMS Servern benötigt wird.

So **Entfernen Sie einen** **Windows Server 2012 R2-AD RMS Server**

1.  Wählen Sie auf dem Windows Server 2012 R2-AD RMS Server in Server-Manager in den oberen rechten Menüs die Option **Verwalten** aus, und wählen Sie dann **Rollen und Features entfernen**aus.

2.  Der **Assistent zum Entfernen von Rollen und Features** wird geöffnet, und klicken Sie auf dem Bildschirm **Vorbemerkungen** auf **weiter**.

3.  Klicken Sie auf dem Bildschirm **Server Auswahl** auf **weiter**.

4.  Entfernen Sie auf dem Bildschirm **Server Rollen** die Option neben **Active Directory Rights Management Services** , und klicken Sie auf **weiter**.

5.  Klicken Sie auf dem Bildschirm **Features** auf **weiter**.

6.  Klicken Sie auf dem **Bestätigungs** Bildschirm auf **Entfernen**.

7.  Nachdem dieser Vorgang abgeschlossen ist, starten Sie den Server neu.

8.  Sie können diesen Server jetzt Herunterfahren und die Ressourcen bei Bedarf neu zuordnen.
