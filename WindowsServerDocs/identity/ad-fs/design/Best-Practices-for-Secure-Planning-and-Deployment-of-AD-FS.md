---
ms.assetid: 963a3d37-d5f1-4153-b8d5-2537038863cb
title: Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: be488ccffee7b267d2a3a120b85436abf206f65a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359201"
---
# <a name="best-practices-for-secure-planning-and-deployment-of-ad-fs"></a>Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS


Dieses Thema enthält Informationen zu bewährten Methoden zum Planen und Auswerten der Sicherheit beim Entwerfen Ihrer Active Directory-Verbunddienste (AD FS)-Bereitstellung (AD FS). Dieses Thema ist ein Ausgangspunkt für die Überprüfung und Bewertung von Überlegungen, die sich auf die allgemeine Sicherheit der Verwendung von AD FS auswirken. Die Informationen in diesem Thema sollen Ihre vorhandene Sicherheitsplanung und andere bewährte Entwurfsmethoden ergänzen und erweitern.  
  
## <a name="core-security-best-practices-for-ad-fs"></a>Wichtige bewährte Sicherheitsmethoden für AD FS  
Die folgenden grundlegenden bewährten Methoden gelten für alle AD FS Installationen, bei denen Sie die Sicherheit Ihres Entwurfs oder Ihrer Bereitstellung verbessern oder erweitern möchten:  

-   **Sicheres AD FS als System der Ebene 0** 

    AD FS ist im Grunde genommen ein Authentifizierungssystem.  Daher sollte Sie als "Tier 0"-System wie das andere Identitätssystem in Ihrem Netzwerk behandelt werden.  In [Microsoft-Dokumentation](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material) finden Sie weitere Informationen zum Modell der Active Directory administrativen Ebene. 


