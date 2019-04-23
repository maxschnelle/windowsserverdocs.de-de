---
ms.assetid: 963a3d37-d5f1-4153-b8d5-2537038863cb
title: Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 67b122353ca9dff3a4df6cbfac56b16bed52b539
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848081"
---
# <a name="best-practices-for-secure-planning-and-deployment-of-ad-fs"></a>Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält bewährte Methoden-Informationen zur Planung und Auswertung von Sicherheit beim Entwerfen Ihrer Bereitstellung von Active Directory-Verbunddienste (AD FS). Dieses Thema ist ein Ausgangspunkt für die Prüfung und Bewertung von Überlegungen, die die allgemeine Sicherheit bei der Verwendung von AD FS auswirken. Die Informationen in diesem Thema sollen Ihre vorhandene Sicherheitsplanung und andere bewährte Entwurfsmethoden ergänzen und erweitern.  
  
## <a name="core-security-best-practices-for-ad-fs"></a>Wichtige bewährte Sicherheitsmethoden für AD FS  
Die folgenden wichtigen bewährten Sicherheitsmethoden gelten für alle AD FS-Installationen, wo Sie möchten verbessern oder erweitern die Sicherheit des Entwurfs oder der Bereitstellung werden:  
  
-   **Verwenden des Sicherheitskonfigurations-Assistenten AD FS-spezifischen bewährten Sicherheitsmethoden für Verbundserver- und Verbundserverproxy-Computer anwenden**  
  
    (Security Configuration Wizard, SCW) ist ein Tool, das auf alle Windows Server 2008, Windows Server 2008 R2 und Windows Server 2012-Computer vorinstalliert ist. Sie können mit dem Assistenten bewährte Sicherheitsmethoden anwenden, die dazu beitragen, die Angriffsfläche für einen Server auf der Basis der von Ihnen installierten Serverrollen zu reduzieren.  
  
    Wenn Sie AD FS installieren, erstellt das Setupprogramm Rollenerweiterungsdateien mit dem Sicherheitskonfigurations-Assistenten, um eine Sicherheitsrichtlinie zu erstellen, die für die bestimmte AD FS-Serverrolle (Verbundserver oder Verbundserverproxy) angewendet wird, die Sie während des Setups auswählen.  
  
    Jede installierte Rollenerweiterungsdatei stellt den Rollen- und Unterrollentyp dar, für den jeder Computer konfiguriert ist. Die folgenden rollenerweiterungsdateien werden im C:WindowsADFSScw Verzeichnis installiert:  
  
    -   Farm.xml  
  
    -   SQLFarm.xml  
  
    -   StandAlone.xml  
  
    -   Proxy.xml (Diese Datei ist nur vorhanden, wenn der Computer in der Verbundserverproxy-Rolle konfiguriert wurde.)  
  
    Führen Sie die folgenden Schritte in der angegebenen Reihenfolge durch, um die AD FS-Rollenerweiterungen im Sicherheitskonfigurations-Assistenten zuzuweisen:  
  
    1.  Installieren Sie AD FS, und wählen Sie die geeignete Serverrolle für diesen Computer aus. Weitere Informationen finden Sie unter [Verbunddienst-Rollendienst installieren](../../ad-fs/deployment/Install-the-Federation-Service-Proxy-Role-Service.md) in AD FS-Bereitstellungshandbuch.  
  
    2.  Registrieren Sie die geeignete Rollenerweiterungsdatei mit dem Scwcmd-Befehlszeilentool. Ausführliche Informationen zur Verwendung des Tools in der Rolle, für die Ihr Computer konfiguriert ist, finden Sie in der folgenden Tabelle.  
  
    3.  Stellen Sie sicher, dass der Befehl erfolgreich abgeschlossen wurde, mithilfe der Datei scwregister_log.XML untersuchen, die sich im Verzeichnis WindowssecurityMsscwLogs befindet.  
  
    Sie müssen all diese Schritte auf jedem Verbundserver- oder Verbundserverproxy-Computer durchführen, für den Sie AD FS-basierte Sicherheitsrichtlinien des Sicherheitskonfigurations-Assistenten anwenden möchten.  
  
    In der folgenden Tabelle wird erklärt, wie Sie die geeignete Rollenerweiterung des Sicherheitskonfigurations-Assistenten auf der Basis der AD FS-Serverrolle registrieren, die Sie auf dem Computer ausgewählt haben, auf dem AD FS installiert ist.  
  
    |AD FS-Serverrolle|Verwendete AD FS-Konfigurationsdatenbank|Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein:|  
    |---------------------|-------------------------------------|---------------------------------------------------|  
    |Eigenständiger Verbundserver|Interne Windows-Datenbank|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwStandAlone.xml"`|  
    |Einer Farm angehöriger Verbundserver|Interne Windows-Datenbank|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwFarm.xml"`|  
    |Einer Farm angehöriger Verbundserver|SQL Server|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwSQLFarm.xml"`|  
    |Verbundserverproxy|Nicht zutreffend|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwProxy.xml"`|  
  
    Weitere Informationen zu den Datenbanken, die Sie mit AD FS verwenden können, finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   **Verwenden Sie Erkennung von tokenwiederholungen in Situationen, in denen Sicherheit sehr wichtig ist, z. B. ist wenn Kiosks verwendet werden.**  
    Erkennung von tokenwiederholungen ist ein Feature von AD FS, die sicherstellt, dass jeder Versuch der Wiederholung einer tokenanforderung, die an den Verbunddienst vorgenommen wird, wird erkannt, und die Anforderung wird verworfen. Die Erkennung von Tokenwiederholungen ist standardmäßig aktiviert. Sie funktioniert sowohl für das passive WS-Verbundprofil als auch das Security Assertion Markup Language (SAML)-WebSSO-Profil, indem sie sicherstellt, dass dasselbe Token niemals mehr als einmal verwendet wird.  
  
    Wenn der Verbunddienst gestartet wird, wird ein Cache aller erfüllten Tokenanforderungen aufgebaut. Wenn mit der Zeit anschließende Tokenanforderungen zum Cache hinzugefügt werden, hat der Verbunddienst immer bessere Möglichkeiten, alle Versuche der mehrmaligen Wiederholung von Tokenanforderungen zu erkennen. Wenn Sie Erkennung von Tokenwiederholungen deaktivieren und später entscheiden, sie erneut zu aktivieren, denken Sie daran, dass der Verbunddienst für einen gewissen Zeitraum weiterhin Token akzeptiert, die zuvor verwendet wurden, bis der Wiederholungscache ausreichend Zeit erhält, seine Inhalte aufzubauen. Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   **Verwenden der tokenverschlüsselung, insbesondere dann, wenn Sie unterstützende SAML-artefaktauflösung verwenden.**  
  
    Verschlüsselung von Token wird dringend empfohlen, zum Erhöhen der Sicherheit und Schutz vor potenziellen Man-in-the-Middle (MITM)-Angriffe, die für Ihre AD FS-Bereitstellung ausgeführt werden kann. Die Verwendung der Verschlüsselung hat möglicherweise geringfügige allgemeine Auswirkungen, aber in der Regel sollten diese nicht bemerkbar sein, und in vielen Bereitstellungen überwiegen die Vorteile einer höheren Sicherheit alle Nachteile hinsichtlich der Serverleistung.  
  
    Zum Aktivieren der Tokenverschlüsselung fügen Sie zuerst ein Verschlüsselungszertifikat für die Vertrauensstellungen der vertrauenden Seite hinzu. Sie können ein Verschlüsselungszertifikat entweder bei der Erstellung einer Vertrauensstellung der vertrauenden Seite oder später erstellen. Sie können ein Zertifikat zur Verwendung für festlegen, um ein Verschlüsselungszertifikat später zu einer vorhandenen Vertrauensstellung der vertrauenden hinzufügen, die **Verschlüsselung** im Eigenschaften der Vertrauensstellung bei der Verwendung von AD FS-Snap-in auf der Registerkarte. Um ein Zertifikat für eine vorhandene Vertrauensstellung mit der AD FS-Cmdlets angeben, verwenden Sie den Parameter "EncryptionCertificate" entweder die **Set-ClaimsProviderTrust** oder **Set-RelyingPartyTrust** Cmdlets. Um ein Zertifikat für den Verbunddienst zur Entschlüsselung von Token festzulegen, verwenden die **Set-ADFSCertificate** Cmdlet, und geben Sie "`Token-Encryption`" für die *CertificateType* Parameter. Die Aktivierung und Deaktivierung der Verschlüsselung für eine bestimmte Vertrauensstellung der vertrauenden Seite kann über den Parameter *EncryptClaims* des Cmdlets **Set-RelyingPartyTrust** durchgeführt werden.  
  
