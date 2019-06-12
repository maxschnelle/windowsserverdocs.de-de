---
ms.assetid: e6fa9069-ec9c-4615-b266-957194b49e11
title: Aktualisieren von AD RMS auf WindowsServer 2016
description: ''
author: msmbaldwin
ms.author: esaggese
ms.date: 05/30/2019
ms.topic: article
ms.openlocfilehash: ce058a2885315c84d2c1c6701ad2801790d3c590
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66814073"
---
# <a name="upgrading-ad-rms-to-windows-server-2016"></a>Aktualisieren von AD RMS auf WindowsServer 2016

## <a name="introduction"></a>Einführung

Active Directory Rights Management Services (AD RMS) ist ein Microsoft-Dienst, der vertraulichen Dokumente und e-Mails geschützt werden. Im Gegensatz zu herkömmlichen Schutzmethoden, wie Firewalls und Zugriffssteuerungslisten sind AD RMS-Verschlüsselung und Schutz persistenten unabhängig von der, in dem eine Datei geht und wie diese übermittelt werden. 

Dieses Dokument enthält Anleitungen zum Migrieren von Windows Server 2012 R2 mit SQL Server 2012 zu Windows Server 2016 und SQL Server 2016. Genauso kann zum Migrieren von älteren aber unterstützten Versionen von AD RMS verwendet werden.
Bitte beachten Sie, dass Active Directory Rights Management Services nicht mehr in der aktiven Entwicklung ist, und für die neuesten Funktionen Kunden erwägen sollten, Migrieren zu [Azure Information Protection](https://azure.microsoft.com/services/information-protection/), dem bietet es sich um eine noch viel mehr umfassende Reihe von Funktionen mit vollständige Geräte- und anwendungsunterstützung. 

Informationen zum Migrieren zu Azure Information Protection von AD RMS ohne erneutes Schützen Ihrer Inhalte finden Sie unter [der Dokumentation zur Migration von Azure Information Protection](https://docs.microsoft.com/azure/information-protection/migrate-from-ad-rms-to-azure-rms).

## <a name="about-the-environment-used-in-this-guide"></a>Über die Umgebung, die in diesem Handbuch verwendeten

AD FS ist eine optionale Komponente von einem AD RMS-Installation. In diesem Handbuch wird die Verwendung von ADFS ausgegangen. Wenn AD FS in Ihrer Umgebung verwendet wurde noch nicht für die Unterstützung von AD RMS-Benutzer, können Sie alle Schritte überspringen, die auf AD FS verweisen.

In diesem Handbuch wird die SQL Server durch Ausführen einer parallelen Installation, und Verschieben von Datenbanken über über eine Sicherung auf SQL Server 2016 aktualisiert. Auch wenn Sie Ihre AD RMS und AD FS-Datenbankserver Direktes SQL Server 2016 aktualisieren können, können Sie mit dem nächsten Abschnitt in diesem Dokument verschieben nach müssen ausgeführt werden, ohne dass Sie die Schritte in diesem Abschnitt.  

## <a name="installation"></a>Installation

### <a name="configuring-sql-server-2016"></a>Konfigurieren von SQLServer 2016

Die folgenden Abschnitt Details Implementierungsaufgaben im Zusammenhang direkt an die SQL Server 2016-Konfiguration. Dieser Leitfaden konzentriert sich auf den Server-Manager und SQL Server Management Studio zum Ausführen dieser Aufgaben verwenden.

Diese Schritte müssen in einer SQL Server 2016-Installation ausgeführt werden. Installieren Sie SQL Server 2016 auf geeigneter Hardware gemäß den Standardmethoden Ihres Unternehmens und Richtlinien. 

#### <a name="preparing-the-sql-server"></a>Vorbereiten von SQLServer

Im folgende Abschnitt wird erläutert, wie die SQL-Server vorbereiten, damit sie auf SQL Server 2016 aktualisiert werden kann, vor dem Upgrade von anderen Diensten in der AD RMS-Plattform Windows Server 2016 verwenden.

##### <a name="adding-cname-for-sql-server-2016-to-dns"></a>DNS CNAME-Eintrag für SQLServer 2016 hinzufügt

Der CNAME-Eintrag wird verwendet, um sicherzustellen, dass das Windows Server 2016-Setup die erforderlichen Daten erhalten werden wird, da wurde an den neuen SQL Server 2016 gezeigt werden, wird. **Hinweis: Wenn Sie bereits einen CNAME-Eintrag für den AD FS und AD RMS-Dienst verwenden, können Sie mit den nächsten Schritten fortfahren.**


**So DNS einen CNAME-Eintrag für SQL Server 2016 hinzu**

1.  Melden Sie sich bei dem Windows Server 2012 R2-Domänencontroller mit Domain-Administratoranmeldeinformationen an.

2.  Öffnen Sie den Server-Manager.

3.  Klicken Sie auf **Tools** , und wählen Sie **DNS** zu DNS-Manager zu öffnen.

4.  Erweitern Sie den DC aus im linken Navigationsbereich, und öffnen Sie **Forward-Lookupzonen**.

5.  Öffnen Sie die Ressourcen der entsprechenden Domäne und dann klicken Sie mit der rechten Maustaste im rechten Ansicht aus, und wählen **neuer Alias (CNAME)** zu beginnen, den CNAME-Eintrag zu erstellen.

6.  Für der Aliasnamen ein. Geben Sie in ein logischer Namen für die Unterscheidung von anderen (ex möglicherweise vorhanden SQLADRMS oder SQLADFS)

7.  Geben Sie nach Eingabe des Namens den FQDN für den Zielhost, der den neuen SQL Server 2016-Server ist. (z. b. SQL2016.contoso.com)

8.  Nachdem alle Informationen eingegeben wurde, klicken Sie auf **OK**.

##### <a name="backup-the-ad-rms-and-adfs-databases"></a>Sichern der AD RMS und AD FS-Datenbanken

Die AD RMS und AD FS-Datenbanken enthalten wichtigen Informationen zu AD RMS, z. B. den öffentlichen Schlüssel des der Lizenzgebenden Serverzertifikats, Vorlagen für Benutzerrechterichtlinien, AD FS-Konfigurationsdaten und Protokollieren von Informationen erforderlich. Ohne diese Datenbanken können keine Clients Verwaltungslizenzen für die Nutzung geschützter Inhalte, neben anderen Problemen ausstellen.

Die Datenbanken, die AD RMS-Konfigurationsdatenbank gilt als am wichtigsten, speichert der SLC rights Richtlinienvorlagen Benutzer Schlüssel und Konfigurationsinformationen. Wenn Sie darauf achten sollten, um alle AD RMS und AD FS-Datenbanken zu sichern, sollten Sie daher die Konfigurationsdatenbank, regelmäßig zu sichern planen.

Die Datenbank speichert Informationen zu den benutzeranforderungen zum AD RMS-Clusters für Zertifikate und Nutzungslizenzen. Ihre Sicherungsstrategie für diese Datenbank sollte Ihrer Unternehmensrichtlinie für die Beibehaltung dieser Art von Informationen basieren.

Der Directory Services-Datenbank ist nicht entscheidend für AD RMS-Funktionalität und, wenn die neuesten Daten verloren geht, die Datenbank neu Auffüllen mit Informationen, wie der AD RMS-Server Anforderungen für Zertifikate empfängt und Lizenzen verwenden. Sie müssen sich nicht um diese Datenbank regelmäßig zu sichern, aber Sie müssen mindestens eine Kopie der Datenbank haben, wie es ursprünglich nach der Bereitstellung von AD RMS konfiguriert wurde.

**Sicherung einer AD RMS bzw. AD FS-Datenbank mit Microsoft SQL Server**

1.  Melden Sie sich an den Windows Server 2012 R2 AD RMS-Datenbank-Server mit SQL 2012.

2.  Klicken Sie auf **starten**, klicken Sie auf **Programme**, klicken Sie auf **Microsoft SQL Server**, und klicken Sie auf **SQL Server Management Studio**.

3.  In der **Herstellen einer Verbindung mit Server** Fenster bestätigen, dass der Hostserver für AD RMS-Datenbanken der **Servernamen** ein, und klicken Sie auf **Connect**.

4.  Erweitern Sie **Datenbanken**. Klicken Sie mit der rechten Maustaste auf die entsprechende Datenbank (**DRMS** und **Adfs**), zeigen Sie auf **Aufgaben**, und wählen Sie **Sicherung**.

5.  Wiederholen Sie Schritt 4 für die verbleibenden Datenbanken aus.

6.  Stellen Sie sicher, dass die Sicherung der Datenbanken von anderen Computern im Netzwerk oder einem Speichergerät verwenden, da sie während der Migration für die Verwendung in späteren Schritten benötigt werden, zugegriffen werden kann.

Jetzt können Sie die Kopien der Datenbank an einem sicheren Ort speichern. Denken Sie daran, Ihre Datenbanken regelmäßig sichern.

##### <a name="adding-domain-admin-sql-ad-rms-andor-adfs-service-account-to-sql-server-2016"></a>Hinzufügen von Domänen-Admins-Konto SQL, AD RMS und/oder AD FS-Dienst auf SQLServer 2016

Die folgenden Schritte aus Gerätepalette wie die verschiedenen Dienstkonten auf SQL Server 2016 zur Unterstützung beim Migrieren von Daten aus der Windows Server 2012 R2-Umgebung hinzugefügt. Dadurch erhalten die erforderlichen Berechtigungen, beim Versuch, den Zugriff auf den Inhalt und verarbeiten die Daten.

**SQL-Server die Domänen-Admins, SQL, AD RMS und/oder AD FS-Dienstkonto hinzu**

1.  Melden Sie sich an den Server mit SQL Server 2016 als das lokale Administratorkonto an.

2.  Klicken Sie auf **starten**, klicken Sie auf **Programme**, klicken Sie auf **Microsoft SQL Server**, und klicken Sie auf **SQL Server Management Studio**.

3.  In der **Herstellen einer Verbindung mit Server** Fenster bestätigen, dass der Hostserver für AD RMS-Datenbanken der **Servernamen** und dann für die Authentifizierung klicken Sie auf das Dropdownmenü und wählen Sie **SQL Server Authentifizierung**.

4.  In der **Anmeldung** Feld Geben Sie den Namen des lokalen Administratorkontos (z.B.) LocalAdmin), und klicken Sie dann das entsprechende Kennwort angeben, und klicken Sie auf **Connect**.

5.  Erweitern Sie **Sicherheit** , und klicken Sie dann mit der rechten Maustaste **Anmeldungen** , und wählen Sie **NewLogin** aus dem Kontextmenü, das angezeigt wird.

6.  Wenn das Fenster angezeigt wird, geben Sie in das Konto "Domänen-Admins" in der **Anmeldename** Feld (z.B.) Contoso\\ContosoAdmin)

