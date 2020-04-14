---
title: Slmgr.vbs-Optionen zum Abrufen von Informationen zur Volumenaktivierung
description: Listet die verfügbaren Optionen für das Skript „Slmg.vbs“ auf und beschreibt ihre Verwendung
ms.date: 09/24/2019
ms.technology: server-general
ms.topic: article
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
appliesto:
- Windows Server 2012 R2
- Windows 10
- Windows 8.1
ms.openlocfilehash: e3e4b4d236672ce310c8a0eb038d0e19f936a5d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826343"
---
# <a name="slmgrvbs-options-for-obtaining-volume-activation-information"></a>Slmgr.vbs-Optionen zum Abrufen von Informationen zur Volumenaktivierung

Im Folgenden wird die Syntax des Skripts Slmgr.vbs beschrieben. In den Tabellen in diesem Artikel finden Sie Beschreibungen der einzelnen Befehlszeilenoptionen.

```cmd
slmgr.vbs [<ComputerName> [<User> <Password>]] [<Options>]
```

> [!NOTE]
> In diesem Artikel sind optionale Argumente in eckigen Klammern \[] und Platzhalter in spitzen Klammern \<> eingeschlossen. Lassen Sie bei der Eingabe dieser Anweisungen die Klammern fort, und ersetzen Sie die Platzhalter durch entsprechende Werte.

> [!NOTE]
> Informationen über andere Softwareprodukte, die Volumenaktivierung verwenden, finden Sie in der spezifischen Dokumentation der betreffenden Anwendungen.

## <a name="using-slmgr-on-remote-computers"></a>Verwenden von „Slmgr“ auf Remotecomputern

Verwenden Sie zum Verwalten von Remoteclients das Tool für die Volumenaktivierungsverwaltung (Volume Activation Management Tool, VAMT) Version 1.2 oder höher, oder erstellen Sie benutzerdefinierte WMI-Skripts, die die Unterschiede zwischen den Plattformen berücksichtigen. Weitere Informationen zu WMI-Eigenschaften und -Methoden für die Volumenaktivierung finden Sie unter [WMI-Eigenschaften und -Methoden für die Volumenaktivierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502536(v=ws.11)).

> [!IMPORTANT]
> Aufgrund von WMI-Änderungen in Windows 7 und Windows Server 2008 R2 kann das Skript „Slmgr.vbs“ nicht plattformübergreifend eingesetzt werden. Die Verwendung von „Slmgr.vbs“ zum Verwalten eines Windows 7- oder Windows Server 2008 R2-Systems vom Windows Vista&reg;-Betriebssystem aus wird nicht unterstützt. Der Versuch, ein älteres System aus Windows 7 oder Windows Server 2008 R2 zu verwalten, führt zu einem spezifischen Fehler wegen nicht übereinstimmender Versionen. Beispielsweise wird beim Ausführen von **cscript slmgr.vbs \<Name\_des\_Vista-Computers\> /dlv** die folgende Ausgabe erzeugt:
>  
>> Microsoft (R) Windows Script Host Version 5.8 Copyright (C) Microsoft Corporation. Alle Rechte vorbehalten.
>>  
>> Diese Version von „SLMgr.vbs“ wird vom Remotecomputer nicht unterstützt.

## <a name="general-slmgrvbs-options"></a>Allgemeine Slmgr.vbs-Optionen

|Option |Beschreibung |
| - | - |
|\[\<Computername\>] |Name des Remotecomputers (Standardwert ist lokaler Computer) |
|\[\<Benutzer\>] |Konto mit den erforderlichen Berechtigungen für den Remotecomputer |
|\[\<Kennwort\>] |Kennwort für das Konto mit den erforderlichen Berechtigungen für den Remotecomputer |

## <a name="global-options"></a>Globale Optionen