-   **Verwenden des Sicherheitskonfigurations-Assistenten zum Anwenden AD FS spezifischer bewährter Sicherheitsmethoden auf Verbund Server und Verbund Server Proxy-Computer**  
  
    Der Sicherheitskonfigurations-Assistent (Security Configuration Wizard, SCW) ist ein Tool, das auf allen Computern unter Windows Server 2008, Windows Server 2008 R2 und Windows Server 2012 vorinstalliert ist. Sie können mit dem Assistenten bewährte Sicherheitsmethoden anwenden, die dazu beitragen, die Angriffsfläche für einen Server auf der Basis der von Ihnen installierten Serverrollen zu reduzieren.  
  
    Wenn Sie AD FS installieren, erstellt das Setupprogramm Rollenerweiterungsdateien mit dem Sicherheitskonfigurations-Assistenten, um eine Sicherheitsrichtlinie zu erstellen, die für die bestimmte AD FS-Serverrolle (Verbundserver oder Verbundserverproxy) angewendet wird, die Sie während des Setups auswählen.  
  
    Jede installierte Rollenerweiterungsdatei stellt den Rollen- und Unterrollentyp dar, für den jeder Computer konfiguriert ist. Die folgenden Rollen Erweiterungs Dateien werden im Verzeichnis "c:windowsadf SSCW" installiert:  
  
    -   Farm.xml  
  
    -   SQLFarm.xml  
  
    -   StandAlone.xml  
  
    -   Proxy.xml (Diese Datei ist nur vorhanden, wenn der Computer in der Verbundserverproxy-Rolle konfiguriert wurde.)  
  
    Führen Sie die folgenden Schritte in der angegebenen Reihenfolge durch, um die AD FS-Rollenerweiterungen im Sicherheitskonfigurations-Assistenten zuzuweisen:  
  
    1.  Installieren Sie AD FS, und wählen Sie die geeignete Serverrolle für diesen Computer aus. Weitere Informationen finden Sie unter [Installieren des Verbunddienstproxy-Rollen Dienstanbieter](../../ad-fs/deployment/Install-the-Federation-Service-Proxy-Role-Service.md) im AD FS Bereitstellungs Handbuch.  
  
    2.  Registrieren Sie die geeignete Rollenerweiterungsdatei mit dem Scwcmd-Befehlszeilentool. Ausführliche Informationen zur Verwendung des Tools in der Rolle, für die Ihr Computer konfiguriert ist, finden Sie in der folgenden Tabelle.  
  
    3.  Überprüfen Sie, ob der Befehl erfolgreich abgeschlossen wurde, indem Sie die Datei "SCWRegister_log. xml" untersuchen, die sich im Verzeichnis "windowssecuritymsscwlogs" befindet.  
  
    Sie müssen all diese Schritte auf jedem Verbundserver- oder Verbundserverproxy-Computer durchführen, für den Sie AD FS-basierte Sicherheitsrichtlinien des Sicherheitskonfigurations-Assistenten anwenden möchten.  
  
    In der folgenden Tabelle wird erklärt, wie Sie die geeignete Rollenerweiterung des Sicherheitskonfigurations-Assistenten auf der Basis der AD FS-Serverrolle registrieren, die Sie auf dem Computer ausgewählt haben, auf dem AD FS installiert ist.  
  
    |AD FS-Serverrolle|Verwendete AD FS-Konfigurationsdatenbank|Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein:|  
    |---------------------|-------------------------------------|---------------------------------------------------|  
    |Eigenständiger Verbundserver|Interne Windows-Datenbank|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwStandAlone.xml"`|  
    |Einer Farm angehöriger Verbundserver|Interne Windows-Datenbank|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwFarm.xml"`|  
    |Einer Farm angehöriger Verbundserver|SQL Server|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwSQLFarm.xml"`|  
    |Verbundserverproxy|Nicht zutreffend|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwProxy.xml"`|  
  
    Weitere Informationen zu den Datenbanken, die Sie mit AD FS verwenden können, finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   **Verwenden Sie die Erkennung von tokenwiederholungen in Situationen, in denen die Sicherheit ein sehr wichtiges Problem ist, z. b. wenn Kiosk verwendet werden.**  
    Die Erkennung von tokenreplay ist eine Funktion von AD FS, mit der sichergestellt wird, dass jeder Versuch, eine Tokenanforderung wiederzugeben, die an der Verbunddienst erfolgt, erkannt wird und die Anforderung verworfen wird. Die Erkennung von Tokenwiederholungen ist standardmäßig aktiviert. Sie funktioniert sowohl für das passive WS-Verbundprofil als auch das Security Assertion Markup Language (SAML)-WebSSO-Profil, indem sie sicherstellt, dass dasselbe Token niemals mehr als einmal verwendet wird.  
  
    Wenn der Verbunddienst gestartet wird, wird ein Cache aller erfüllten Tokenanforderungen aufgebaut. Wenn mit der Zeit anschließende Tokenanforderungen zum Cache hinzugefügt werden, hat der Verbunddienst immer bessere Möglichkeiten, alle Versuche der mehrmaligen Wiederholung von Tokenanforderungen zu erkennen. Wenn Sie Erkennung von Tokenwiederholungen deaktivieren und später entscheiden, sie erneut zu aktivieren, denken Sie daran, dass der Verbunddienst für einen gewissen Zeitraum weiterhin Token akzeptiert, die zuvor verwendet wurden, bis der Wiederholungscache ausreichend Zeit erhält, seine Inhalte aufzubauen. Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   **Verwenden Sie die tokenverschlüsselung, insbesondere dann, wenn Sie unterstützende SAML-artefaktauflösung verwenden.**  
  
    Die Verschlüsselung von Token wird dringend empfohlen, um die Sicherheit und den Schutz vor potenziellen man-in-the-Middle-Angriffen (MITM) zu erhöhen, die möglicherweise für Ihre AD FS-Bereitstellung ausprobiert werden. Die Verwendung der Verschlüsselung hat möglicherweise geringfügige allgemeine Auswirkungen, aber in der Regel sollten diese nicht bemerkbar sein, und in vielen Bereitstellungen überwiegen die Vorteile einer höheren Sicherheit alle Nachteile hinsichtlich der Serverleistung.  
  
    Zum Aktivieren der Tokenverschlüsselung fügen Sie zuerst ein Verschlüsselungszertifikat für die Vertrauensstellungen der vertrauenden Seite hinzu. Sie können ein Verschlüsselungszertifikat entweder bei der Erstellung einer Vertrauensstellung der vertrauenden Seite oder später erstellen. Wenn Sie einer vorhandenen Vertrauensstellung der vertrauenden Seite ein Verschlüsselungs Zertifikat hinzufügen möchten, können Sie ein Zertifikat für die Verwendung auf der Registerkarte **Verschlüsselung** innerhalb von Vertrauens Eigenschaften festlegen, während Sie das AD FS-Snap-in verwenden. Zum Angeben eines Zertifikats für eine vorhandene Vertrauensstellung mithilfe der AD FS-Cmdlets verwenden Sie den Parameter "verschlüsselungcertificate" der Cmdlets " **Set-claimsprovidertrust** " oder " **Set-relyingpartytrust** ". Wenn Sie ein Zertifikat für den Verbunddienst festlegen möchten, das beim Entschlüsseln von Token verwendet werden soll, verwenden Sie das Cmdlet **Set-adfscertificate** , und geben Sie für den Parameter *certifikatetype* "`Token-Encryption`" an. Die Aktivierung und Deaktivierung der Verschlüsselung für eine bestimmte Vertrauensstellung der vertrauenden Seite kann über den Parameter *EncryptClaims* des Cmdlets **Set-RelyingPartyTrust** durchgeführt werden.  
  