7.  Wählen Sie im linken Navigationsbereich **Serverrollen**.

8.  Klicken Sie dann das Kontrollkästchen für **Sysadmin** unter der Server-Rollen und auf **OK**.

9.  Starten Sie neu **SQL Server-Verwaltung**.

10. In der **Herstellen einer Verbindung mit Server** Fenster bestätigen, dass der Hostserver für AD RMS-Datenbanken der **Servernamen** und dann für die Authentifizierung klicken Sie auf das Dropdownmenü und wählen Sie **Windows Authentifizierung** , und klicken Sie auf **Connect**.

##### <a name="restoring-the-ad-rms-and-adfs-databases-to-sql-server-2016"></a>Wiederherstellen der AD RMS und AD FS-Datenbanken zu SQLServer 2016

Die folgenden Schritte werden die Wiederherstellung von Daten aus der vorherigen SQL Server-Instanz zur neuen 2016-Instanz zu veranschaulichen. Dadurch wird die neue SQL relevante Konfigurationen für Daten aus den vorherigen AD RMS und AD FS-Datenbanken nutzen können.

**Zum Wiederherstellen der Daten aus der vorherigen SQL Server auf den neuen SQL Server**

1.  Melden Sie sich an den Server mit SQL Server 2016 mit dem entsprechenden Konto an.

