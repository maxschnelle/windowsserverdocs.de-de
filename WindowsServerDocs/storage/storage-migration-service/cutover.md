---
title: Funktionsweise von cudever im Speicher Migrationsdienst
description: Zusammenfassung und Details zu den Umfassungs Phasen im Speicher Migrationsdienst
author: t-chrche
ms.author: t-chrche
manager: nedpyle
ms.date: 08/31/2020
ms.topic: article
ms.openlocfilehash: 985fd14b7791d28246b8e9186ca83216df734875
ms.sourcegitcommit: a640c2d7f2d21d7cd10a9be4496e1574e5e955f0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2020
ms.locfileid: "89448926"
---
# <a name="how-cutover-works-in-storage-migration-service"></a>Funktionsweise von cudever im Speicher Migrationsdienst

Bei der Migration handelt es sich um die Migrationsphase, bei der die Netzwerk Identität des Quell Computers auf den Zielcomputer verschoben wird. Nach dem umbrechen enthält der Quellcomputer weiterhin dieselben Dateien wie zuvor, er ist jedoch für Benutzer und apps nicht verfügbar.

## <a name="summary"></a>Zusammenfassung

![Screenshot der ](media/cutover/cutover_configuration.png)
 __cudever-Konfiguration Abbildung 1: Konfiguration des Speicher Migrations Dienstanbieter-Konfigurations__ Elements

Vor dem Start der Umstellung werden die Informationen zur Netzwerkkonfiguration bereitgestellt, die zum Ausschneiden vom Quellcomputer zum Zielcomputer erforderlich sind. Sie können auch einen neuen eindeutigen Namen für den Quellcomputer auswählen oder von Storage Migration Service einen zufälligen Namen erstellen lassen.

Anschließend führt der Speicher Migrationsdienst die folgenden Schritte aus, um den Quellcomputer auf den Zielcomputer zu übernehmen:

1. Wir stellen eine Verbindung mit den Quell-und Ziel Computern her. Die folgenden Firewallregeln sollten für beide bereits in eingehender Richtung aktiviert sein:
    * Datei-und Druckerfreigabe (SMB-in), TCP-Port 445
    * Anmeldedienst (NP-in), TCP-Port 445
    * Windows-Verwaltungsinstrumentation (DCOM-in), TCP-Port 135
    * Windows-Verwaltungsinstrumentation (WMI-in), TCP, beliebiger Port

2. Die Sicherheits Berechtigungen auf dem Zielcomputer werden in Active Directory Domain Services festgelegt, um die Berechtigungen des Quell Computers zu erfüllen.

3. Auf dem Quellcomputer wird ein temporäres lokales Benutzerkonto erstellt. Wenn der Computer einer Domäne beigetreten ist, lautet der Benutzername "MsftSmsStorMigratSvc". Wir deaktivieren die [Filter Richtlinie für das lokale Konto Token](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows) auf dem Quellcomputer, um das Konto zuzulassen, und stellen dann eine Verbindung mit dem Quellcomputer her. Wir legen dieses temporäre Konto fest, damit wir, wenn wir den Quellcomputer neu starten und den Quellcomputer später aus der Domäne entfernen, weiterhin auf den Quellcomputer zugreifen können.

4. Wir wiederholen den vorherigen Schritt auf dem Zielcomputer.

5. Der Quellcomputer wird aus der Domäne entfernt, um sein Active Directory Konto freizugeben, das der Zielcomputer später übernimmt.

6. Wir ordnen Netzwerkschnittstellen auf dem Quellcomputer zu und benennen den Quellcomputer um.

7. Der Quellcomputer wird wieder der Domäne hinzugefügt. Der Quellcomputer verfügt nun über eine neue Identität und ist für Administratoren verfügbar, aber nicht für Benutzer und apps.

8. Auf dem Quellcomputer entfernen wir alle veralteten Alternativen Computernamen, entfernen das temporäre lokale Konto, das wir erstellt haben, und aktivieren die Filter Richtlinie für das lokale Konto Token erneut.

9. Der Zielcomputer wird aus der Domäne entfernt.