-   **Verwenden des erweiterten Schutzes zur Authentifizierung**  
  
    Um Ihre Bereitstellungen zu schützen, können Sie festlegen und den erweiterten Schutz für Authentifizierungsfunktion mit AD FS verwenden. Diese Einstellung gibt an, die Stufe des erweiterten Schutzes zur Authentifizierung von einem Verbundserver unterstützt wird.  
  
    Der erweiterte Schutz für die Authentifizierung trägt dazu bei, Schutz vor Man-in-the-Middle-Angriffen (MITM) bereitzustellen, bei denen ein Angreifer Clientanmeldeinformationen abfängt und an einen Server weiterleitet. Der Schutz vor solchen Angriffen wird durch ein Kanalbindungstoken ermöglicht, das vom Server erfordert, zugelassen oder nicht erfordert wird, wenn diese eine Kommunikation mit Clients einrichtet.  
  
    Zur Aktivierung der Funktion für den erweiterten Schutz verwenden Sie den Parameter **ExtendedProtectionTokenCheck** des Cmdlets **Set-ADFSProperties**. Mögliche Werte für diese Einstellung und die Sicherheitsstufe, die der jeweilige Wert bereitstellt, sind in der folgenden Tabelle beschrieben.  
  
    |Parameterwert|Sicherheitsstufe|Schutzeinstellung|  
    |-------------------|------------------|----------------------|  
    |Require|Die Sicherheit des Servers ist vollständig verstärkt.|Der erweiterte Schutz wird erzwungen und ist immer erforderlich.|  
    |Zulassen|Die Sicherheit des Servers ist teilweise verstärkt.|Der erweiterte Schutz wird erzwungen, wenn die beteiligten Systeme einen Patch erhalten haben, um diesen zu unterstützen.|  
    |Keine|Der Server ist anfällig.|Der erweiterte Schutz wird nicht erzwungen.|  
  