2.  Klicken Sie im linken Navigationsbereich mit der Maustaste **Datenbanken** , und wählen Sie **Restore Database** um den Wiederherstellungsprozess zu starten.

3.  Klicken Sie unter **Quelle** wählen **Gerät** und navigieren Sie dann für den Speicherort, in dem die Datenbankdateien in den vorherigen Schritten gespeichert wurden.

4.  Nachdem die Dateien ausgewählt wurden, klicken Sie auf **OK**.

5.  Stellen Sie sicher, dass alle Datenbankdateien hinzugefügt wurden, und schließen den Prozess, indem Sie auf **OK**.

### <a name="configuring-windows-server-2016-active-directory-federation-services-ad-fs"></a>Konfigurieren von Windows Server 2016 Active Directory-Verbunddienste (AD FS)

AD FS wurde bereitgestellt, um einmaliges Anmelden (SSO) den Zugriff auf AD RMS als eine Anwendung bereitzustellen. Es wurde auch mit AD RMS Mobile Device Extension (MDE), konfiguriert die Mac- und Unterstützung für Benutzer mobiler Geräte ermöglicht.

Die folgenden Abschnitte enthalten Anleitungen auf operative Aufgaben müssen Sie möglicherweise für Ihre AD FS-Bereitstellung ausführen.

#### <a name="adding-a-2016-ad-fs-server-to-the-farm"></a>Hinzufügen eines 2016 AD FS-Servers zur Farm

Sie können zusätzliche AD FS-Server zur Unterstützung von AD RMS-Bereitstellung bereitstellen. Sie können zum Ausführen dieser Aktion bei stärkerer Datenverkehr zu den AD RMS-Server oder zusätzliche Anwendungen oder wenn Sie einen der Server derzeit für AD FS verwendeten außer Kraft setzen möchten.

**Auf den 2016-AD FS-Server der Farm hinzufügen**

1.  Azure AD Connect-Server, doppelklicken klicken Sie auf die **Azure AD Connect** Symbol, um den Azure AD Connect-Assistenten zu starten.

2.  Klicken Sie auf der Seite Willkommen auf **konfigurieren**.

3.  Klicken Sie auf der Seite zusätzliche Tasks auf **weiteren Verbundserver bereitstellen** , und klicken Sie dann auf **Weiter**.

4.  Verbindung mit Azure AD-Seite herstellen, geben Sie den Benutzernamen und das Kennwort eines Kontos mit globalen Administratorberechtigungen, und klicken Sie dann auf **Weiter**.

5.  In der Seite der Domänenadministrator-Anmeldeinformationen eingeben den Benutzernamen und das Kennwort eines Kontos mit Domänen-Admins-Berechtigungen, und klicken Sie auf **Weiter**.

6.  Klicken Sie auf **Durchsuchen** und wählen Sie die Zertifikatdatei wird, wenn verwendet Konfigurieren von Azure AD Connect mit AD FS-Farm.

7.  Klicken Sie auf **Geben Sie das Kennwort** das Zertifikatkennwort ein Dialogfeld zu öffnen.

8.  Geben Sie das Kennwort des Zertifikats in das Feld "Kennwort", und klicken Sie dann auf **OK**.

9.  Klicken Sie auf **Weiter**.

10. Geben Sie auf der AD FS-Server ein, den Namen oder die IP-Adresse des neuen AD FS-Servers ein, und klicken Sie auf **hinzufügen**.

11. Die bereit für die Seite "konfigurieren", klicken Sie auf **installieren**.

12. Klicken Sie auf der Seite Installation ist abgeschlossen auf **beenden**.

#### <a name="raising-the-adfs-farm-behavior-level"></a>Die AD FS-Farm mit Verhaltensebene auslösen

Wenn Sie einen ADFs-Server bereitstellen, der die aktuelle Umgebungsebene, z. B. überschreitet, müssen eine AD FS unter Windows Server 2012 R2 und klicken Sie dann auf Hinzufügen, dass eine AD FS Windows Server 2016, die Farmen mit Verhaltensebene erhöht werden müssen. Dies ist erforderlich, um sicherzustellen, dass die Umgebung die neuesten Informationen und Funktionen verwendet wird.

**Die AD FS-Farm mit Verhaltensebene ausgelöst werden soll.**

1.  Navigieren Sie zu den Windows Server 2016-ADFS.

2.  Öffnen Sie eine Administrator-PowerShell-Sitzung.

3.  Geben Sie den folgenden Befehl:  **\$Cred = Get-Credential**

4.  Geben Sie mit der ein Fenster wird angezeigt, in der die Anmeldeinformationen in den Anmeldeinformationen von Domänenadministratoren.

5.  Geben Sie dann diesen Befehl aus: **Invoke-AdfsFarmBehaviorLevelRaise -Credential \$cred**

6.  Eine Aufforderung erscheint werden Sie gefragt: **möchten Sie den Vorgang fortsetzen?** Geben Sie dann **eine** , akzeptieren die Eingabeaufforderung.

7.  Nachdem der Befehl abgeschlossen ist, wird die Farmen mit Verhaltensebene eingerichtet werden und bereit sind.

#### <a name="enabling-mobile-device-extension-logging"></a>Aktivieren der Protokollierung für Mobile Geräte-Erweiterung