-   **Verwenden des erweiterten Schutzes für die Authentifizierung**  
  
    Um Ihre bereit Stellungen zu sichern, können Sie die Funktion erweiterter Schutz für die Authentifizierung mit AD FS festlegen und verwenden. Diese Einstellung gibt die Ebene des erweiterten Schutzes für die Authentifizierung an, die von einem Verbund Server unterstützt wird.  
  
    Der erweiterte Schutz für die Authentifizierung trägt dazu bei, Schutz vor Man-in-the-Middle-Angriffen (MITM) bereitzustellen, bei denen ein Angreifer Clientanmeldeinformationen abfängt und an einen Server weiterleitet. Der Schutz vor solchen Angriffen wird durch ein Kanalbindungstoken ermöglicht, das vom Server erfordert, zugelassen oder nicht erfordert wird, wenn diese eine Kommunikation mit Clients einrichtet.  
  
    Zur Aktivierung der Funktion für den erweiterten Schutz verwenden Sie den Parameter **ExtendedProtectionTokenCheck** des Cmdlets **Set-ADFSProperties**. Mögliche Werte für diese Einstellung und die Sicherheitsstufe, die der jeweilige Wert bereitstellt, sind in der folgenden Tabelle beschrieben.  
  
    |Parameterwert|Sicherheitsstufe|Schutzeinstellung|  
    |-------------------|------------------|----------------------|  
    |Require|Die Sicherheit des Servers ist vollständig verstärkt.|Der erweiterte Schutz wird erzwungen und ist immer erforderlich.|  
    |Zulassen|Die Sicherheit des Servers ist teilweise verstärkt.|Der erweiterte Schutz wird erzwungen, wenn die beteiligten Systeme einen Patch erhalten haben, um diesen zu unterstützen.|  
    |Keine|Der Server ist anfällig.|Der erweiterte Schutz wird nicht erzwungen.|  
  