-   **Wenn Sie Protokollierung und Ablaufverfolgung verwenden, stellen Sie auf den Datenschutz für alle sensiblen Informationen sicher.**  
  
    AD FS, in der Standardeinstellung verfügbar machen oder nicht persönlich identifizierbare Informationen (PII) direkt als Teil des Verbunddiensts oder normaler Vorgänge überwachen. Bei der Protokollierung von Komponentenereignissen und Debug-ablaufverfolgungsprotokollierung in AD FS aktiviert sind, können jedoch abhängig von der Richtlinie für Ansprüche, die Sie konfigurieren, dass einige Ansprüche Typen und die zugehörigen Werte personenbezogene Informationen enthalten, die in der AD FS-Ereignis oder Ablaufverfolgungsprotokollen protokolliert sein können.  
  
    Aus diesem Grund wird das Erzwingen einer Zugriffssteuerung für die AD FS-Konfiguration und ihre Protokolldateien dringend empfohlen. Wenn diese Art von Informationen nicht sichtbar sein soll, sollten Sie die Protokollierung deaktivieren oder alle personenbezogenen Informationen oder sensiblen Daten in Ihren Protokollen herausfiltern, bevor Sie diese mit anderen gemeinsam verwenden.  
  
    Die folgenden Tipps können Ihnen helfen, die Inhalte einer Protokolldatei nicht versehentlich verfügbar zu machen:  
  
    -   Stellen Sie sicher, dass das AD FS-Ereignisprotokoll und die Ablaufverfolgungs-Protokolldateien durch Access Control Lists (ACL) geschützt sind, die Zugriff auf die vertrauenswürdige Administratoren einschränken, die Zugriff darauf benötigen.  
  
    -   Kopieren oder archivieren Sie Protokolldateien nicht mit Dateierweiterungen oder Pfaden, die einfach über eine Webanforderung bereitgestellt werden können. Beispielsweise ist die Dateinamenerweiterung .xml keine sichere Option. Im Administratorhandbuch für die Internetinformationsdienste finden Sie eine Liste der Erweiterungen, die bereitgestellt werden können.  
  
    -   Wenn Sie den Pfad zur Protokolldatei überprüfen, stellen Sie sicher, dass Sie einen absoluten Pfad für den Speicherort der Protokolldatei angeben, der außerhalb öffentlichen Verzeichnisses des virtuellen Webhoststamms liegt, um zu verhindern, dass eine externe Partei über einen Webbrowser darauf zugreifen kann.  