Die Erweiterung für Mobile Geräte können Anforderungen protokollieren, die Empfang von Endbenutzergeräten. Protokollierung ist standardmäßig deaktiviert, und es wird empfohlen, nur Aktivieren der Protokollierung, die zur Problembehandlung. Alle Anforderungen von mobilen Geräten und Desktopcomputern, bootstrap, oder erwerben einer Lizenz für die Endbenutzer werden in der Datenbank für AD RMS-Protokollierung oder Azure Storage-Konto protokolliert. MDE-Protokollierung erstellt zwei weitere Tabellen mit der SQL Server mithilfe von AD RMS verwendet: den Client zu debuggen, Tabelle und der Client-Performance-Protokolltabelle.

**Zum Aktivieren der Protokollierung der Erweiterung für Mobile Geräte**

1.  Öffnen Sie in einem AD RMS-Server Windows PowerShell als Administrator aus.

2.  Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**: **Import-Module AdRmsAdmin**

3.  Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**: **New-PSDrive-Namen AdrmsCluster - PsProvider AdRmsAdmin-Stamm https://localhost**

4.  Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**: **Set-ItemProperty-Path AdrmsCluster:\\ -IsLoggingEnabled von Name-Wert \$"true"**

Wenn Sie für die Problembehandlung MDE-Protokollierung verwenden, wird empfohlen, sie nach Behebung des Problems zu deaktivieren.

**Zum Deaktivieren der Protokollierung der Erweiterung für Mobile Geräte**

1.  Öffnen Sie in einem AD RMS-Server Windows PowerShell als Administrator aus.

2.  Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**: **Import-Module AdRmsAdmin**

3.  Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**: **New-PSDrive-Namen AdrmsCluster - PsProvider AdRmsAdmin-Stamm https://localhost**

4.  Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**: **Set-ItemProperty-Path AdrmsCluster:\\ -IsLoggingEnabled von Name-Wert \$"false"**

### <a name="upgrading-ad-rms-to-windows-server-2016"></a>Aktualisieren von AD RMS auf WindowsServer 2016

Die folgenden Abschnitte enthalten Anleitungen zum Hinzufügen einer Windows Server 2016-basierten AD RMS-Server in der aktuellen Windows Server 2012 R2-Cluster. Der Server wird mit dem Cluster hinzugefügt werden, und die Informationen werden darin repliziert werden, so, dass der vorherige AD RMS-Server als veraltet markiert werden kann, um Ressourcen freizugeben.

Nachdem Sie eines, die Ihre AD RMS-Cluster Windows Server 2016-basierten AD RMS-Server hinzugefügt wurde hinzufügen, werden alle Knoten, die unter älteren Versionen von Windows nach inaktiv. Anschließend können Sie diese Server (z. B. Herunterfahren, wiederverwenden oder mit Windows Server 2016 auf dem AD RMS-Cluster beitreten neu installieren müssen) Bereitstellung aufheben. 

Sie können zusätzliche AD RMS-Server bereitstellen, mit dem Cluster, um die Last auf Ihrem AD RMS-Bereitstellung zu unterstützen. Sie können auch zum Ausführen dieser Aktion bei stärkerer Datenverkehr zu den AD RMS-Server auswählen.

Dieses Handbuch behandelt nicht, die erforderlichen Schritte zum Ändern des Lastenausgleich Mechanismen, die Sie möglicherweise in Ihrer Umgebung verwenden auf die Servern zu ausschließen, die Sie als veraltet markiert werden und die einzuschließen, die Sie mit dem Cluster hinzufügen. 

#### <a name="adding-a-2016-ad-rms-server"></a>Hinzufügen eines 2016 AD RMS-Servers

Wenn Ihr AD RMS-Cluster ein Hardwaresicherheitsmodul statt einem zentral verwalteten Schlüssel für die Lizenzgebenden Serverzertifikats verwendet wird, müssen Sie die Software und andere HSM-Artefakte (z. B. Schlüssel und die Sendeaktivität-Dateien) auf dem Server zu installieren, bevor die Installation von AD RMS. Sie müssen auch das HSM auf dem Server, entweder physisch oder über die Konfigurationen im relevanten Netzwerk zu verbinden. Führen Sie die HSM-Prozessleitfaden für die folgenden Schritte aus. 

**Hinzufügen eines 2016 AD RMS-Servers**

1.  Installieren Sie die AD RMS-Serverrolle, auf die gewünschte Windows Server 2016-Bereitstellung.

2.  Nach Abschluss der Installation wählen Sie den Link, um **zusätzliche Einstellungen konfigurieren**.

3.  Wählen Sie **beitreten zu einem vorhandenen AD RMS-Cluster** , und klicken Sie auf **Weiter**.

4.  Auf der **Konfigurationsdatenbank wählen** geben den CNAME-Eintrag im DNS für den 2016 SQLServer (FQDN) angegeben.

5.  Klicken Sie auf **Liste** auf der zweiten Zeile und wählen die **DefaultInstance** aus der Dropdownliste aus.

6.  Klicken Sie unter **Name der Standardkonfigurationsdatenbank**, wählen Sie im Dropdown-Menü, und wählen Sie die DRMS-Konfiguration, die angezeigt wird. Klicken Sie dann auf **Weiter**.

7.  Auf der **Datenbankinformationen** geben das Clusterschlüsselkennwort in das dafür vorgesehene Feld. Klicken Sie danach auf **Weiter**.

8.  In der nächsten Seite des Assistenten geben Sie den AD RMS-Dienstkonto, und geben Sie das Kennwort dafür, und klicken Sie auf **Weiter** Nachdem sie überprüft wurde.

9.  Sobald die **Clusterwebsite** Seite angezeigt wird, einfach sicherstellen, dass die entsprechende Website ausgewählt wurde, und klicken Sie auf **Weiter**.

10. Auf der **wählen Sie ein Serverauthentifizierungszertifikat** Seite, wählen Sie das importierte SSL-Zertifikat aus, und klicken Sie auf **Weiter**.

11. Klicken Sie auf **Installieren**, um die Installation zu starten.

12. Nach der Konfiguration abgeschlossen ist, müssen Sie sich ab- und wieder anmelden, um AD RMS verwalten.