|Option |Beschreibung |
| - | - |
|\/ipk&nbsp;&lt;ProductKey&gt; |Versucht, einen 5x5-Product Key zu installieren. Der von diesem Parameter bereitgestellte Schlüssel wird als gültig bestätigt und ist für das installierte Betriebssystem geeignet.<br />Andernfalls wird ein Fehler zurückgegeben.<br />Wenn der Schlüssel gültig und anwendbar ist, wird er installiert. Wenn ein Schlüssel bereits installiert ist, wird dieser automatisch ersetzt.<br />Zur Vermeidung von Problemen mit der Stabilität des Lizenzdienstes sollten das System oder der Softwareschutzdienst neu gestartet werden.<br />Dieser Vorgang muss in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden, oder der Registrierungswert „Standardbenutzervorgänge“ muss so festgelegt sein, dass auch Benutzer ohne die entsprechenden Berechtigungen auf den Softwareschutzdienst zugreifen können. |
|/ato&nbsp;\[\<Aktivierungs-&nbsp;ID\>] |Bei Verkaufsversionen und Volumensystemen mit installiertem KMS-Hostschlüssel oder Mehrfachaktivierungsschlüssel (Multiple Activation Key, MAK), fordert **/ato** Windows zur Onlineaktivierung auf.<br />Bei Systemen mit einem installierten generischen Volumenlizenzschlüssel (Generic Volume License Key, GVLK) wird hiermit zur KMS-Aktivierung aufgefordert. Systeme mit einer fehlenden automatischen KMS-Aktivierung ( **/stao**) werden dennoch versuchen, eine KMS-Aktivierung durchzuführen, wenn **/ato** ausgeführt wird.<br />**Hinweis:** Ab Windows 8 (und Windows Server 2012) ist die Option **/stao** veraltet. Verwenden Sie stattdessen die Option **/act-type**.<br />Mit dem Parameter \<**Aktivierungs-ID**\> wird die **/ato**-Unterstützung auf die Erkennung einer auf dem Computer installierten Windows-Edition erweitert. Bei Angabe des Parameters \<**Aktivierungs-ID**\> werden die Ergebnisse der Option auf die mit dieser Aktivierungs-ID verknüpfte Edition beschränkt. Führen Sie **slmgr.vbs /dlv all** aus, um die Aktivierungs-IDs für die installierte Windows-Version abzurufen. Wenn Sie Unterstützung für weitere Anwendungen benötigen, finden Sie weitere Anweisungen in den Handbüchern zur jeweiligen Anwendung.<br />Für die KMS-Aktivierung sind keine erhöhten Rechte erforderlich. Für die Onlineaktivierung werden jedoch erhöhte Rechte benötigt, oder der Registrierungswert Standardbenutzervorgänge muss so festgelegt sein, dass auch Benutzer ohne die entsprechenden Berechtigungen auf den Softwareschutzdienst zugreifen können. |
|\/dli&nbsp;\[<Aktivierungs-&nbsp;ID\>&nbsp;\|&nbsp;All\] |Anzeigen von Lizenzinformationen.<br />Standardmäßig werden mit **/dli** die Lizenzinformationen der installierten, aktiven Windows-Edition angezeigt. Bei Angabe des Parameters \<**Aktivierungs-ID**\> werden die Lizenzinformationen der angegebenen Edition, die mit dieser Aktivierungs-ID verbunden ist, angezeigt. Bei Angabe von **All** als Parameter werden die Lizenzinformationen aller betroffenen installierten Produkte angezeigt.<br />Für diesen Vorgang sind keine erhöhten Rechte erforderlich. |
|\/dlv&nbsp;\[<Aktivierungs-&nbsp;ID\>&nbsp;\|&nbsp;All\] |Anzeigen von detaillierten Lizenzinformationen.<br />Standardmäßig werden mit **/dlv** die Lizenzinformationen des installierten Betriebssystems angezeigt. Bei Angabe des Parameters \<**Aktivierungs-ID**\> werden die Lizenzinformationen der angegebenen Edition, die mit dieser Aktivierungs-ID verbunden ist, angezeigt. Bei Angabe des Parameters **All** werden die Lizenzinformationen aller betroffenen installierten Produkte angezeigt.<br />Für diesen Vorgang sind keine erhöhten Rechte erforderlich. |
|\/xpr \[\<Aktivierungs-&nbsp;ID\>] |Zeigt das Ablaufdatum der Aktivierung des Produkts an. Dies bezieht sich standardmäßig auf die aktuelle Windows-Edition und wird in erster Linie für KMS-Clients genutzt, da die MAK-Aktivierung und die Aktivierung von Verkaufsversionen unbefristet sind.<br />Bei Angabe des Parameters \<**Aktivierungs-ID**\> wird das Aktivierungsablaufdatum der angegebenen Edition angezeigt, die mit dieser Aktivierungs-ID verbunden ist. Für diesen Vorgang sind keine erhöhten Rechte erforderlich. |

