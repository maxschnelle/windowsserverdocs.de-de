---
ms.assetid: 963a3d37-d5f1-4153-b8d5-2537038863cb
title: "Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ed8c36d4bec455879ffd00ad40b72fd5e90484ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="best-practices-for-secure-planning-and-deployment-of-ad-fs"></a>Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält bewährte Informationen zum Planen und auswerten Sicherheit beim Entwerfen Ihrer Bereitstellung von Active Directory-Verbunddienste (AD FS). In diesem Thema ist ein Ausgangspunkt für die Überprüfung und Auswertung von Überlegungen, die die allgemeine Sicherheit bei der Verwendung von AD FS betreffen. Die Informationen in diesem Thema ist Entwurfsmethoden ergänzen und erweitern Ihre vorhandene sicherheitsplanung und andere Bewährte Entwurfsmethoden vorgesehen.  
  
## <a name="core-security-best-practices-for-ad-fs"></a>Wichtige bewährte Sicherheitsmethoden für AD FS  
Die folgenden wichtigen bewährten Sicherheitsmethoden gelten für alle AD FS-Installationen, wo Sie möchten verbessern oder erweitern die Sicherheit des Entwurfs oder der Bereitstellung werden:  
  
-   **Verwenden des Sicherheitskonfigurations-Assistenten zum Anwenden von AD FS-spezifischen bewährten Sicherheitsmethoden für Verbundserver- und Verbundserverproxy-Computer**  
  
    (Security Configuration Wizard, SCW) ist ein Tool, das auf allen Windows Server 2008, Windows Server 2008 R2 und Windows Server 2012-Computer vorinstalliert ist. Sie können es verwenden, Sicherheitsmethoden anwenden, bewährte Methoden, die Ihnen helfen, der Angriffsfläche für einen Server reduzieren, basierend auf den Serverrollen, die Sie installieren.  
  
    Bei der Installation von AD FS erstellt das Setupprogramm Rolle Erweiterungsdateien, die Sie mit dem Sicherheitskonfigurations-Assistenten verwenden können, um eine Sicherheitsrichtlinie erstellen, die auf die bestimmte AD FS-Serverrolle (Verbundserver oder Verbundserverproxy) angewendet wird, die Sie während des Setups auswählen.  
  
    Jede Rolle Extension-Datei, die installiert wird stellt den Typ der Rollen- und unterrollentyp für die einzelnen Computer konfiguriert ist. Die folgenden rollenerweiterungsdateien werden im Verzeichnis C:WindowsADFSScw installiert:  
  
    -   Farm.Xml  
  
    -   SQLFarm.xml  
  
    -   StandAlone.xml  
  
    -   Proxy.XML (diese Datei ist nur vorhanden, wenn Sie den Computer in der Verbundserverproxy-Rolle konfiguriert.)  
  
    Wenn die AD FS-Rolle Erweiterungen für den Sicherheitskonfigurations-Assistenten anwenden möchten, müssen führen Sie die folgenden Schritte in der Reihenfolge aus:  
  
    1.  Installieren Sie AD FS, und wählen Sie die geeignete Serverrolle für diesen Computer. Weitere Informationen finden Sie unter [Verbunddienst-Rollendienst installieren](../../ad-fs/deployment/Install-the-Federation-Service-Proxy-Role-Service.md) in AD FS-Bereitstellungshandbuch.  
  
    2.  Registrieren Sie die geeignete rollenerweiterungsdatei mit dem Scwcmd-Befehlszeilentool. Finden Sie in der folgenden Tabelle finden Sie Details zur Verwendung dieses Tools in der Rolle für die der Computer konfiguriert ist.  
  
    3.  Stellen Sie sicher, dass der Befehl erfolgreich ausgeführt wurde, die Datei scwregister_log.XML untersuchen, die sich im Verzeichnis WindowssecurityMsscwLogs befindet.  
  
    Auf jedem Verbundserver oder Verbundserverproxy-Computer, dem Sie AD FS-basierte Sicherheitsrichtlinien anwenden möchten, müssen Sie alle diese Schritte ausführen.  
  
    In der folgende Tabelle wird erläutert, wie die geeignete rollenerweiterung, basierend auf dem AD FS-Serverrolle, die Sie auf dem Computer ausgewählt haben, auf dem AD FS installiert, registrieren.  
  
    |AD FS-Serverrolle|AD FS-Konfigurationsdatenbank verwendet|Geben Sie folgenden Befehl an einer Eingabeaufforderung ein:|  
    |---------------------|-------------------------------------|---------------------------------------------------|  
    |Eigenständiger Verbundserver|Interne Windows-Datenbank|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwStandAlone.xml"`|  
    |Einer Farm Angehöriger Verbundserver|Interne Windows-Datenbank|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwFarm.xml"`|  
    |Einer Farm Angehöriger Verbundserver|SqlServer|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwSQLFarm.xml"`|  
    |Verbundserverproxy|N/V|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwProxy.xml"`|  
  
    Weitere Informationen zu den Datenbanken, die Sie mit AD FS verwenden können, finden Sie unter [die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   **Verwenden Sie Erkennung von tokenwiederholungen in Situationen, in der Sicherheit sehr wichtig ist, z. B. wenn Kioske verwendet werden.**  
    Erkennung von tokenwiederholungen ist ein Feature von AD FS, die sicherstellt, dass jeder Versuch der Wiederholung einer tokenanforderung, die an den Verbunddienst vorgenommen wird erkannt, und die Anforderung verworfen. Erkennung von tokenwiederholungen ist standardmäßig aktiviert. Es funktioniert für das passive WS-Federation-Profil und das Security Assertion Markup Language (SAML)-WebSSO-Profil, indem Sie sicherstellen, dass dasselbe Token niemals mehr als einmal verwendet wird.  
  
    Wenn der Verbunddienst gestartet wird, beginnt es einen Cache aller erfüllten tokenanforderungen aufgebaut. Im Laufe der Zeit anschließende tokenanforderungen zum Cache hinzugefügt werden erhöht sich die Fähigkeit, erkennen alle Versuche, Wiederholung einer tokenanforderung mehrmals für den Verbunddienst. Wenn Sie die Erkennung von tokenwiederholungen deaktivieren und später entscheiden, sie erneut zu aktivieren, denken Sie daran, dass der Verbunddienst weiterhin Token für einen gewissen Zeitraum akzeptieren, die zuvor verwendet wurden, bis der Cache Replay genug Zeit gewährt, seine Inhalte aufzubauen. Weitere Informationen finden Sie unter [die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   **Verwenden der tokenverschlüsselung, insbesondere dann, wenn Sie die unterstützende SAML-artefaktauflösung verwenden.**  
  
    Verschlüsselung von Token wird dringend empfohlen, zum Erhöhen der Sicherheit und Schutz vor potenziellen Man-in-the-Middle (MITM)-Angriffen, die vor der Bereitstellung von AD FS versucht werden kann. Verwendung der Verschlüsselung möglicherweise eine geringe Auswirkung auf in der gesamten jedoch im Allgemeinen ist es sollte nicht bemerkbar sein und in vielen Bereitstellungen überschreiten die Vorteile für eine höhere Sicherheit alle Nachteile hinsichtlich der Leistung.  
  
    Klicken Sie zum Aktivieren der tokenverschlüsselung ersten Satz ein Verschlüsselungszertifikat für Vertrauensstellungen der vertrauenden Seite hinzufügen. Sie können ein Verschlüsselungszertifikat entweder beim Erstellen einer der vertrauenden Seite der Vertrauensstellung Partei oder höher. Sie können ein Zertifikat zur Verwendung auf festlegen, um ein Verschlüsselungszertifikat später zu einer vorhandenen Vertrauensstellung für vertrauende Seiten hinzuzufügen, die **Verschlüsselung** Registerkarte in Eigenschaften der Vertrauensstellung bei der Verwendung von AD FS-Snap-in. Verwenden Sie zum Angeben eines Zertifikats für eine vorhandene Vertrauensstellung mit der AD FS-Cmdlets den Parameter "EncryptionCertificate" des entweder die **Set-ClaimsProviderTrust** oder **Set-RelyingPartyTrust** Cmdlets. Verwenden Sie zum Festlegen eines Zertifikats für den Verbunddienst zur Entschlüsselung von Token der **Set-ADFSCertificate** Cmdlet, und geben Sie "`Token-Encryption`" für die *CertificateType* Parameter. Aktivieren und Deaktivieren der Verschlüsselung für bestimmte vertrauende vertrauen, können Sie dazu die *EncryptClaims* -Parameter von der **Set-RelyingPartyTrust** Cmdlet.  
  
-   **Verwenden des erweiterten Schutzes für die Authentifizierung**  
  
    Um Ihre Bereitstellungen zu sichern, können Sie festlegen und verwenden den erweiterten Schutz für Authentifizierungsfeature mit AD FS. Diese Einstellung gibt die Ebene der erweiterten Schutz für die Authentifizierung von einem Verbundserver unterstützt werden.  
  
    Der erweiterte Schutz für die Authentifizierung schützt vor Man-in-the-Middle (MITM)-Angriffe, in denen ein Angreifer Clientanmeldeinformationen abfängt und an einen Server weiterleitet. Schutz vor solchen Angriffen wird durch einen Kanal Binding Token (CBT) ermöglicht die können entweder erforderlich, zugelassen, oder werden nicht vom Server erforderlich, wenn sie die Kommunikation mit Clients einrichtet.  
  
    Um die erweiterten Schutz zu aktivieren, verwenden Sie die **ExtendedProtectionTokenCheck** Parameter auf die **Set-ADFSProperties** Cmdlet. Mögliche Werte für diese Einstellung und die Sicherheitsstufe, die die Werte angeben, werden in der folgenden Tabelle beschrieben.  
  
    |Parameterwert|Sicherheitsstufe|Die Einstellung Schutz|  
    |-------------------|------------------|----------------------|  
    |Erfordern|Server ist vollständig verstärkt.|Der erweiterte Schutz wird erzwungen, und immer erforderlich.|  
    |Zulassen|Servers ist teilweise verstärkt.|Der erweiterte Schutz wird erzwungen, in denen beteiligten Systeme einen Patch erhalten haben, für die Unterstützung.|  
    |Keine|Der Server ist anfällig.|Der erweiterte Schutz wird nicht erzwungen.|  
  
-   **Wenn Sie die Protokollierung und Ablaufverfolgung verwenden, stellen Sie den Datenschutz für alle sensiblen Informationen sicher.**  
  
    AD FS nicht standardmäßig oder Verfolgung von persönlich identifizierbare Informationen (PII) direkt als Teil des Verbunddiensts oder normaler Vorgänge. Wenn in AD FS-ereignisprotokollierung und Debug-ablaufverfolgungsprotokollierung aktiviert sind, können jedoch je nach der Richtlinie Ansprüche, einige Ansprüche zu konfigurieren Typen und die zugehörigen Werte PII enthalten, die in der AD FS-Ereignis oder Ablaufverfolgungsprotokollen protokolliert werden kann.  
  
    Aus diesem Grund wird das Erzwingen der Zugriffssteuerung auf die AD FS-Konfiguration und ihre Protokolldateien dringend empfohlen. Wenn Sie nicht, dass diese Art von Informationen angezeigt werden möchten, sollten Sie herausfiltern deaktivieren oder alle personenbezogenen Informationen oder sensiblen Daten in Ihren Protokollen filtern, bevor Sie mit anderen zu teilen.  
  
    Die folgenden Tipps helfen Ihnen die verhindern, dass des Inhalts einer Protokolldatei nicht versehentlich verfügbar:  
  
    -   Stellen Sie sicher, dass der AD FS-Ereignisprotokoll und Ablaufverfolgungsprotokoll-Dateien durch Zugriffssteuerungslisten (ACLs) geschützt sind, die Zugriff auf die vertrauenswürdige Administratoren einschränken, wer Zugriff darauf benötigen.  
  
    -   Kopieren Sie oder Sie keine archivieren Sie Protokolldateien, die mit Dateierweiterungen oder Pfaden, die einfach über eine webanforderung bereitgestellt werden können. Beispielsweise ist die XML-Erweiterung nicht sichere Option. Sie können überprüfen, die Internetinformationsdienste (Internet Information Services, IIS)-Administratorhandbuch zum Anzeigen einer Liste der Erweiterungen, die bereitgestellt werden können.  
  
    -   Wenn Sie den Pfad der Protokolldatei ändern, achten Sie darauf, dass Sie einen absoluten Pfad für den Speicherort der Protokolldatei an, der außerhalb des Web-Host virtuellen webhoststamms öffentlichen Verzeichnisses zu verhindern, dass Zugriff auf eine externe Partei über einen Webbrowser werden soll.  

-   **AD FS Extranet Lockout Schutz**  
    
    Bei einem Angriff in Form von authentifizierungsanforderungen mit invalid(bad) Kennwörter, die über das Web Application Proxy stammen, können mit AD FS-extranet-Sperre die Benutzer aus einer AD FS-Kontosperre zu schützen. Zusätzlich zum Schutz von Ihren Benutzern von einem AD FS Kontosperren, AD FS-extranet-Sperre schützt auch Kennwortermittlung brute-Force-Angriffe.  Weitere Informationen finden Sie unter [AD FS Extranet-Sperre Schutz](../../ad-fs/operations/Configure-AD-FS-Extranet-Lockout-Protection.md).  
  
## <a name="sql-serverspecific-security-best-practices-for-ad-fs"></a>SQL Server-spezifische Bewährte Sicherheitsmethoden für AD FS  
Die folgenden bewährten Sicherheitsmethoden sind spezifisch für die Verwendung von Microsoft SQL Server® oder Windows Internal Database (WID), wenn diese Datenbank Technologien zum Verwalten von Daten in AD FS-Entwurf und die Bereitstellung verwendet werden.  
  
> [!NOTE]  
> Diese Empfehlungen sollen erweitern, aber nicht ersetzen, Sicherheitsleitfaden für SQL Server-Produkt. Weitere Informationen zur Planung einer sicheren SQL Server-Installations finden Sie unter [Überlegungen zur Sicherheit für eine sichere SQL-Installation](https://go.microsoft.com/fwlink/?LinkID=139831) (https://go.microsoft.com/fwlink/?LinkID=139831).  
  
-   **Stellen Sie SQL Server immer hinter einer Firewall in einer physisch sicheren Netzwerkumgebung bereit.**  
  
    SQL Server-Installation sollte niemals direkt mit dem Internet verfügbar gemacht werden. Nur Computer, die in Ihrem Rechenzentrum befinden sollten Ihre SQL Server-Installation zu erreichen, die AD FS unterstützt werden. Weitere Informationen finden Sie unter [Prüfliste für bewährte Sicherheitsmethoden](https://go.microsoft.com/fwlink/?LinkID=189229) (https://go.microsoft.com/fwlink/?LinkID=189229).  
  
-   **Führen Sie SQL Server unter einem Dienstkonto anstelle der integrierten Standardsystem-Dienstkonten.**  
  
    Standardmäßig wird SQL Server oft installiert und so konfiguriert, dass eine der unterstützten integrierten Systemkonten, z. B. die Konten "LocalSystem" oder "NetworkService" verwenden. Um die Sicherheit der SQL Server-Installation für AD FS zu verbessern, wo ein separates Dienstkonto für den Zugriff auf Ihre SQL Server-Dienst verwenden und Kerberos-Authentifizierung aktivieren, indem Sie den Sicherheitsprinzipalnamen (SPN) für dieses Konto in Active Directory-Bereitstellung registrieren. Dies ermöglicht die gegenseitigen Authentifizierung zwischen Client und Server. Ohne SPN-Registrierung eines separaten Dienstkontos verwendet SQL Server NTLM für die Windows-basierte Authentifizierung, in denen nur der Client authentifiziert wird.  
  
-   **Minimieren Sie die Oberfläche von SQL Server.**  
  
    Aktivieren Sie nur für diese SQL Server-Endpunkte, die erforderlich sind. Standardmäßig stellt SQL Server einen einzigen integrierten TCP-Endpunkt, der nicht entfernt werden kann. Für AD FS sollten Sie diesen TCP-Endpunkt für die Kerberos-Authentifizierung aktivieren. Zum Überprüfen der aktuellen TCP-Endpunkte, um festzustellen, ob zusätzliche benutzerdefinierte TCP-Ports zu einer SQL-Installation hinzugefügt werden, können Sie die "Wählen Sie * FROM SYS. tcp_endpoints" Abfrage in einer Sitzung (T-SQL) Transact-SQL-Anweisung. Weitere Informationen zu SQL Server-Endpunktkonfiguration finden Sie unter [so wird's gemacht: Konfigurieren der Datenbankmoduls zum Überwachen mehrerer TCP-Ports](https://go.microsoft.com/fwlink/?LinkID=189231) (https://go.microsoft.com/fwlink/?LinkID=189231).  
  
-   **Verwenden Sie keine SQL-basierten Authentifizierung.**  
  
    Um zu vermeiden, dass Kennwörter als Klartext über das Netzwerk übertragen oder Speichern von Kennwörtern in Konfigurationseinstellungen, Windows-Authentifizierung nur mit der SQL Server-Installation verwenden. SQL Server-Authentifizierung ist ein legacyauthentifizierungsmodus. Speichern von Structured Query Language (SQL)-Anmeldeinformationen (SQL-Benutzernamen und Kennwörter) bei Verwendung der SQL Server-Authentifizierung nicht empfohlen. Weitere Informationen finden Sie unter [Authentifizierungsmodi](https://go.microsoft.com/fwlink/?LinkID=189232) (https://go.microsoft.com/fwlink/?LinkID=189232).  
  
-   **Bewerten Sie sorgfältig Weitere Channel-Sicherheit in Ihrer SQL-Installation.**  
  
    Selbst mit Kerberos-Authentifizierung bietet die SQL Server Security Support Provider-Schnittstelle (SSPI) im Grunde keine Sicherheit auf. Jedoch kann für Installationen, die in denen Server sicher auf eine Firewall geschützten Netzwerk befinden, Verschlüsselung der SQL-Kommunikation nicht erforderlich.  
  
    Zwar Verschlüsselung ein wertvolles Tool zur Sicherheit zu gewährleisten, sollten sie nicht für alle Daten oder Verbindungen betrachtet werden. Berücksichtigen Sie, ob zum Implementieren der Verschlüsselung entscheiden, wie Benutzer auf Daten zugreifen. Wenn Benutzer über ein öffentliches Netzwerk auf Daten zugreifen, kann datenverschlüsselung erforderlich sein, um die Sicherheit zu erhöhen. Jedoch, wenn alle Zugriff auf SQL-Daten von AD FS eine sichere Intranetkonfiguration beinhaltet, möglicherweise Verschlüsselung nicht erforderlich sein. Die Verwendung von Verschlüsselung sollte auch eine Wartungsstrategie für Kennwörter, Schlüssel und Zertifikate enthalten.  
  
    Liegt ein Problem, dass die SQL-Daten angezeigt werden oder über das Netzwerk manipuliert werden können, verwenden Sie Internet Protocol Security (IPsec) oder Secure Sockets Layer (SSL) zum Schutz Ihrer SQL-Verbindungen. Jedoch möglicherweise Dies beeinträchtigt die Leistung von SQL Server, die beeinträchtigen oder AD FS-Leistung in einigen Situationen einschränken. Beispielsweise kann AD FS-Leistung bei der tokenausstellung verschlechtert, wenn Sie das Abrufen von Attributen aus einem SQL-basierten Attributspeicher wichtig für die tokenausstellung sind. Sie können eine SQL-manipulationsbedrohung durch die Verwendung einer umkreissicherheitskonfiguration besser vermeiden. Beispielsweise ist die bessere Lösung für das Sichern der SQL Server-Installation um sicherzustellen, dass rechenzentrumsumgebung für Internet-Benutzer und Computer nur von Benutzern oder Computern in Ihrer Umgebung Datacenter zugegriffen werden bleibt.  
  
    Weitere Informationen finden Sie unter [Verschlüsseln von Verbindungen zu SQL Server](https://go.microsoft.com/fwlink/?LinkID=189234) oder [SQL Server-Verschlüsselung](https://go.microsoft.com/fwlink/?LinkID=189233).  
  
-   **Konfigurieren Sie mithilfe von gespeicherten Prozeduren ausführen alle SQL-basierten Abfragen von AD FS von SQL-gespeicherten Daten sicher entworfenen Zugriff.**  
  
    Um eine bessere Dienst- und datenisolierung bereitzustellen, können Sie gespeicherte Prozeduren für alle Abrufbefehle für Attribut erstellen. Sie können eine Datenbankrolle erstellen, die Sie dann über die Berechtigung zum Ausführen der gespeicherten Prozeduren erteilen. Weisen Sie dieser Datenbankrolle die Dienstidentität des AD FS-Windows-Diensts. Der AD FS-Windows-Dienst sollte nicht in der Lage, eine beliebige andere SQL-Anweisung außer den geeigneten gespeicherten Verfahren auszuführen, die für die Suche Attribut verwendet werden. Sperren Sie den Zugriff auf SQL Server-Datenbank auf diese Weise reduziert das Risiko eines Angriffs Erhöhung von Berechtigungen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