-   **Soft-Extranetsperre von AD FS und AD FS Extranet intelligente Schutz durch Kontosperrung**  
    
    Bei einem Angriff in Form von authentifizierungsanforderungen invalid(bad) Kennwörter, die über den Webanwendungsproxy stammen, können AD FS extranet Lockout Sie Ihre Benutzer vor einer AD FS-kontosperrung zu schützen. Zusätzlich zum Schutz von Benutzern aus einem AD FS-kontosperrung, AD FS extranet Lockout schützt auch Kennwortermittlung brute-Force-Angriffe.  
    
    Weiche Extranetsperre für AD FS unter Windows Server 2012 R2 finden Sie unter [AD FS vorläufig Extranetsperrschutz](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md).  

     Extranet Smart Lockout für AD FS unter Windows Server 2016 finden Sie unter [AD FS intelligente Extranetsperrschutz](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md).  
  
## <a name="sql-serverspecific-security-best-practices-for-ad-fs"></a>Wichtige SQL Server-spezifische bewährte Sicherheitsmethoden für AD FS  
Die folgenden bewährten Sicherheitsmethoden sind spezifisch für die Verwendung von Microsoft SQL Server® oder Windows Internal Database (WID), wenn diese datenbanktechnologien verwendet werden, um Daten in AD FS-Entwurfs und der Bereitstellung zu verwalten.  
  