## <a name="advanced-options"></a>Erweiterte Optionen

|Option |Beschreibung |
| - | - |
|\/cpky |Einige Wartungsoptionen setzen voraus, dass der Product Key bei Vorgängen der Windows-Willkommensseite (OOBE) in der Registrierung vorhanden ist. Mit der Option **/cpky** wird der Product Key aus der Registrierung entfernt, damit dieser nicht durch schädlichen Code gestohlen werden kann.<br />Bei Installationen von Verkaufsversionen, bei denen Schlüssel bereitgestellt werden, stellt das Ausführen dieser Option eine bewährte Methode dar. Diese Option ist für MAK- und KMS-Hostschlüssel nicht erforderlich, da dies das Standardverhalten für diese Schlüssel ist. Diese Option wird lediglich für andere Schlüsseltypen benötigt, bei denen der Schlüssel nicht standardmäßig aus der Registrierung gelöscht wird.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/ilc&nbsp;&lt;Lizenzdatei&gt; |Mit dieser Option wird die Lizenzdatei installiert, die mit dem obligatorischen Parameter angegeben wird. Diese Lizenzen können als Problembehebungsmaßnahme, zur Unterstützung tokenbasierter Aktivierung, oder als Teil der manuellen Installation einer bereits integrierten Anwendung installiert werden.<br />Lizenzen werden im Verlauf dieses Prozesses nicht überprüft: Lizenzüberprüfung gehört nicht zum Leistungsumfang von Slmgr.vbs. Stattdessen wird diese Überprüfung zur Laufzeit vom Softwareschutzdienst durchgeführt.<br />Dieser Vorgang muss in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden, oder der Registrierungswert **Standardbenutzervorgänge** muss so festgelegt sein, dass auch Benutzer ohne die entsprechenden Berechtigungen auf den Softwareschutzdienst zugreifen können. |
|\/rilc |Mit dieser Option werden alle unter %SystemRoot%\system32\oem und %SystemRoot%\System32\spp\tokens gespeicherten Lizenzen erneut installiert. Hierbei handelt es sich um „als funktionierend bekannte“ Kopien, die bei der Installation gespeichert wurden.<br />Alle übereinstimmenden Lizenzen im vertrauenswürdigen Speicher werden ersetzt. Alle weiteren Lizenzen &mdash; z.B. Veröffentlichungslizenzen von vertrauenswürdigen Stellen (Trusted Authority Issuance Licenses, TA ILs), Lizenzen für Anwendungen &mdash; bleiben hiervon unberührt.<br />Dieser Vorgang muss in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden, oder der Registrierungswert **Standardbenutzervorgänge** muss so festgelegt sein, dass auch Benutzer ohne die entsprechenden Berechtigungen auf den Softwareschutzdienst zugreifen können. |
|\/rearm |Mit dieser Option werden die Aktivierungszähler zurückgesetzt. Der Prozess **/rearm** wird auch von **sysprep /generalize** aufgerufen.<br />Dieser Vorgang bewirkt nichts, wenn der Registrierungseingrag **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform\SkipRearm** auf **1** festgelegt wurde. Weitere Informationen zu diesem Registrierungseintrag finden Sie unter [Registrierungseinstellungen für die Volumenaktivierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502532(v=ws.11)).<br />Dieser Vorgang muss in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden, oder der Registrierungswert **Standardbenutzervorgänge** muss so festgelegt sein, dass auch Benutzer ohne die entsprechenden Berechtigungen auf den Softwareschutzdienst zugreifen können. |
|\/rearm-app &lt;Anwendungs-&nbsp;ID&gt; |Setzt den Lizenzierungsstatus der angegebenen App zurück. |
|\/rearm-sku &lt;Anwendungs&nbsp;ID&gt; |Setzt den Lizenzierungsstatus der angegebenen SKU zurück. |
|\/upk&nbsp;\[&lt;Anwendungs-&nbsp;ID&gt;] |Mit dieser Option wird der Product Key der aktuellen Windows-Edition deinstalliert. Nach dem Neustart weist das System den Status „Nicht lizenziert“ auf, bis ein neuer Product Key installiert wurde.<br />Optional können Sie mit dem Parameter \<**Aktivierungs-ID**\> ein anderes installiertes Produkt angeben.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/dti&nbsp;\[\<Aktivierungs&nbsp;ID\>] |Mit dieser Option wird die Installations-ID für Offlineaktivierung angezeigt. |
|\/atp &lt;Bestätigungs&nbsp;ID&gt; |Führt eine Produktaktivierung mit vom Benutzer angegebener Bestätigungs-ID durch. |

