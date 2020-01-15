---
title: „Speicher“.
description: ''
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 03/08/2019
ms.openlocfilehash: 7e7fbd6ce3fcef6b0f8da88927d83f28d3fff0a8
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950228"
---
# <a name="storage"></a>„Speicher“.

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows Server? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />
Der Speicher in Windows Server bietet neue und verbesserte Funktionen für Kunden des softwaredefinierten Rechenzentrums (software-defined datacenter, SDDC), die sich auf virtualisierte Workloads konzentrieren. Windows Server bietet außerdem umfassende Unterstützung für Unternehmenskunden, die Dateiserver mit vorhandenen Workloads verwenden.

<hr />
<ul class="cardsF panelContent">
<li>
 <a href="whats-new-in-storage.md">
                            <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                            <h2>Das ist neu:</h2>
                                            <p>Erfahren Sie mehr über die Neuerungen im Windows Server-Speicher</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
<hr />
<ul class="cardsF panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Softwaredefinierter Speicher für virtualisierte Workloads</h3>
<HR />
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">Direkte Speicherplätze</a></h3> Direkt angefügter lokaler Speicher, einschließlich SATA-und nvme-Geräte, zur Optimierung der Datenträger Verwendung nach dem Hinzufügen neuer physischer Datenträger und für schnellere Wiederherstellungszeiten virtueller Festplatten. Informationen zu freigegebenen SAS und eigenständige Speicherplätze finden Sie unter <a href="storage-spaces/overview.md">Speicherplätze</a> .</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">Speicherreplikat</a></h3> Speicher agnostische, synchrone Replikation auf Blockebene zwischen Clustern oder Servern für Notfallvorsorge und-Wiederherstellung sowie das Strecken eines Failoverclusters Zwischenstand Orten für hohe Verfügbarkeit. Die synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um auf Dateisystemebene sicherzustellen, dass kein Datenverlust auftritt.</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">Speicher Quality of Service (QoS)</a></h3> Zentrale Überwachung und Verwaltung der Speicherleistung für virtuelle Computer mithilfe von Hyper-V und den Dateiserver mit horizontaler Skalierung Rollen, die Speicherressourcen mit dem gleichen Datei Server Cluster automatisch nicht ordnungsgemäß verwenden.</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">Datendeduplizierung</a></h3> Optimiert den freien Speicherplatz auf einem Volume, indem die Daten auf dem Volume für die Duplizierung überprüft werden. Nach ihrer Erkennung werden duplizierte Teile des Datasets des Volumes einmal gespeichert und für weitere Einsparungen (optional) komprimiert. Die Datendeduplizierung optimiert Redundanzen, ohne dadurch die Originaltreue oder Integrität von Daten zu gefährden.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Allgemeine Dateiserver</h3>
<HR />
                        <p><h3><a href="storage-migration-service/overview.md">Speicher Migrationsdienst</a></h3>Migrieren von Servern zu einer neueren Version von Windows Server mithilfe eines grafischen Tools zum Inventarisieren von Daten auf Servern, übertragen der Daten und der Konfiguration auf neuere Server und anschließendes Verschieben der Identitäten der alten Server auf die neuen Server, damit apps und Benutzer Sie müssen nichts ändern.</p>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">Arbeitsordner</a></h3> Speichern und Zugreifen auf Arbeitsdateien auf PCs und Geräten, häufig auch als Bring-your-own-Device (BYOD) bezeichnet, zusätzlich zu den Unternehmens Computern. Benutzer erhalten einen komfortablen Ort, um Arbeitsdateien zu speichern und von beliebigem Ort aus darauf zuzugreifen. Organisationen behalten die Kontrolle über Unternehmensdaten durch Speichern der Dateien auf zentral verwalteten Dateiservern und optionale Festlegung von Benutzerrichtlinien für Geräte (z.B. Verschlüsselung und Sperrbildschirmkennwörter).</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">Offlinedateien und Ordner Umleitung</a></h3> Leiten Sie den Pfad lokaler Ordner (z. b. des Ordners "Dokumente") an einen Netzwerk Speicherort um, während Sie die Inhalte lokal zwischenspeichern, um die Geschwindigkeit und Verfügbarkeit</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">Roaming-Benutzerprofile</a></h3> Umleiten eines Benutzerprofils an eine Netzwerkadresse.</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">DFS-Namespaces</a></h3> Gruppieren Sie freigegebene Ordner, die sich auf unterschiedlichen Servern befinden, in einem oder mehreren logisch strukturierten Namespaces. Jeder Namespace wird Benutzern als einzelner freigegebener Ordner mit einer Reihe von Unterordnern angezeigt. Die zugrunde liegende Struktur des Namespace kann jedoch aus zahlreichen Dateifreigaben bestehen, die sich auf verschiedenen Servern und an mehreren Orten befinden.</p>