-   **Wenn Sie Protokollierung und Ablauf Verfolgung verwenden, stellen Sie sicher, dass alle vertraulichen Informationen vertraulich sind.**  
  
    In AD FS werden personenbezogene Informationen (PII) nicht standardmäßig direkt als Teil der Verbunddienst oder normalen Vorgänge bereitgestellt oder nachverfolgt. Wenn die Ereignisprotokollierung und die Debugprotokollierung der Ablauf Verfolgung in AD FS aktiviert sind, können jedoch in Abhängigkeit von der von Ihnen konfigurierten Anspruchs Richtlinie einige Anspruchs Typen und die zugehörigen Werte personenbezogene Personen enthalten, die möglicherweise im AD FS Ereignis oder in den Ablauf Verfolgungs Protokollen protokolliert werden.  
  
    Daher wird dringend empfohlen, die Zugriffs Steuerung für die AD FS Konfiguration und die zugehörigen Protokolldateien zu erzwingen. Wenn diese Art von Informationen nicht sichtbar sein soll, sollten Sie die Protokollierung deaktivieren oder alle personenbezogenen Informationen oder sensiblen Daten in Ihren Protokollen herausfiltern, bevor Sie diese mit anderen gemeinsam verwenden.  
  
    Die folgenden Tipps können Ihnen helfen, die Inhalte einer Protokolldatei nicht versehentlich verfügbar zu machen:  
  
    -   Stellen Sie sicher, dass die AD FS Ereignisprotokoll-und Ablauf Verfolgungs Protokolldateien durch Zugriffs Steuerungs Listen (Access Control Lists, ACL) geschützt sind, die den Zugriff auf vertrauenswürdige Administratoren beschränken, die Zugriff auf Sie benötigen.  
  
    -   Kopieren oder archivieren Sie Protokolldateien nicht mit Dateierweiterungen oder Pfaden, die einfach über eine Webanforderung bereitgestellt werden können. Beispielsweise ist die Dateinamenerweiterung .xml keine sichere Option. Im Administratorhandbuch für die Internetinformationsdienste finden Sie eine Liste der Erweiterungen, die bereitgestellt werden können.  
  
    -   Wenn Sie den Pfad zur Protokolldatei überprüfen, stellen Sie sicher, dass Sie einen absoluten Pfad für den Speicherort der Protokolldatei angeben, der außerhalb öffentlichen Verzeichnisses des virtuellen Webhoststamms liegt, um zu verhindern, dass eine externe Partei über einen Webbrowser darauf zugreifen kann.  

-   **AD FS Extranet Soft Lockout und AD FS Extranet Smart Lockout Protection**  
    
    Bei einem Angriff in Form von Authentifizierungsanforderungen mit ungültigen (ungültigen) Kenn Wörtern, die den webanwendungsproxy durchlaufen, können Sie mit AD FS extranetsperre Ihre Benutzer vor einer AD FS Konto Sperre schützen. Zusätzlich zum Schutz Ihrer Benutzer vor einer AD FS Konto Sperre schützt AD FS extranetsperrungs-Lock auch vor Brute-Force-Kenn Wort Angriffen.  
    
    Informationen zur vorläufigen Sperre für die Extranet-Sperre für AD FS unter Windows Server 2012 R2 finden [Sie unter AD FS Extranet Soft Lockout Protection](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md).  

     Informationen zur Extranet Smart Lockout for AD FS auf Windows Server 2016 finden [Sie unter AD FS Extranet Smart Lockout Protection](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md).  
  
## <a name="sql-serverspecific-security-best-practices-for-ad-fs"></a>Wichtige SQL Server-spezifische bewährte Sicherheitsmethoden für AD FS  
Die folgenden bewährten Sicherheitsmethoden gelten speziell für die Verwendung von Microsoft SQL Server® oder der internen Windows-Datenbank (WID), wenn diese Datenbanktechnologien zum Verwalten von Daten in AD FS Entwurf und Bereitstellung verwendet werden.  
  