## <a name="kms-client-options"></a>KMS-Clientoptionen

|Option |Beschreibung |
| - | - |
|\/skms \<Name\[:Port]&nbsp;\|&nbsp;\:&nbsp;Port\> \[\<Aktivierungs&nbsp;-ID\>] |Mit dieser Option wird der Name und optional der Port des zu kontaktierenden KMS-Hostcomputers angegeben. Mit Festlegung dieses Werts wird die automatische Erkennung des KMS-Hosts deaktiviert.<br />Wenn der KMS-Host ausschließlich Internetprotokoll Version 6 (IPv6) verwendet, muss die Adresse im Format \<Hostname\>:\<Port\> angegeben werden. IPv6-Adressen enthalten Doppelpunkte (:), die vom Slmgr.vbs-Skript nicht ordnungsgemäß analysiert werden.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/skms-domain&nbsp;&lt;FQDN&gt; \[\<Aktivierungs&nbsp;-ID\>] |Mit dieser Option wird die DNS-Domäne, in der alle KMS-SRV-Einträge zu finden sind, festgelegt. Diese Einstellung ist nicht wirksam, wenn der KMS-Einzelhost mit der Option **/skms** festgelegt ist. Verwenden Sie diese Option, insbesondere in zusammenhanglosen Namespaceumgebungen, damit KMS die DNS-Suffixsuchliste ignoriert und stattdessen nach KMS-Hosteinträgen in der angegebenen DNS-Domäne sucht. |
|\/ckms&nbsp;\[\<Aktivierungs-&nbsp;ID\>] |Mit dieser Option werden der Name, die Adresse und die Portinformationen des angegebenen KMS-Hosts aus der Registrierung gelöscht, und die Funktion für die automatische KMS-Erkennung wiederhergestellt.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/skhc |Mit dieser Option wird die KMS-Hostzwischenspeicherung aktiviert (Standardwert). Nachdem der Client einen funktionierenden KMS-Host erkannt hat, verhindert diese Einstellung Auswirkungen von DNS-Priorität und -Gewichtung (Domain Name System) auf die weitere Kommunikation mit dem Host. Wenn das System keine Verbindung mit dem funktionierenden KMS-Host mehr herstellen kann, versucht der Client, einen neuen Host zu ermitteln.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/ckhc |Mit dieser Option wird die KMS-Hostzwischenspeicherung deaktiviert. Mit dieser Einstellung wird der Client angewiesen, bei jeder versuchten KMS-Aktivierung eine automatische DNS-Erkennung zu verwenden (empfohlen bei Verwendung von Priorität und Gewichtung).<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |

## <a name="kms-host-configuration-options"></a>Optionen für die KMS-Hostkonfiguration

|Option |Beschreibung |
| - | - |
|\/sai&nbsp;&lt;Intervall&gt; |Mit dieser Option wird für nicht aktivierte Clients das Intervall in Minuten für den Versuch festgelegt, eine Verbindung zu KMS aufzubauen. Das Aktivierungsintervall muss zwischen 15 Minuten und 30 Tagen liegen, es wird jedoch empfohlen, den Standardwert (2 Stunden) zu verwenden.<br />Dieses Intervall wird anfangs vom KMS-Client aus der Registrierung übernommen, nach Empfang der ersten KMS-Antwort wird stattdessen jedoch die KMS-Einstellung verwendet.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/sri &lt;Intervall&gt; |Mit dieser Option wird für aktivierte Clients das Erneuerungsintervall in Minuten für den Versuch festgelegt, eine Verbindung zu KMS aufzubauen. Das Erneuerungsintervall muss zwischen 15 Minuten und 30 Tagen liegen. Diese Option wird anfangs auf dem KMS-Server und -Client festgelegt. Der Standardwert ist 10.080 Minuten (sieben Tage).<br />Dieses Intervall wird anfangs vom KMS-Client aus der Registrierung übernommen, nach Empfang der ersten KMS-Antwort wird stattdessen jedoch die KMS-Einstellung verwendet.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/sprt&nbsp;&lt;Port&gt; |Mit dieser Option wird der Port festgelegt, den der KMS-Host für das Erhalten von Clientaktivierungsanforderungen abfragt. Der standardmäßige TCP-Port ist 1688.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/sdns |Aktiviert die DNS-Veröffentlichung durch den KMS-Host (Standard).<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/cdns |Deaktiviert die DNS-Veröffentlichung durch den KMS-Host.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/spri |Legt die KMS-Priorität auf normal fest (Standard).<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/cpri |Legt die KMS-Priorität auf niedrig fest.<br />Verwenden Sie diese Option, um Konflikte von KMS in einer Umgebung mit mehreren Hosts zu vermeiden. Dies kann die Außerkraftsetzung von KMS bewirken, je nachdem, welche anderen Anwendungen oder Serverrollen aktiv sind. Verwenden Sie diesen Wert mit größter Vorsicht.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/act-type \[\<Aktivierungstyp\>] \[\<Aktivierungs-&nbsp;ID\>] |Mit dieser Option wird der Wert in der Registrierung festgelegt, der die Volumenaktivierung auf einen einzigen Typ begrenzt. Aktivierungstyp **1** begrenzt die Aktivierung auf Active Directory-Aktivierung; **2** begrenzt sie auf KMS-Aktivierung; **3** auf tokenbasierte Aktivierung. **0** lässt alle Aktivierungstypen zu und ist der Standardwert. |

## <a name="token-based-activation-configuration-options"></a>Konfigurationsoptionen für tokenbasierte Aktivierung

