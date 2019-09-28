---
ms.assetid: 4b844404-36ba-4154-aa5d-237a3dd644be
title: Datendeduplizierung (Übersicht)
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
ms.openlocfilehash: 1050c63d77db66c8e280ea1bea9503390c5d0bae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386298"
---
# <a name="data-deduplication-overview"></a>Datendeduplizierung (Übersicht)

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), 

## <a name="what-is-dedup"></a>Was ist die Datendeduplizierung?

Die Datendeduplizierung (häufig als Deduplizierung bezeichnet) ist ein Feature, mit dem die Auswirkungen redundanter Daten auf Speicherkosten reduziert werden können. Falls aktiviert, optimiert die Datendeduplizierung den freien Speicherplatz auf einem Volume, indem die Daten auf dem Volume durch Suchen nach duplizierten Teilen auf dem Volume untersucht werden. Duplizierte Teile des Datasets des Volumes werden einmal gespeichert und für weitere Einsparungen (optional) komprimiert. Die Datendeduplizierung optimiert Redundanzen, ohne dadurch die Originaltreue oder Integrität von Daten zu gefährden. Weitere Informationen über die Funktionsweise der Datendeduplizierung finden Sie im Abschnitt [Wie funktioniert die Datendeduplizierung?](understand.md#how-does-dedup-work) auf der Seite [Grundlegendes zur Datendeduplizierung](understand.md).

> [!Important]  
> [KB4025334](https://support.microsoft.com/kb/4025334) enthält einen Rollup der Fehlerbehebungen für die Datendeduplizierung, einschließlich wichtiger Korrekturen der Zuverlässigkeit. Wir empfehlen dringend, Sie zu installieren, wenn Sie die Datendeduplizierung mit Windows Server 2016 und Windows Server 2019 verwenden.

## <a name="why-is-dedup-useful"></a>Warum ist die Datendeduplizierung hilfreich?

Die Datendeduplizierung hilft Speicheradministratoren bei der Reduzierung der Kosten, die mit duplizierten Daten in Verbindung stehen. Große Datasets weisen häufig **<u>ein hohes Maß</u>** an Duplizierung auf, wodurch die Kosten für die Speicherung von Daten steigen. Zum Beispiel:

- Auf Dateifreigaben von Benutzern befinden sich möglicherweise viele Kopien von gleichen oder ähnlichen Dateien.
- Virtualisierungsgäste können von VM zu VM fast identisch sein.
- Sicherungsmomentaufnahmen weisen möglicherweise geringe Unterschiede zum Vortag auf.

Die Einsparungen von Speicherplatz, die Sie mit Datendeduplizierung erzielen können, sind abhängig vom Dataset oder der Workload auf dem Volume. Bei Datasets mit hoher Duplizierung kann eine Optimierungsquote von bis zu 95 % bzw. eine um das 20-fache reduzierte Speicherbelegung erreicht werden. In der folgenden Tabelle sind die typischen Einsparungen aufgeführt, die für verschiedene Inhaltstypen durch Deduplizierung erzielt werden können:

| Szenario       | Content                                        | Typische Platzeinsparung |
|----------------|------------------------------------------------|-----------------------|
| Benutzerdokumente | Office-Dokumente, Fotos, Musik, Videos usw.  | 30 - 50 %                |
| Bereitstellungsfreigaben | Softwarebinärdateien, CAB-Dateien, Symboldateien usw. | 70 - 80 %                |
| Virtualisierungsbibliotheken | ISO-Dateien, virtuelle Festplattendateien usw.  | 80 - 95 %                |
| Allgemeine Dateifreigabe | Alle obigen                           | 50 - 60 %                |

## <a id="when-can-dedup-be-used"></a>Wann kann die Datendeduplizierung verwendet werden?  
<table>
    <tbody>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-clustered-gpfs.png" alt="Illustration of file servers" /></td>
            <td style="vertical-align:top">
                <b>univers Elle Dateiserver @ no__t-1<br />
Allgemeine Dateiserver sind Server, die beliebige der folgenden Typen von Freigaben enthalten können: <ul>
                    <li>Teamfreigaben</li>
                    <li>Basisordner von Benutzern</li>
                    <li><a href="https://technet.microsoft.com/library/dn265974.aspx">Arbeitsordner</a></li>
                    <li>Freigaben für die Softwareentwicklung</li>
                </ul>
Allgemeine Dateiserver eignen sich gut für die Datendeduplizierung, weil mehrere Benutzer tendenziell über zahlreiche Kopien oder Versionen derselben Datei verfügen. Freigaben für die Softwareentwicklung profitieren von der Datendeduplizierung, da viele Binärdateien von Build zu Build im Wesentlichen unverändert bleiben. 
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-vdi.png" alt="Illustration of VDI servers" /></td>
            <td style="vertical-align:top">
                <b>virtualisierte Desktop Infrastructure (VDI)-bereit Stellungen @ no__t-1<br />
VDI-Server, wie z. B. <a href="https://technet.microsoft.com/library/cc725560.aspx">Remotedesktopdienste</a>, bieten Organisationen eine schlanke Möglichkeit, Benutzern Desktops zur Verfügung zu stellen. Es gibt viele Gründe für eine Organisation, diese Technologie zu nutzen: <ul>
                    <li><b>Anwendungs Bereitstellung</b>: Sie können Anwendungen im gesamten Unternehmen schnell bereitstellen. Dies ist besonders nützlich bei Anwendungen, die häufig aktualisiert werden, selten verwendet werden oder schwierig zu verwalten sind.</li>
                    <li><b>Anwendungs Konsolidierung</b>: Wenn Sie Anwendungen aus einem Satz von zentral verwalteten virtuellen Computern installieren und ausführen, entfällt die Notwendigkeit, Anwendungen auf Client Computern zu aktualisieren. Dadurch verringert sich zudem die Netzwerkbandbreite, die für den Zugriff auf Anwendungen erforderlich ist.</li>
                    <li><b>Remote Zugriff</b>: Benutzer können auf Unternehmensanwendungen von Geräten wie Heimcomputern, Kiosken, niedriger Hardware und Betriebssystemen außer Windows zugreifen.</li>
                    <li><b>Zugriff auf Zweig</b>stellen: VDI-bereit Stellungen können eine bessere Anwendungsleistung für Zweigstellen bereitstellen, die Zugriff auf zentralisierte Datenspeicher benötigen. Datenintensive Anwendungen haben mitunter keine Client/Server-Protokolle, die für langsame Verbindungen optimiert sind.</li>
                </ul>
VDI-Bereitstellungen eignen sich gut für die Datendeduplizierung, da die virtuellen Festplatten auf den Remotedesktops der Benutzer im Wesentlichen identisch sind. Darüber hinaus kann die Datendeduplizierung einen Beitrag gegen die <em>VDI-Startverzögerung</em> leisten, was den Abfall der Speicherleistung bezeichnet, wenn sich viele Benutzer gleichzeitig am Morgen an ihren Desktop-PCs anmelden.
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-backup.png" alt="Illustration of backup applications" /></td>
            <td style="vertical-align:top">
                <b>backup-Ziele, z. b. virtualisierte Sicherungs Anwendungen @ no__t-1<br />
Sicherungsprogramme, wie z.B. <a href="https://technet.microsoft.com/library/hh758173.aspx">Microsoft Data Protection Manager (DPM)</a>, eignen sich aufgrund der erheblichen Duplizierung zwischen Sicherungsmomentaufnahmen besonders gut für Datendeduplizierung.
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-other.png" alt="Illustration of other workloads" /></td>
            <td style="vertical-align:top">
                <b>andere Workloads @ no__t-1<br />
                <a href="install-enable.md#enable-dedup-candidate-workloads" data-raw-source="[Other workloads may also be excellent candidates for Data Deduplication](install-enable.md#enable-dedup-candidate-workloads)">Andere Workloads eignen sich möglicherweise auch hervorragend für die Datendeduplizierung</a>.
            </td>
        </tr>
    </tbody>
</table>