> [!NOTE]  
> Die Empfehlungen sollen SQL Server-Produktsicherheitsanleitungen ergänzen, aber nicht ersetzen. Weitere Informationen zur Planung einer sicheren SQL Server-Installation finden Sie unter [Überlegungen zur Sicherheit für eine sichere SQL-Installation](https://go.microsoft.com/fwlink/?LinkID=139831) (https://go.microsoft.com/fwlink/?LinkID=139831).  
  
-   **Bereitstellen von SQL Server immer hinter einer Firewall in einem physisch sicheren Netzwerkumgebung.**  
  
    Eine SQL Server-Installation sollte niemals direkt für das Internet verfügbar gemacht werden. Nur Computer, die in Ihrem Rechenzentrum befinden muss SQL Server-Installation zu erreichen, die AD FS unterstützt. Weitere Informationen finden Sie unter [Prüfliste für bewährte Sicherheitsmethoden](https://go.microsoft.com/fwlink/?LinkID=189229) (https://go.microsoft.com/fwlink/?LinkID=189229).  
  
-   **Führen Sie SQL Server unter einem Dienstkonto anstelle der integrierten Standardsystem-Dienstkonten.**  
  
    Standardmäßig wird SQL Server oft installiert und konfiguriert, um eins der unterstützten integrierten Systemkonten zu verwenden, beispielsweise das LocalSystem- oder das NetworkService-Konto. Um die Sicherheit von SQL Server-Installation für AD FS zu verbessern, ganz egal, wo möglich ein separates Dienstkonto für den Zugriff auf Ihre SQL Server-Dienst und Kerberos-Authentifizierung aktivieren, indem Sie den Sicherheitsprinzipalnamen (SPN) dieses Kontos registrieren Ihre Active Directory-Bereitstellung. Damit wird eine gegenseitige Authentifizierung zwischen Client und Server ermöglicht. Ohne SPN-Registrierung eines separaten Dienstkontos verwendet SQL Server NTLM für die Windows-basierte Authentifizierung, bei der nur der Client authentifiziert wird.  
  
-   **Minimieren Sie die Oberfläche von SQL Server.**  
  
    Aktivieren Sie nur die SQL Server-Endpunkte, die erforderlich sind. Standardmäßig stellt SQL Server einen einzigen integrierten TCP-Endpunkt bereit, der nicht entfernt werden kann. Für AD FS sollten Sie diesen TCP-Endpunkt für die Kerberos-Authentifizierung aktivieren. Zum Überprüfen der aktuellen TCP-Endpunkte, um zu sehen, ob zusätzliche benutzerdefinierte TCP-Ports zu einer SQL-Installation hinzugefügt werden, können Sie die Abfrageanweisung „SELECT * FROM sys.tcp_endpoints“ in einer Transact-SQL-Sitzung (T-SQL) verwenden. Weitere Informationen zu SQL Server-Endpunktkonfiguration, finden Sie unter [so wird's gemacht: Konfigurieren Sie die Datenbank-Engine zum Überwachen mehrerer TCP-Ports](https://go.microsoft.com/fwlink/?LinkID=189231) (https://go.microsoft.com/fwlink/?LinkID=189231).  
  
-   **Verwenden Sie SQL-basierte Authentifizierung.**  
  
    Damit Sie Kennwörter nicht in Klartext über Ihrer Netzwerk übertragen oder in Konfigurationseinstellungen speichern müssen, verwenden Sie nur die Windows-Authentifizierung mit Ihrer SQL Server-Installation. Die SQL Server-Authentifizierung ist ein Legacyauthentifizierungsmodus. Das Speichern von SQL-Anmeldeinformationen (SQL-Benutzernamen und -Kennwörter) bei der Verwendung der SQL Server-Authentifizierung ist nicht empfehlenswert. Weitere Informationen finden Sie unter [Authentifizierungsmodi](https://go.microsoft.com/fwlink/?LinkID=189232) (https://go.microsoft.com/fwlink/?LinkID=189232).  
  
-   **Bewerten Sie die Notwendigkeit zusätzliche kanalsicherheit in Ihrer SQL-Installation sorgfältig.**  
  
    Selbst bei wirksamer Kerberos-Authentifizierung bietet die SQL Server Security Support Provider-Schnittstelle (SSPI) keine Sicherheit auf Kanalebene. Für Installationen, bei denen sich Server sicher in einem durch eine Firewall geschützten Netzwerk befinden, ist eine Verschlüsselung der SQL-Kommunikation möglicherweise jedoch nicht erforderlich.  
  
    Auch wenn die Verschlüsselung ein wertvolles Tool ist, um für Sicherheit zu sorgen, sollte sie nicht für alle Daten oder Verbindungen in Betracht gezogen werden. Wenn Sie entscheiden, ob Sie eine Verschlüsselung implementieren, bedenken Sie, wie Benutzer auf Daten zugreifen. Wenn Benutzer über ein öffentliches Netzwerk auf Daten zugreifen, ist eine Datenverschlüsselung möglicherweise erforderlich, um die Sicherheit zu erhöhen. Jedoch, wenn alle Zugriff auf SQL-Daten von AD FS eine sichere Intranetkonfiguration abspielt, möglicherweise Verschlüsselung nicht erforderlich sein. Jede Verschlüsselungsverwendung beinhaltet auch eine Wartungsstrategie für Kennwörter, Schlüssel und Zertifikate.  
  
    Wenn Sie Bedenken haben, dass SQL-Daten möglicherweise in Ihrem Netzwerk gesehen oder manipuliert werden, verwenden Sie die Internetprotokollsicherheit (IPsec) oder Secure Sockets Layer (SSL), um Ihre SQL-Verbindungen zu sichern. Allerdings möglicherweise dies negative Auswirkungen auf die Leistung von SQL Server, die möglicherweise Auswirkungen auf oder AD FS-Leistung in einigen Fällen zu beschränken. AD FS-Leistung bei der tokenausstellung kann z. B. beeinträchtigt werden, wenn das Abrufen von Attributen aus einem SQL-basierten Attributspeicher wichtig für die tokenausstellung sind. Sie können eine SQL-Manipulationsbedrohung einfacher vermeiden, indem Sie eine robuste Umkreissicherheitskonfiguration haben. Für eine bessere Lösung für das Sichern einer SQL Server-Installation sollten Sie beispielsweise sicherstellen, dass sie für Internetbenutzer und -computer nicht zugänglich ist und der Zugriff nur für Benutzer oder Computer in Ihrer Rechenzentrumsumgebung möglich ist.  
  
    Weitere Informationen finden Sie unter [Verschlüsseln von Verbindungen zu SQL Server](https://go.microsoft.com/fwlink/?LinkID=189234) oder [SQL Server-Verschlüsselung](https://go.microsoft.com/fwlink/?LinkID=189233).  
  
-   **Konfigurieren Sie mithilfe von gespeicherten Prozeduren zum Ausführen von Lookups aller SQL-basierten AD FS der SQL-gespeicherten Daten sicher entworfenen Zugriff.**  
  
    Für eine bessere Dienst- und Datenisolierung können Sie gespeicherte Verfahren für alle Abrufbefehle für den Attributspeicher erstellen. Sie können eine Datenbankrolle erstellen, der Sie dann die Berechtigung erteilen, die gespeicherten Verfahren auszuführen. Weisen Sie dieser Datenbankrolle die Dienstidentität des AD FS-Windows-Diensts. Der AD FS-Windows-Dienst sollte nicht zu einer anderen SQL-Anweisung als die entsprechenden gespeicherten Prozeduren ausführen, die für die Attributsuche verwendet werden können. Wenn Sie den Zugriff auf die SQL Server-Datenbank auf diese Weise sperren, reduzieren Sie das Risiko von Rechteerweiterungsangriffen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