13. Öffnen Sie nach der Anmeldung Back **Server-Manager** wählen **Tools** und dann **Active Directory Rights Management**. Das Fenster "Verwaltung" angezeigt werden soll, und um anzugeben, dass der Cluster die zusätzlichen Server im Cluster verfügt.

14. 14. Wenn die AD RMS-Erweiterung für Mobile Geräte in der ursprünglichen AD RMS-Cluster installiert wurde, müssen Sie auch MDE in den aktualisierten Clusterknoten installiert werden. Folgen Sie den Anweisungen in der Dokumentation zu MDE MDE Ihrer AD RMS-Cluster hinzu. An diesem Punkt können alle bereits vorhandenen Knoten wiederverwenden oder ein upgrade auf Windows Server 2016 und verknüpfen Sie sie erneut mit AD RMS-Clusters mit dem oben beschriebenen Verfahren. 

### <a name="configuring-windows-server-2016-web-application-proxy-wap"></a>Konfigurieren von Windows Server 2016-Webanwendungsproxy (WAP)

Die folgenden Abschnitte enthalten Anleitungen auf operative Aufgaben, die Sie möglicherweise auf Ihre Web Application Proxy-Bereitstellung vornehmen müssen. Dies ist ein optionaler Schritt, nicht erforderlich, wenn Sie AD RMS auf andere Art mit dem Internet veröffentlichen. 

#### <a name="adding-a-windows-server-2016-wap-server"></a>Hinzufügen eines Windows Server 2016-WAP-Servers

Sie können die zusätzlichen Webanwendungs-Proxyserver zur Unterstützung von AD RMS-Bereitstellung bereitstellen. Sie können zum Durchführen dieser Aktion im Fall von stärkerer Datenverkehr zu den AD RMS-Server oder wenn Sie einen der Server wird derzeit für den Webanwendungsproxy verwendet außer Kraft setzen müssen.

**Hinzufügen eines 2016 Webanwendungsproxy-Servers**

1.  Vom Server Sie Setup als Webanwendungs-Proxyserver möchten, navigieren Sie zu der Server-Manager-Konsole, und klicken Sie auf **Rollen und Features hinzufügen**.

2.  In der **Hinzufügen von Rollen und Features Assistenten**, klicken Sie auf **Weiter** bis Sie auf dem Auswahlbildschirm des Server-Rolle.

3.  Wählen Sie auf der Seite Serverrollen auswählen **RAS**, und klicken Sie dann auf **Weiter** bis Sie wieder auf dem Bildschirm Serverrollen auswählen können.

4.  Wählen Sie auf der Seite Serverrollen auswählen **Web Application Proxy**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.

5.  Klicken Sie auf dem Bildschirm "Installationsauswahl bestätigen" auf **installieren**.

6.  Nachdem die Installation abgeschlossen ist, klicken Sie auf **schließen**.

7.  Jetzt ist es Zeit für den Server zu konfigurieren. Zu diesem Zweck öffnen Sie die Remotezugriffs-Verwaltungskonsole auf dem Webanwendungsproxy-Server. Öffnen der **starten** Menü, Typ **RAMgmtUI.exe**, und wählen Sie dann die Anwendung.

8.  Klicken Sie im Navigationsbereich auf **Web Application Proxy**.

9.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **führen Sie die Web Application Proxy-Konfigurationsassistenten**. Einmal klicken Sie im Assistenten auf **Weiter**.

10. Geben Sie den vollqualifizierten Domänennamen des AD FS-Servers (ex, auf dem Verbundserver-Bildschirm "ADFS.contoso.com"), und geben Sie Anmeldeinformationen für einen Administrator auf dem AD FS-Server.

11. Wählen Sie auf dem Bildschirm "AD FS-Proxyzertifikat" in der Liste der derzeit auf dem Webanwendungsproxy-Server installierten Zertifikate ein Zertifikat vom Webanwendungsproxy für AD FS-Proxy verwendet werden, und klicken Sie dann auf **Weiter**.

12. Klicken Sie auf dem Bestätigungsbildschirm, überprüfen Sie die Einstellungen, und klicken Sie auf **konfigurieren**.

13. Nachdem die Konfiguration abgeschlossen ist, klicken Sie auf **schließen**.

#### <a name="dns-configuration-for-2016-wap-server"></a>DNS-Konfiguration für 2016-WAP-Servers

Sobald der Windows Server 2016-Webanwendungsproxy-Server direktes abgelegten müssen einige DNS-Änderungen vorgenommen werden. Dies erfordert, dass ein Dienst z. B. GoDaddy, zeigen Sie die AD FS und AD RMS-Dienste auf dem WAP-Server 2016 verwenden.

**Um das DNS auf dem WAP-Server zu verweisen**

1.  Navigieren Sie zur Ihres Anbieters-Website (z. b. GoDaddy).

2.  Wechseln Sie zur Domänenverwaltung, und klicken Sie dann DNS-Verwaltung.

3.  Suchen Sie den AD FS und AD RMS-Dienst, und Ersetzen Sie die **verweist auf** Teil mit der öffentlichen IP-Adresse des 2016 WAP-Servers und **speichern**.

4.  Die Änderungen dauern verteilt werden, aber sobald sie dies getan haben dieses Setup nicht abgeschlossen.

#### <a name="enabling-debugging-logs"></a>Aktivieren der Debug-Protokolle

Detaillierte Protokollinformationen ist auf den Webanwendungsproxy-Servern verfügbar. Sie können die erweiterten Debug-Protokollierung mithilfe der Ereignisanzeige konfigurieren. Zusätzliche Einstellungen können auch ausgewählt werden für die Größe der Protokolle, um sicherzustellen, dass die Analyse in der Ereignisanzeige nützlich sind.

**Aktivieren Debuggen Protokolle für den Webanwendungsproxy**

1.  Öffnen der **Ereignisanzeige** -Konsole auf den Webanwendungsproxy.