|Option |Beschreibung |
| - | - |
|/lil |Führt installierte Veröffentlichungslizenzen für die tokenbasierte Aktivierung auf. |
|\/ril&nbsp;&lt;ILID&gt;&nbsp;&lt;ILvID&gt; |Entfernt eine installierte Veröffentlichungslizenz für die tokenbasierte Aktivierung.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. |
|\/stao |Legt das Kennzeichen **Token-based Activation Only** (Nur tokenbasierte Aktivierung) fest und deaktiviert dadurch die automatische KMS-Aktivierung.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden.<br />Diese Option wurde in Windows Server 2012 R2 und Windows 8.1 entfernt. Verwenden Sie stattdessen die Option **/act–type**. |
|\/ctao |Entfernt das Kennzeichen **Nur tokenbasierte Aktivierung** (Standard) und aktiviert dadurch die automatische KMS-Aktivierung.<br />Dieser Vorgang kann nur in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden.<br />Diese Option wurde in Windows Server 2012 R2 und Windows 8.1 entfernt. Verwenden Sie stattdessen die Option **/act-type**</strong>. |
|\/ltc |Führt gültige Zertifikate für die tokenbasierte Aktivierung auf, mit denen installierte Software aktiviert werden kann. |
|\/fta &lt;Zertifikat&nbsp;fingerabdruck&gt; \[&lt;PIN&gt;] |Erzwingt die tokenbasierte Aktivierung unter Verwendung des identifizierten Zertifikats. Die optionale PIN wird bereitgestellt, damit der private Schlüssel ohne PIN-Eingabeaufforderung entsperrt werden kann, wenn hardwaregeschützte Zertifikate (z. B. Smartcards) verwendet werden. |

## <a name="active-directory-based-activation-configuration-options"></a>Konfigurationsoptionen für Aktivierung über Active Directory

|Option |Beschreibung |
| - | - |
|\/ad-activation-online &lt;Product&nbsp;Key&gt; \[\<Name&nbsp;des&nbsp;Aktivierungsobjekts\>] |Sammelt Active Directory-Daten und startet die Aktivierung der Active Directory-Gesamtstruktur unter Verwendung der von der Eingabeaufforderung ausgeführten Anmeldeinformationen. Es ist kein Zugriff durch einen lokalen Administrator erforderlich. Allerdings wird eine Lese-/Schreibberechtigung für den Aktivierungsobjektcontainer in der Stammdomäne der Gesamtstruktur benötigt. |
|\/ad-activation-get-IID &lt;Product&nbsp;Key&gt; |Mit dieser Option wird die telefonische Aktivierung der Active Directory-Gesamtstruktur gestartet. Es wird die Installations-ID (IID) ausgegeben, mit der die Gesamtstruktur bei fehlender Internetverbindung telefonisch aktiviert werden kann. Nach Eingabe der IID während des Aktivierungsanrufs wird eine CID zurückgegeben, mit der die Aktivierung abgeschlossen wird. |
|\/ad-activation-apply-cid &lt;Product&nbsp;Key&gt; &lt;Bestätigungs&nbsp;-ID&gt; \[\<Name&nbsp;des&nbsp;Aktivierungsobjekts>] |Wenn Sie diese Option verwenden, geben Sie die CID ein, die beim Telefongespräch zur Aktivierung angegeben wurde, um die Aktivierung abzuschließen |
|\[/name: &lt;AO_Name&gt;] |Optional können Sie die Option **/name** bei allen diesen Befehlen einfügen, um den Namen für das in Active Directory gespeicherte Aktivierungsobjekt anzugeben. Der Name darf nicht länger als 40 Unicode-Zeichen sein. Verwenden Sie doppelte Anführungszeichen, um die Namenszeichenfolge explizit zu definieren.<br />In Windows Server 2012 R2 und Windows 8.1 können Sie den Namen direkt hinter **/ad-activation-online &lt;Product&nbsp;Key&gt;** und **/ad-activation-apply-cid** anfügen, ohne die Option **/name** verwenden zu müssen. |
|\/ao-list |Zeigt Aktivierungsobjekte an, die für den lokalen Computer verfügbar sind. |
|\/del-ao &lt;AO_DN&gt;<br />\/del-ao &lt;AO_RDN&gt; |Löscht das angegebene Aktivierungsobjekt aus der Gesamtstruktur. |

## <a name="see-also"></a>Siehe auch

- [Technische Referenz zur Volumenaktivierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502529%28v%3dws.11%29)
- [Volumenaktivierung: Übersicht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831612%28v%3dws.11%29)

