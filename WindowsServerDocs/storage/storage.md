---
title: Speicher
description: ''
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 03/08/2019
ms.openlocfilehash: d83d51ebf56d38f93c176d403ea5c6c14f625ee2
ms.sourcegitcommit: 419bf9d6d18e7a32cba2cbcd98587b81a79adc51
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2019
ms.locfileid: "9152177"
---
# Speicher

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere anderen [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen auf [dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) .

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
                                            <p>Erfahren Sie, was neu in Windows Server-Speicher ist</p>
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
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">Speicherplätze DAS</a></h3> Direkt angeschlossenen lokalen Speicher, einschließlich SATA- und NVME-Geräte, zur Optimierung der Datenträgerverwendung nach dem Hinzufügen neuer physischer Datenträger, und für schneller virtuellen Datenträger Reparaturzeiten. Informationen zu freigegebenen SAS und eigenständige Speicherplätze finden Sie unter <a href="storage-spaces/overview.md">Speicherplätze</a> .</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">Speicherreplikat</a></h3> Speicheragnostische auf Blockebene, synchrone Replikation zwischen Clustern oder Servern für die notfallbereitschaft und Wiederherstellung sowie Strecken eines Failoverclusters über mehrere Standorte für hohe Verfügbarkeit. Die synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um auf Dateisystemebene sicherzustellen, dass kein Datenverlust auftritt.</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">Quality of Service (QoS) für Speicher</a></h3> Zentrale Überwachung und Verwaltung der speicherleistung für virtuelle Computer mit Hyper-V und der Scale-Out-Dateiservers automatisch Improveing-Fairness zwischen mehrere virtuelle Computer, die denselben Dateiservercluster verwenden.</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">Datendeduplizierung</a></h3> Optimiert den freien Speicherplatz auf einem Volume durch die Daten auf dem Volume auf Duplizierung untersucht. Nach ihrer Erkennung werden duplizierte Teile des Datasets des Volumes einmal gespeichert und für weitere Einsparungen (optional) komprimiert. Die Datendeduplizierung optimiert Redundanzen, ohne dadurch die Originaltreue oder Integrität von Daten zu gefährden.</p>
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
                        <p><h3><a href="storage-migration-service/overview.md">Speicherdienst-Migration</a></h3>Migrieren von Servern auf eine neuere Version von Windows Server mit einem Grafiktool, die Daten auf Servern inventarisiert, Daten und Konfiguration auf neuere Server überträgt, und dann optional die Identitäten der alten Server auf die neuen Server daher diese apps und Benutzer nichts ändern müssen.</p>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">Arbeitsordner</a></h3> Arbeiten Dateien auf PCs und Geräte, die so genannte bring-your-own Device (BYOD), neben Firmen-PCs, speichern und darauf zuzugreifen. Benutzer erhalten einen komfortablen Ort, um Arbeitsdateien zu speichern und von beliebigem Ort aus darauf zuzugreifen. Organisationen behalten die Kontrolle über Unternehmensdaten durch Speichern der Dateien auf zentral verwalteten Dateiservern und optionale Festlegung von Benutzerrichtlinien für Geräte (z.B. Verschlüsselung und Sperrbildschirmkennwörter).</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">Offlinedateien und Ordnerumleitung</a></h3> Umzuleiten Sie den Pfad lokaler Ordner (z. B. den Ordner "Dokumente") an eine Netzwerkadresse, den Inhalt für eine höhere Geschwindigkeit und Verfügbarkeit lokal zwischenzuspeichern.</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">Roaming-Benutzerprofile</a></h3> Umleiten Sie ein Benutzerprofil an eine Netzwerkadresse.</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">DFS-Namespaces</a></h3> Gruppieren Sie freigegebene Ordner, die auf verschiedenen Servern, in einen oder mehrere logisch strukturierten Namespaces befinden. Jeder Namespace wird Benutzern als einzelner freigegebener Ordner mit einer Reihe von Unterordnern angezeigt. Die zugrunde liegende Struktur des Namespace kann jedoch aus zahlreichen Dateifreigaben bestehen, die sich auf verschiedenen Servern und an mehreren Orten befinden.</p>
<HR />
                        <p><h3><a href="dfs-replication/dfsr-overview.md">DFS-Replikation</a></h3> Replizieren von Ordnern (einschließlich jenen, auf durch einen DFS-Namespacepfad) über mehrere Server und Websites. Für die DFS-Replikation wird ein Komprimierungsalgorithmus verwendet, der als Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) bezeichnet wird. Mit RDC werden Änderungen an den Daten in einer Datei erkannt. Dadurch ist es möglich, mit der DFS-Replikation anstelle der gesamten Datei lediglich die geänderten Dateiblöcke zu replizieren.</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">Ressourcen-Manager für Dateiserver</a></h3> Verwalten und Klassifizieren von auf Dateiservern gespeicherten Daten.<p>