2.  Erweitern Sie die **Microsoft** Knoten.

3.  Erweitern Sie die **Windows** Knoten.

4.  Öffnen der **Web Application Proxy** Protokolle.

5.  Sie werden dann in der Lage sind, öffnen Sie die **Admin** Protokolle.

6.  Öffnen der **Aktion** Menü befindet sich in der oberen linken Ecke, und wählen **Eigenschaften**.

7.  Unter den **allgemeine** Registerkarte, wählen Sie die Option **Aktivieren der Protokollierung**.

8.  Schließlich können Sie sich zum Anpassen der maximalen Dateigröße und was geschieht, wenn die Maximalgröße des Ereignisprotokolls erreicht wird.

### <a name="configuring-high-availability-for-windows-server-2016-services"></a>Konfigurieren der hohen Verfügbarkeit für Windows Server 2016-Dienste

Die folgenden Abschnitte enthalten Anleitungen auf operative Aufgaben, die Sie möglicherweise Ihre Windows Server 2016-Umgebung hochverfügbarkeit einrichten müssen.

#### <a name="adding-a-2016-ad-rms-server-for-high-availability"></a>Hinzufügen eines 2016 AD RMS-Servers für hohe Verfügbarkeit

Sie können zusätzliche AD RMS-Server zum Einrichten von Hochverfügbarkeit bereitstellen. Sie können auswählen, zum Ausführen dieser Aktion bei stärkerer Datenverkehr zu den AD RMS-Server.

**Hinzufügen einen 2016 AD RMS-Server für hohe Verfügbarkeit**

1.  Installieren Sie die AD RMS-Serverrolle, auf die gewünschte Windows Server 2016-Bereitstellung.

2.  Nach Abschluss der Installation wählen Sie den Link, um **zusätzliche Einstellungen konfigurieren**.

3.  Wählen Sie **beitreten zu einem vorhandenen AD RMS-Cluster** , und klicken Sie auf **Weiter**.

4.  Auf der **Konfigurationsdatenbank wählen** geben den CNAME-Eintrag im DNS für den 2016 SQLServer (FQDN) angegeben.

5.  Klicken Sie auf **Liste** auf der zweiten Zeile und wählen die **DefaultInstance** aus der Dropdownliste aus.

6.  Klicken Sie unter **Name der Standardkonfigurationsdatenbank**, wählen Sie im Dropdown-Menü, und wählen Sie die DRMS-Konfiguration, die angezeigt wird. Klicken Sie dann auf **Weiter**.

7.  Auf der **Datenbankinformationen** geben das Clusterschlüsselkennwort in das dafür vorgesehene Feld. Klicken Sie danach auf **Weiter**.

8.  In der nächsten Seite des Assistenten geben Sie den AD RMS-Dienstkonto, und geben Sie das Kennwort dafür, und klicken Sie auf **Weiter** Nachdem sie überprüft wurde.

9.  Sobald die **Clusterwebsite** Seite angezeigt wird, einfach sicherstellen, dass die entsprechende Website ausgewählt wurde, und klicken Sie auf **Weiter**.

10. Auf der **wählen Sie ein Serverauthentifizierungszertifikat** Seite, wählen Sie das importierte SSL-Zertifikat aus, und klicken Sie auf **Weiter**.

11. Klicken Sie auf **Installieren**, um die Installation zu starten.

12. Nach der Konfiguration abgeschlossen ist, müssen Sie sich ab- und wieder anmelden, um AD RMS verwalten.

13. Öffnen Sie nach der Anmeldung Back **Server-Manager** wählen **Tools** und dann **Active Directory Rights Management**. Das Fenster "Verwaltung" angezeigt werden soll, und um anzugeben, dass der Cluster die zusätzlichen Server im Cluster verfügt.

14. Nach der Bestätigung des Server-Setups, können konfigurieren Sie den Lastenausgleich-Dienst für den Lastenausgleich zwischen den anderen AD RMS-Servern im Cluster.

#### <a name="adding-a-windows-server-2016-ad-fs-server-for-high-availability"></a>Hinzufügen eines Windows Server 2016 AD FS-Servers für hohe Verfügbarkeit

Sie können zusätzliche AD FS-Server zum Einrichten von Hochverfügbarkeit bereitstellen. Sie können auswählen, um diese Aktion bei stärkerer Datenverkehr zu den AD FS-Servern auszuführen. **Hinweis: nach dem Auslösen der Farmen mit verhaltensebene, ein neuen Datenbankeintrag eingegeben werden in den SQL Server 2016 (Adfs Configv3), und die alte Konfigurationsdatenbank muss gelöscht werden, bevor Sie mit den folgenden Schritten fortfahren.**

**Hinzufügen von Windows Server 2016 AD FS-Server für hohe Verfügbarkeit**

1.  Installieren Sie die AD RMS-Serverrolle, auf die gewünschte Windows Server 2016-Bereitstellung.

2.  Nach Abschluss der Installation wählen Sie den Link, um **konfigurieren Sie den Verbunddienst auf diesem Server**.

3.  Wählen Sie im Abschnitt Willkommen des Assistenten die Option zum **Hinzufügen eines Verbundservers zu einer Verbundserverfarm** , und klicken Sie dann auf **Weiter**.

4.  Geben Sie das richtige Administratorkonto ein, und klicken Sie auf **Weiter**.

5.  Auf der **Farm angeben** Seite, wählen Sie die **Geben Sie an der Datenbank für eine vorhandene Farm mithilfe von SQL Server** dann geben Sie den CNAME-Eintrag für den SQL-Dienst für den Hostnamen für die Datenbank, und klicken Sie auf **Weiter**.

6.  Unter den **angeben des Dienstkontos** Bereich des Assistenten geben Sie die Anmeldeinformationen für das AD FS-Dienstkonto, und klicken Sie dann auf **Weiter**.

7.  In **Optionen prüfen**, klicken Sie auf **Weiter**.