10. Wir ersetzen die IP-Adressen auf dem Zielcomputer durch die IP-Informationen, die von der Quelle bereitgestellt werden, und benennen den Zielcomputer dann in den ursprünglichen Namen des Quell Computers um.

11. Der Zielcomputer wird wieder zur Domäne hinzugefügt. Wenn Sie verknüpft ist, wird das ursprüngliche Active Directory Computer Konto des Quell Computers verwendet. Hierdurch werden Gruppenmitgliedschaften und Sicherheits-ACLs beibehalten. Der Zielcomputer verfügt jetzt über die Identität des Quell Computers.

12. Auf dem Zielcomputer entfernen Sie alle anderen alternativen Computernamen, entfernen das temporäre lokale Konto, das wir erstellt haben, und aktivieren die Richtlinie für das lokale Konto tokenfilter erneut.

Nachdem die Umstellung abgeschlossen ist, hat der Zielcomputer die Identität des Quell Computers übernommen, und Sie können dann den Quellcomputer außer Betrieb setzen.

## <a name="detailed-stages"></a>Ausführliche Phasen

![](media/cutover/cutover_stage_description.png)
__Abbildung der cudever-Phase: Screenshot Abbildung 2: Storage Migration Service zeigt eine umrandungsphase__ an

Sie können den Verlauf des Verlaufs durch Beschreibungen der einzelnen Phasen nachverfolgen, die in der obigen Abbildung angezeigt werden. In der folgenden Tabelle sind die einzelnen möglichen Phasen sowie der Fortschritt, die Beschreibung und die Anmerkungen zur Verdeutlichung aufgeführt.