> [!NOTE]  
> Die Empfehlungen sollen SQL Server-Produktsicherheitsanleitungen ergänzen, aber nicht ersetzen. Weitere Informationen zum Planen einer sicheren SQL Server-Installation finden Sie unter [Sicherheitsüberlegungen für eine sichere SQL-Installation](https://go.microsoft.com/fwlink/?LinkID=139831) (https://go.microsoft.com/fwlink/?LinkID=139831).  
  
-   **Stellen Sie SQL Server hinter einer Firewall stets in einer physisch sicheren Netzwerkumgebung bereit.**  
  
    Eine SQL Server-Installation sollte niemals direkt für das Internet verfügbar gemacht werden. Nur Computer innerhalb Ihres Rechenzentrums sollten in der Lage sein, die SQL Server-Installation zu erreichen, die AD FS unterstützt. Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden Checkliste](https://go.microsoft.com/fwlink/?LinkID=189229) (https://go.microsoft.com/fwlink/?LinkID=189229).  
  
-   **Führen Sie SQL Server unter einem Dienst Konto aus, statt die integrierten Standard-Systemdienst Konten zu verwenden.**  
  
    Standardmäßig wird SQL Server oft installiert und konfiguriert, um eins der unterstützten integrierten Systemkonten zu verwenden, beispielsweise das LocalSystem- oder das NetworkService-Konto. Um die Sicherheit Ihrer SQL Server Installation für AD FS zu verbessern, verwenden Sie, sofern möglich, ein separates Dienst Konto für den Zugriff auf Ihren SQL Server Dienst, und aktivieren Sie die Kerberos-Authentifizierung, indem Sie den Sicherheits Prinzipal Namen (SPN) dieses Kontos in Ihrem Active Directory Bereitstellung. Damit wird eine gegenseitige Authentifizierung zwischen Client und Server ermöglicht. Ohne SPN-Registrierung eines separaten Dienstkontos verwendet SQL Server NTLM für die Windows-basierte Authentifizierung, bei der nur der Client authentifiziert wird.  
  
-   **Minimieren Sie den Oberflächen Bereich SQL Server.**  
  
    Aktivieren Sie nur die SQL Server-Endpunkte, die erforderlich sind. Standardmäßig stellt SQL Server einen einzigen integrierten TCP-Endpunkt bereit, der nicht entfernt werden kann. Für AD FS sollten Sie diesen TCP-Endpunkt für die Kerberos-Authentifizierung aktivieren. Zum Überprüfen der aktuellen TCP-Endpunkte, um zu sehen, ob zusätzliche benutzerdefinierte TCP-Ports zu einer SQL-Installation hinzugefügt werden, können Sie die Abfrageanweisung „SELECT * FROM sys.tcp_endpoints“ in einer Transact-SQL-Sitzung (T-SQL) verwenden. Weitere Informationen zur SQL Server Endpunkt Konfiguration finden Sie unter [gewusst wie: Konfigurieren Sie die Datenbank-Engine für das lauschen an mehreren TCP-Ports @ no__t-0 (https://go.microsoft.com/fwlink/?LinkID=189231).  
  
-   **Vermeiden Sie die Verwendung der SQL-basierten Authentifizierung.**  
  
    Damit Sie Kennwörter nicht in Klartext über Ihrer Netzwerk übertragen oder in Konfigurationseinstellungen speichern müssen, verwenden Sie nur die Windows-Authentifizierung mit Ihrer SQL Server-Installation. Die SQL Server-Authentifizierung ist ein Legacyauthentifizierungsmodus. Das Speichern von SQL-Anmeldeinformationen (SQL-Benutzernamen und -Kennwörter) bei der Verwendung der SQL Server-Authentifizierung ist nicht empfehlenswert. Weitere Informationen finden Sie unter [Authentifizierungs Modi](https://go.microsoft.com/fwlink/?LinkID=189232) (https://go.microsoft.com/fwlink/?LinkID=189232).  
  
-   **Evaluieren Sie die Notwendigkeit zusätzlicher Channelsicherheit in der SQL-Installation sorgfältig.**  
  
    Selbst bei wirksamer Kerberos-Authentifizierung bietet die SQL Server Security Support Provider-Schnittstelle (SSPI) keine Sicherheit auf Kanalebene. Für Installationen, bei denen sich Server sicher in einem durch eine Firewall geschützten Netzwerk befinden, ist eine Verschlüsselung der SQL-Kommunikation möglicherweise jedoch nicht erforderlich.  
  
    Auch wenn die Verschlüsselung ein wertvolles Tool ist, um für Sicherheit zu sorgen, sollte sie nicht für alle Daten oder Verbindungen in Betracht gezogen werden. Wenn Sie entscheiden, ob Sie eine Verschlüsselung implementieren, bedenken Sie, wie Benutzer auf Daten zugreifen. Wenn Benutzer über ein öffentliches Netzwerk auf Daten zugreifen, ist eine Datenverschlüsselung möglicherweise erforderlich, um die Sicherheit zu erhöhen. Wenn allerdings der Zugriff auf SQL-Daten durch AD FS eine sichere Intranetkonfiguration umfasst, ist die Verschlüsselung möglicherweise nicht erforderlich. Jede Verschlüsselungsverwendung beinhaltet auch eine Wartungsstrategie für Kennwörter, Schlüssel und Zertifikate.  
  
    Wenn Sie Bedenken haben, dass SQL-Daten möglicherweise in Ihrem Netzwerk gesehen oder manipuliert werden, verwenden Sie die Internetprotokollsicherheit (IPsec) oder Secure Sockets Layer (SSL), um Ihre SQL-Verbindungen zu sichern. Dies kann jedoch eine negative Auswirkung auf die SQL Server Leistung haben, die AD FS Leistung in einigen Situationen beeinträchtigen oder einschränken kann. Beispielsweise kann AD FS Leistung bei der Tokenausstellung beeinträchtigt werden, wenn Attribut Suchvorgänge aus einem SQL-basierten Attribut Speicher für die Tokenausstellung wichtig sind. Sie können eine SQL-Manipulationsbedrohung einfacher vermeiden, indem Sie eine robuste Umkreissicherheitskonfiguration haben. Für eine bessere Lösung für das Sichern einer SQL Server-Installation sollten Sie beispielsweise sicherstellen, dass sie für Internetbenutzer und -computer nicht zugänglich ist und der Zugriff nur für Benutzer oder Computer in Ihrer Rechenzentrumsumgebung möglich ist.  
  
    Weitere Informationen finden Sie unter [Verschlüsseln von Verbindungen mit SQL Server](https://go.microsoft.com/fwlink/?LinkID=189234) oder [SQL Server Verschlüsselung](https://go.microsoft.com/fwlink/?LinkID=189233).  
  
-   **Konfigurieren Sie den sicheren Zugriff mithilfe von gespeicherten Prozeduren, um alle SQL-basierten Suchvorgänge durch AD FS von SQL-gespeicherten Daten auszuführen.**  
  
    Für eine bessere Dienst- und Datenisolierung können Sie gespeicherte Verfahren für alle Abrufbefehle für den Attributspeicher erstellen. Sie können eine Datenbankrolle erstellen, der Sie dann die Berechtigung erteilen, die gespeicherten Verfahren auszuführen. Weisen Sie der Daten Bank Rolle die Dienst Identität des AD FS Windows-Dienstanbieter zu. Der AD FS Windows-Dienst sollte keine andere SQL-Anweisung ausführen können, außer den entsprechenden gespeicherten Prozeduren, die für die Attribut Suche verwendet werden. Wenn Sie den Zugriff auf die SQL Server-Datenbank auf diese Weise sperren, reduzieren Sie das Risiko von Rechteerweiterungsangriffen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