8.  Klicken Sie auf **konfigurieren** Wenn die Schaltfläche verfügbar wird.

9.  Starten Sie nach der Konfiguration den Computer neu.

10. Nach der Bestätigung des Server-Setups, Load Balancer die AD FS-Server nach Bedarf.

#### <a name="adding-a-windows-server-2016-wap-server-for-high-availability"></a>Hinzufügen eines Windows Server 2016-WAP-Servers für hohe Verfügbarkeit

Sie können die zusätzlichen WAP-Server zum Einrichten von Hochverfügbarkeit bereitstellen. Sie können auswählen, zum Ausführen dieser Aktion bei stärkerer Datenverkehr zu den AD RMS-Server.

**Hinzufügen eines Windows Server 2016-Webanwendungsproxy-Servers für hohe Verfügbarkeit**

1.  Vom Server Sie Setup als Webanwendungs-Proxyserver möchten, navigieren Sie zu der Server-Manager-Konsole, und klicken Sie auf **Rollen und Features hinzufügen**.

2.  In der **Hinzufügen von Rollen und Features Assistenten**, klicken Sie auf **Weiter** bis Sie auf dem Auswahlbildschirm des Server-Rolle.

3.  Wählen Sie auf der Seite Serverrollen auswählen **RAS**, und klicken Sie dann auf **Weiter** bis Sie wieder auf dem Bildschirm Serverrollen auswählen können.

4.  Wählen Sie auf der Seite Serverrollen auswählen **Web Application Proxy**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.

5.  Klicken Sie auf dem Bildschirm "Installationsauswahl bestätigen" auf **installieren**.

6.  Nachdem die Installation abgeschlossen ist, klicken Sie auf **schließen**.

7.  Jetzt ist es Zeit für den Server zu konfigurieren. Zu diesem Zweck öffnen Sie die Remotezugriffs-Verwaltungskonsole auf dem Webanwendungsproxy-Server. Öffnen der **starten** Menü, Typ **RAMgmtUI.exe**, und wählen Sie dann die Anwendung.

8.  Klicken Sie im Navigationsbereich auf **Web Application Proxy**.

9.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **führen Sie die Web Application Proxy-Konfigurationsassistenten**. Einmal klicken Sie im Assistenten auf **Weiter**.

10. Geben Sie den vollqualifizierten Domänennamen des AD FS-Servers (ex, auf dem Verbundserver-Bildschirm "ADFS.contoso.com"), und geben Sie Anmeldeinformationen für einen Administrator auf dem AD FS-Server.

11. Wählen Sie auf dem Bildschirm "AD FS-Proxyzertifikat" in der Liste der derzeit auf dem Webanwendungsproxy-Server installierten Zertifikate ein Zertifikat vom Webanwendungsproxy für AD FS-Proxy verwendet werden, und klicken Sie dann auf **Weiter**.

12. Klicken Sie auf dem Bestätigungsbildschirm, überprüfen Sie die Einstellungen, und klicken Sie auf **konfigurieren**.

13. Nachdem die Konfiguration abgeschlossen ist, klicken Sie auf **schließen**.

14. Nach der Bestätigung des Server-Setups, einen Lastenausgleich der WAP-Server im Umkreisnetzwerk.

#### <a name="adding-a-sql-server-2016-node-for-always-on-high-availability"></a>Hinzufügen eines SQL Server 2016-Knotens für hohe Verfügbarkeit mit AlwaysOn

Sie können zusätzliche SQL Server für hohe Verfügbarkeit mit AlwaysOn-setup bereitstellen. Sie können auswählen, zum Ausführen dieser Aktion bei stärkerer Datenverkehr zu den AD RMS-Server. **Hinweis: Stellen Sie sicher, dass beide SQL Server, den eingehenden Port 5022 geöffnet haben.**

**So fügen Sie einem SQL Server 2016-Server für hohe Verfügbarkeit mit AlwaysOn hinzu**

1.  Vom Server Sie Setup als zusätzliche SQL Server 2016-Server möchten, navigieren Sie zu der Server-Manager-Konsole, und klicken Sie auf **Rollen und Features hinzufügen**.

2.  Klicken Sie auf **Weiter** bis der **Features auswählen** Dialogfeld.

3.  Wählen Sie die **Failover-Clusterunterstützung** Kontrollkästchen. **Hinweis: Führen Sie diesen Schritt bei der ursprünglichen SQL Server 2016-Server aus, sodass beide SQL Server das Feature "Failoverclustering".**

4.  Klicken Sie auf **installieren** zum Installieren des Failoverclustering-Features.

5.  Öffnen Sie nun **Server-Manager** , und wählen Sie **Tools** dann **Failovercluster-Manager**.

6.  Klicken Sie im linken Menü Maustaste **Failovercluster-Manager** , und wählen Sie **Erstellen von Clustern**

7.  Dies öffnet die **Clustererstellungs-Assistenten**.

8.  Suchen Sie den SQL Server 2016-Servern, die für hohe Verfügbarkeit mit AlwaysOn verwendet werden, und geben Sie diese im klicken Sie dann auf **Weiter**.

9.  Sie erhalten eine validierungswarnung. Wählen Sie **Ja** , überprüfen die Clusterknoten, und klicken Sie dann auf **Weiter**.

10. Unter den **Testoptionen** Seite, wählen Sie die Option **Ausführen aller Tests** , und klicken Sie auf **weiter.**

11. **Hinweis: Den Clusterüberprüfungs-Assistenten wird erwartet, einige Warnmeldungen, zurückgeben, insbesondere dann, wenn Sie nicht über freigegebenen Speicher verwenden. Davon abgesehen, wenn Sie alle Fehlermeldungen finden müssen Sie vor dem Erstellen von Windows Server Failover Cluster Problembehebung**.

12. In der **Zugriffspunkt zum Verwalten des Clusters** Dialogfeld Geben Sie den Clusternamen und die virtuelle IP-Adresse für den Windows Server-Failovercluster, und klicken Sie dann **Weiter**.