|  Fortschritt | Beschreibung                                                                                               |  Hinweise |
|:-----|:--------------------------------------------------------------------------------------------------------------------|:---|
|  0 % | Der cuum befindet sich im Leerlauf. |   |
| 2 %  | Verbindung mit dem Quellcomputer wird hergestellt... |   Stellen Sie sicher, dass die [Anforderungen für den Quell-und den Zielcomputer](https://docs.microsoft.com/windows-server/storage/storage-migration-service/overview#security-requirements-the-storage-migration-service-proxy-service-and-firewall-ports) erfüllt sind.|
| 5 %  | Verbindung mit dem Zielcomputer wird hergestellt... |   |
| 6 %  | Sicherheits Berechtigungen für das Computer Objekt in Active Directory werden festgelegt... |   Repliziert die Active Directory Objekt-Sicherheits Berechtigungen des Quell Computers auf dem Zielcomputer.|
| 8 %  | Es wird sichergestellt, dass das von uns erstellte temporäre Konto erfolgreich auf dem Quellcomputer gelöscht wurde... |   Stellt sicher, dass ein temporäres Konto mit dem gleichen Namen erstellt werden kann.|
| 11 % | Auf dem Quellcomputer wird ein temporäres lokales Benutzerkonto erstellt... |   Wenn der Quellcomputer einer Domäne beigetreten ist, lautet der Benutzername des temporären Kontos "MsftSmsStorMigratSvc". Das Kennwort besteht aus 127 zufälligen Unicode-breit Zeichen mit Buchstaben, Ziffern, Symbolen und Fall Änderungen. Wenn sich der Quellcomputer in einer Arbeitsgruppe befindet, werden die ursprünglichen Quell Anmelde Informationen verwendet.|
| 13 % | Die Filter Richtlinie für das lokale Konto Token wird auf dem Quellcomputer festgelegt... |   Deaktiviert die Richtlinie, sodass eine Verbindung mit der Quelle hergestellt werden kann, wenn Sie nicht der Domäne beigetreten ist. Weitere Informationen zur Richtlinie für das lokale Konto Token [finden Sie hier](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows).|
| 16 % | Verbindung mit dem Quellcomputer wird mithilfe des temporären lokalen Benutzerkontos hergestellt... |   |
| 19 % | Es wird sichergestellt, dass das von uns erstellte temporäre Konto auf dem Zielcomputer erfolgreich gelöscht wurde... |   |
| 22 % | Ein temporäres lokales Benutzerkonto auf dem Zielcomputer wird erstellt... | Wenn der Zielcomputer einer Domäne beigetreten ist, lautet der Benutzername des temporären Kontos "MsftSmsStorMigratSvc". Das Kennwort besteht aus 127 zufälligen Unicode-breit Zeichen mit Buchstaben, Ziffern, Symbolen und Fall Änderungen. Wenn sich der Zielcomputer in einer Arbeitsgruppe befindet, werden die ursprünglichen Ziel Anmelde Informationen verwendet. |
| 25% | Die Filter Richtlinie für das lokale Konto Token wird auf dem Zielcomputer festgelegt... | Deaktiviert die Richtlinie, sodass eine Verbindung mit dem Ziel hergestellt werden kann, wenn es nicht mit der Domäne verknüpft ist. Weitere Informationen zur Richtlinie für das lokale Konto Token [finden Sie hier](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows).   |
| 27 % | Verbindung mit dem Zielcomputer wird mithilfe des temporären lokalen Benutzerkontos hergestellt... |   |
| 30 % | Der Quellcomputer wird aus der Domäne entfernt... |   |
| 31,5 | Die IP-Adressen des Quell Computers werden gesammelt. |   Gilt nur für Linux-Quellcomputer. |
| 33 % | Der Quellcomputer wird neu gestartet... (1. Neustart) |   |
| 36% | Es wird darauf gewartet, dass der Quellcomputer nach dem ersten Neustart antwortet... |   Sie werden wahrscheinlich nicht mehr reagiert, wenn der Quellcomputer nicht von einem DHCP-Subnetz abgedeckt ist, Sie aber während der Netzwerkkonfiguration DHCP ausgewählt haben.|
| 38 % | Netzwerkschnittstellen auf dem Quellcomputer werden Zuordnung... |   |
| 41 % | Der Quellcomputer wird umbenannt... |   |
| 42% | Der Quellcomputer wird neu gestartet... (1. Neustart) |   Gilt nur für Linux-Quellcomputer.|
| 43% | Der Quellcomputer wird neu gestartet... (2. Neustart) |   Gilt nur für in die Domäne eingebundenen Windows Server 2003-Quell Computern.|
| 43% | Es wird darauf gewartet, dass der Quellcomputer nach dem ersten Neustart antwortet... |   |
| 43% | Es wird darauf gewartet, dass der Quellcomputer nach dem zweiten Neustart antwortet... |   |
| 44 % | Der Quellcomputer wird der Domäne hinzugefügt... |   |
| 47 % | Der Quellcomputer wird neu gestartet... (1. Neustart) |   |
| 50% | Der Quellcomputer wird neu gestartet... (2. Neustart) |   |
| 51 % | Der Quellcomputer wird neu gestartet... (3. Neustart) |   Gilt nur für Windows Server 2003-Quellcomputer.|
| 52 % | Es wird auf die Antwort des Quell Computers gewartet... |   |
| 52 % | Es wird darauf gewartet, dass der Quellcomputer nach dem ersten Neustart antwortet... |   |
| 55 % | Es wird darauf gewartet, dass der Quellcomputer nach dem zweiten Neustart antwortet... |   |
| 56 % | Es wird darauf gewartet, dass der Quellcomputer nach dem dritten Neustart antwortet... |   |
| 57% | Alternative Computernamen werden auf der Quelle entfernt... |   Stellt sicher, dass die Quelle für andere Benutzer und apps nicht erreichbar ist. Weitere Informationen finden Sie unter [netdom computername](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc835082(v=ws.11)). |
| 58% | Ein temporäres lokales Konto, das auf dem Quellcomputer erstellt wurde, wird entfernt... |   |
| 61 % | Die Richtlinie zum Zurücksetzen des lokalen Kontos auf dem Quellcomputer wird zurückgesetzt... |   Aktiviert die Richtlinie.|
| 63% | Der Zielcomputer wird aus der Domäne entfernt... |   |
| 66 % | Der Zielcomputer wird neu gestartet... (1. Neustart) |   |
| 69% | Es wird darauf gewartet, dass der Zielcomputer nach dem ersten Neustart antwortet... |   |
| 72% | Netzwerkschnittstellen auf Zielcomputer werden Zuordnung... |  Ordnet jeden Netzwerkadapter und jede IP-Adresse vom Quellcomputer dem Zielcomputer zu und ersetzt dabei die Netzwerkinformationen des Ziels.   |
| 75% | Der Zielcomputer wird umbenannt... |   |
| 77 % | Der Zielcomputer wird der Domäne hinzugefügt... |  Der Zielcomputer übernimmt das Active Directory Objekt des alten Quell Computers. Dies kann fehlschlagen, wenn der Ziel Benutzer kein Mitglied der Gruppe "Domänen-Admins" ist oder nicht über Administratorrechte für den Quellcomputer Active Directory Objekt verfügt. Sie können alternative Ziel Anmelde Informationen im Schritt "Anmelde Informationen eingeben" angeben, bevor der cuum gestartet wird.|
| 80 % | Der Zielcomputer wird neu gestartet... (1. Neustart) |   |
| 83 % | Der Zielcomputer wird neu gestartet... (2. Neustart) |   |
| 84% | Es wird auf die Antwort des Ziel Computers gewartet... |   |
| 86% | Es wird darauf gewartet, dass der Zielcomputer nach dem ersten Neustart antwortet... |   |
| 88% | Es wird darauf gewartet, dass der Zielcomputer nach dem zweiten Neustart antwortet... |   |
| 91% | Es wird darauf gewartet, dass der Zielcomputer mit dem neuen Namen antwortet... |  Kann aufgrund Active Directory und der DNS-Replikation viel Zeit in Anspruch nehmen. |
| 93% | Alternative Computernamen auf dem Ziel werden entfernt... |   Stellt sicher, dass der Zielname ersetzt wurde.|
| 94 % | Ein temporäres lokales Konto, das auf dem Zielcomputer erstellt wurde, wird entfernt...|   |
| 97% | Die Richtlinie zum Zurücksetzen des lokalen Kontos auf dem Zielcomputer wird zurückgesetzt... |   Aktiviert die Richtlinie.|
| (100%) | Erfolgreich |   |

## <a name="faq"></a>FAQ

### <a name="__is-domain-controller-migration-supported__"></a>__Wird die Migration des Domänen Controllers unterstützt?__

Derzeit nicht, aber eine Problem Umgehung finden Sie auf der [FAQ-Seite](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq#is-domain-controller-migration-supported) .


## <a name="known-issues"></a>Bekannte Probleme
>Stellen Sie sicher, dass Sie die Anforderungen der [Übersicht über den Speicher Migrationsdienst](overview.md) erfüllt und das neueste Windows-Update auf dem Computer installiert haben, auf dem Storage Migration Service ausgeführt wird.

Weitere Informationen zu den folgenden Problemen finden Sie auf der [Seite bekannte Probleme](https://docs.microsoft.com/windows-server/storage/storage-migration-service/known-issues) .
* [__Die Überprüfung des Speicher Migrationsdienst-cutovers schlägt mit dem Fehler "Zugriff wird für die tokenfilterrichtlinie auf dem Zielcomputer verweigert" fehl__](https://docs.microsoft.com/windows-server/storage/storage-migration-service/known-issues#storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer)

* [__Fehler "Fehler beim CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO für die NetName-Ressource", und der Windows Server 2008 R2-Cluster-cudever schlägt fehl__](https://docs.microsoft.com/windows-server/storage/storage-migration-service/known-issues#error-clusctl_resource_netname_repair_vco-failed-against-netname-resource-and-windows-server-2008-r2-cluster-cutover-fails)

* [__Die Umstellung hängt von "38% Mapping Network Interfaces on the Source Computer..." ab. bei Verwendung statischer IPS__](https://docs.microsoft.com/windows-server/storage/storage-migration-service/known-issues#cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer-when-using-static-ips)

* [__Die Umstellung hängt von "38% Mapping Network Interfaces on the Source Computer..." ab.__](https://docs.microsoft.com/windows-server/storage/storage-migration-service/known-issues#cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer)

## <a name="additional-references"></a>Weitere Verweise

- [Übersicht über den Speicher Migrationsdienst](overview.md)
- [Migrieren eines Dateiservers mithilfe von Storage Migration Service](migrate-data.md)
- [Häufig gestellte Fragen (FAQ) zu Storage Migration Services](faq.md)
- [Bekannte Probleme bei Storage Migration Service](known-issues.md)