<HR />
                        <p><h3><a href="dfs-replication/dfsr-overview.md">DFS-Replikation</a></h3> Replizieren Sie Ordner (einschließlich derjenigen, auf die durch einen DFS-Namespace Pfad verwiesen wird) über mehrere Server und Standorte. Für die DFS-Replikation wird ein Komprimierungsalgorithmus verwendet, der als Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) bezeichnet wird. Mit RDC werden Änderungen an den Daten in einer Datei erkannt. Dadurch ist es möglich, mit der DFS-Replikation anstelle der gesamten Datei lediglich die geänderten Dateiblöcke zu replizieren.</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">Ressourcen-Manager für Dateiserver</a></h3> Verwalten und Klassifizieren von auf Dateiservern gespeicherten Daten.<p>
<HR />
                        <p><h3><a href="iscsi/iscsi-target-server.md">iSCSI-Zielserver</a></h3> Stellt mithilfe des iSCSI-Standards (Internet SCSI) Blockspeicher für andere Server und Anwendungen im Netzwerk zur Verfügung.</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">iSCSI-Zielserver</a></h3> Können Hunderte von Computern von einem einzelnen Betriebssystem Abbild, das an einem zentralen Ort gespeichert ist, gestartet werden. Dies führt zu einer Verbesserung von Effizienz, Verwaltbarkeit, Verfügbarkeit und Sicherheit.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Dateisysteme, Protokolle usw.</h3>
<HR />
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> Ein robustes Dateisystem, das die Datenverfügbarkeit maximiert, effizient für sehr große Datasets in verschiedenen Workloads skaliert und Datenintegrität durch Resilienz gegenüber Beschädigungen (unabhängig von Software-oder Hardwarefehlern) bereitstellt.<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">Server Message Block-Protokoll (SMB)</a></h3> Ein Netzwerkdatei Freigabe Protokoll, das es Anwendungen auf einem Computer ermöglicht, Dateien zu lesen und in Dateien zu schreiben sowie Dienste von Serverprogrammen in einem Computernetzwerk anzufordern. Das SMB-Protokoll kann zusätzlich zu den TCP/IP-Protokollen oder anderen Netzwerkprotokollen verwendet werden. Mit dem SMB-Protokoll kann eine Anwendung (oder der Benutzer einer Anwendung) auf Dateien oder andere Ressourcen auf einem Remoteserver zugreifen. Dadurch wird es Anwendungen ermöglicht, Dateien auf dem Remoteserver zu lesen, zu erstellen und zu aktualisieren. Anwendungen können zudem mit jedem beliebigen Serverprogramm kommunizieren, das für den Empfang einer SMB-Clientanforderung eingerichtet ist.<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">Speicher Klassen Speicher</a></h3> Bietet eine ähnliche Leistung wie der Computer Arbeitsspeicher (sehr schnell), jedoch mit der Daten Persistenz normaler Speicher Laufwerke. Windows behandelt Speicherklassenspeicher ähnlich wie normale Laufwerke (nur schneller), doch es gibt einige Unterschiede in der Verwaltung der Geräteintegrität.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">BitLocker-Laufwerkverschlüsselung</a></h3> Speichert Daten auf Volumes in verschlüsselter Form, auch wenn der Computer manipuliert oder das Betriebssystem nicht ausgeführt wird. Dies bietet Schutz vor „Offline-Angriffen“, bei denen entweder das installierte Betriebssystem deaktiviert oder umgangen oder die Festplatte physisch aus dem Computer entfernt wird, um die Daten separat anzugreifen.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">NTFS</a></h3> Das primäre Dateisystem für neuere Versionen von Windows und Windows Server – bietet einen vollständigen Satz von Features, einschließlich Sicherheits Deskriptoren, Verschlüsselung, Datenträger Kontingente und umfangreiche Metadaten, und kann mit freigegebenen Clustervolumes (CSV) verwendet werden, um kontinuierlich bereitzustellen. Verfügbare Volumes, auf die gleichzeitig von mehreren Knoten eines Failoverclusters aus zugegriffen werden kann.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">Network File System (NFS)</a></h3> Bietet eine Dateifreigabe Lösung für Unternehmen mit heterogenen Umgebungen, die aus Windows-und nicht-Windows-Computern bestehen.<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## <a name="in-azure"></a>In Azure

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure storsimple](https://www.microsoft.com/cloud-platform/azure-storsimple)