13. Stellen Sie sicher, dass die Konfiguration erfolgreich **Zusammenfassung** , und klicken Sie auf **Fertig stellen**.

14. In der **Failovercluster-Manager** mit der rechten Maustaste auf Ihr Cluster, und wählen **Weitere Aktionen** wählen Sie dann **Clusterquorumeinstellungen konfigurieren**

15. Klicken Sie auf **Weiter** und wählen Sie dann die Option für **quorumzeugen auswählen** und klicken Sie auf **Weiter** erneut aus.

16. In der **Quorumzeuge auswählen** Seite die **konfigurieren ein dateifreigabezeugen** Option. Klicken Sie dann auf **Weiter**.

17. Wählen Sie **Durchsuchen** und suchen Sie den Pfad der Dateifreigabe, die Sie in das Dialogfeld für die Freigabe Pfad verwenden möchten. Klicken Sie auf **Weiter**.

18. Klicken Sie auf der Bestätigungsseite auf **Weiter**.

19. Klicken Sie auf der Seite Zusammenfassung auf **Fertig stellen**.

20. Öffnen Sie nun die **starten** Menü, und suchen Sie nach **SQL Server-Konfigurations-Manager**.

21. Mit der rechten Maustaste in des SQL Server-Namens, und wählen Sie **Eigenschaften**.

22. Wählen Sie im Dialogfeld "Eigenschaften" die **hohe Verfügbarkeit mit AlwaysOn** Registerkarte. Überprüfen Sie die **AlwaysOn-Verfügbarkeitsgruppen aktivieren** Kontrollkästchen. Klicken Sie auf **OK**. **Hinweis: dies sowohl auf SQLServer 2016-Servern.**

23. Klicken Sie dann starten Sie den SQL Server-Dienst neu.

24. Öffnen Sie nun die **starten** Menü, und suchen Sie nach **SQL Server Management Studio** , und klicken Sie im linken Navigationsbereich mit der Maustaste **Verfügbarkeitsgruppen** , und klicken Sie auf **Assistenten für neue Verfügbarkeitsgruppen** klicken Sie dann auf **Weiter**.

25. In der **Namen der Verfügbarkeitsgruppe angeben** Seite Wählen Sie einen Gruppennamen (Ex.SQLAvailabilityGroup2016). Klicken Sie dann auf **Weiter**.

26. Unter den **Datenbanken auswählen** Abschnitt, der die Datenbanken angeben. Klicken Sie anschließend auf Weiter. **Hinweis: Einige Datenbank muss u. u. erneut gesichert oder fügen Sie in der vollständige Wiederherstellungsmodus**.

27. Einmal auf die **Replikate angeben** klicken Sie auf die **Hinzufügen von Replikaten** Schaltfläche, und wählen Sie Ihre 2016 SQL Server.

28. Nach dem Hinzufügen des andere Servers, klicken Sie auf die Kontrollkästchen, und legen Sie den sekundären Server ein lesbares sekundäres Replikat sein.

29. Navigieren Sie zu der **Endpunkte** Registerkarte, und klicken Sie auf die **aktualisieren** Option. Und auch hier einen Bildlauf durch, und stellen Sie sicher, dass das gleiche Dienstkonto auf dem primären und sekundären Knoten ist.

30. Wählen Sie nun die **Sicherungseinstellungen** Registerkarte, und wählen Sie die **sekundären bevorzugen** Option.

31. Fahren mit dem **Listener** Registerkarte.

32. Geben Sie einen Namen (z.B.) SqlListener weitergegeben) und stellen Sie sicher, dass der Port **1433** , und klicken Sie dann auf **Weiter**.

33. In der **anfängliche Datensynchronisierung auswählen** Seite des Assistenten wählen Sie die **vollständige** aus, und geben Sie Speicherort im Netzwerk zugegriffen werden kann, indem alle SQL Server, und klicken Sie dann auf **Weiter**.

34. Klicken Sie abschließend auf **Fertig stellen** und der Vorgang wird abgeschlossen.

### <a name="decommission-windows-server-2012-r2-nodes"></a>Außerbetriebnahme von Windows Server 2012 R2-Knoten

Die folgenden Abschnitte enthalten Hinweise auf operative Aufgaben, die Sie möglicherweise Ihre Windows Server 2012 R2-Server entfernen, die nach der erfolgreichen Aktualisierung von AD RMS-Clusters auf Windows Server 2016.

#### <a name="removing-a-windows-server-2012-r2-ad-rms-server"></a>Entfernen ein Windows Server 2012 R2 AD RMS-Server

Sie können nicht benötigte AD RMS-Server nach dem Upgrade entfernen. Sie können auswählen, um diese Aktion auszuführen, wenn er für die Außerbetriebnahme von AD RMS-Server benötigt wird.

**So entfernen Sie eine** **Windows Server 2012 R2 AD RMS-Server**

1.  Wählen Sie auf dem Windows Server 2012 R2 AD RMS-Server im Server-Manager **verwalten** von oben nach rechts Menüs, und wählen Sie dann **Entfernen von Rollen und Features**.

2.  Die **Entfernen von Rollen und Features Assistenten** wird geöffnet, oben "und" auf die **Vorbemerkungen** auf **Weiter**.

3.  Auf der **Serverauswahl** Bildschirm, klicken Sie auf **Weiter**.

4.  Auf der **Serverrollen** Bildschirm, entfernen Sie das Kontrollkästchen neben **Active Directory Rights Management Services** , und klicken Sie auf **Weiter**.

5.  Auf der **Features** Bildschirm, klicken Sie auf **Weiter**.

6.  Auf der **Bestätigung** Bildschirm, klicken Sie auf **entfernen**.

7.  Sobald dies abgeschlossen ist, starten Sie den Server neu.

8.  Sie können jetzt Herunterfahren auf diesem Server und die Ressourcen neu zuteilt, je nach Bedarf.