<HR />
                        <p><h3><a href="iscsi/iscsi-target-server.md">iSCSI Target Server</a></h3> Bietet Blockspeicher für andere Server und Anwendungen im Netzwerk mithilfe des Standards Internet SCSI (iSCSI).</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">iSCSI Target Server</a></h3> Können Sie Hunderte von Computern aus einem einzelnen Betriebssystemimage starten, die an einem zentralen Ort gespeichert ist. Dies führt zu einer Verbesserung von Effizienz, Verwaltbarkeit, Verfügbarkeit und Sicherheit.</p>
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
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> Ein robustes Dateisystem, das maximiert, effizient, sehr große Datasets über diverse Arbeitslasten skaliert und Datenintegrität resilienz gegenüber Beschädigungen (ungeachtet von Software- oder Hardwarefehlern).<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">Server Message Block (SMB)-Protokoll</a></h3> Eine Netzwerkdatei, die Freigabe von Netzwerkdateien und ermöglicht es Anwendungen auf einem Computer zum Lesen und Schreiben von Dateien und Dienste von Serverprogrammen in einem Computernetzwerk anzufordern. Das SMB-Protokoll kann zusätzlich zu den TCP/IP-Protokollen oder anderen Netzwerkprotokollen verwendet werden. Mit dem SMB-Protokoll kann eine Anwendung (oder der Benutzer einer Anwendung) auf Dateien oder andere Ressourcen auf einem Remoteserver zugreifen. Dadurch wird es Anwendungen ermöglicht, Dateien auf dem Remoteserver zu lesen, zu erstellen und zu aktualisieren. Anwendungen können zudem mit jedem beliebigen Serverprogramm kommunizieren, das für den Empfang einer SMB-Clientanforderung eingerichtet ist.<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">Speicherklassenspeicher</a></h3> Bietet eine ähnliche Leistung Arbeitsspeicher des Computers (sehr schnell), doch mit der Datenpersistenz normaler Speichergeräte. Windows behandelt Speicherklassenspeicher ähnlich wie normale Laufwerke (nur schneller), doch es gibt einige Unterschiede in der Verwaltung der Geräteintegrität.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">BitLocker-Laufwerkverschlüsselung</a></h3> Speichert Daten auf Volumes in einem verschlüsselten Format, auch wenn der Computer manipuliert wird oder wenn das Betriebssystem nicht ausgeführt wird. Dies bietet Schutz vor „Offline-Angriffen“, bei denen entweder das installierte Betriebssystem deaktiviert oder umgangen oder die Festplatte physisch aus dem Computer entfernt wird, um die Daten separat anzugreifen.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">NTFS</a></h3> Das primäre Dateisystem für die aktuellsten Versionen von Windows und Windows Server – bietet einen vollständigen Satz von Funktionen, einschließlich Sicherheitsdeskriptoren, Verschlüsselung, Datenträgerkontingente und umfangreiche Metadaten und kontinuierlich Bereitstellen mit Cluster freigegebenen Clustervolumes (CSV) verwendet werden können Verfügbare Volumes, die gleichzeitig von mehreren Knoten eines Failoverclusters aus zugegriffen werden können.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">Network File System (NFS)</a></h3> Stellt eine dateifreigabelösung für Unternehmen, die über heterogene Umgebungen verfügen, die von Windows und nicht-Windows-Computern bestehen.<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## In Azure

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure StorSimple](https://www.microsoft.com/en-us/cloud-platform/azure-storsimple)
