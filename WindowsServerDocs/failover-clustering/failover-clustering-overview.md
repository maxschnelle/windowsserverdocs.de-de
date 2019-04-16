---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: Failoverclustering
ms.prod: windows-server-threshold
layout: LandingPage
ms.topic: landing-page
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 03/08/2019
ms.localizationpriority: high
ms.openlocfilehash: 445de065ff5b68b83481ee5bd83ebf18fdd180a7
ms.sourcegitcommit: b0fece76b871da3fa9d6a996798a5008756f486b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2019
ms.locfileid: "9178601"
---
# Failoverclustering in Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen auf [dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />

Ein Failovercluster ist eine Gruppe aus unabhängigen Computern, die miteinander interagieren, um die Verfügbarkeit und Skalierbarkeit von Clusterrollen (früher Clusteranwendungen und -dienste genannt) zu erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem oder mehreren der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort von anderen Knoten übernommen. Dieser Vorgang wird als Failover bezeichnet. Zusätzlich werden die Clusterrollen proaktiv überwacht, um sicherzustellen, dass sie ordnungsgemäß funktionieren. Funktionieren sie nicht, werden sie neu gestartet oder auf einen anderen Knoten verschoben.

Failovercluster stellen darüber hinaus Funktionen für freigegebene Clustervolumes (Cluster Shared Volume, CSV) mit einem konsistenten verteilten Namespace bereit, mit dem Clusterrollen von allen Knoten aus auf den freigegebenen Speicher zugreifen können. Failoverclustering sorgt dafür, dass die Unterbrechung auf Benutzerseite nur minimal ist.

Für Failoverclustering gibt es viele praktische Anwendungsfälle, einschließlich:
* Hoch verfügbarer oder fortlaufend verfügbarer Dateifreigabespeicher für Anwendungen wie Microsoft SQL Server und Hyper-V-basierte virtuelle Computer
* Hoch verfügbare Clusterrollen, die auf physischen Servern oder virtuellen Computern ausgeführt werden, die auf Servern mit Hyper-V installiert sind

<hr />

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h2><a href="whats-new-in-failover-clustering.md">Neuigkeiten in Failoverclustering</a></h2>
                                        </div>
                                    </div>
                                </div>
                             </div>
                          </a>
                        </li>
                     </ul>
<HR />

<ul class="cardsF panelContent">

<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>Grundlegende Informationen</h3>
<HR />
                                        <p><a href="sofs-overview.md">Dateiserver mit horizontaler Skalierung für Anwendungsdaten</a></p>
<HR />
                                        <p><a href="../storage/storage-spaces/understand-quorum.md">Cluster und Pool quorum</a></p>
<HR />
                                        <p><a href="fault-domains.md">Fehlerdomänenunterstützung</a></p>
<HR />
                                        <p><a href="smb-multichannel.md">Vereinfachte SMB-Multichannel- und Multi-NIC-Clusternetzwerke</a></p>
<HR />
                                        <p><a href="vm-load-balancing-overview.md">VM-Lastenausgleich</a></p>
<HR />
                                        <p><a href="../storage/storage-spaces/cluster-sets.md">Cluster-Gruppen</a></p>
<HR />
                                        <p><a href="cluster-affinity.md">Cluster-Affinität</a></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>

<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>Planung</h3>
<HR />
                                        <p><a href="clustering-requirements.md">Hardwareanforderungen und Speicheroptionen für Failoverclustering</a></p>
<HR />
                                        <p><a href="failover-cluster-csvs.md">Verwenden von freigegebenen Clustervolumes (CSVs)</a></p>               
<HR />
                                        <p><a href="../storage/storage-spaces/storage-spaces-direct-in-vm.md">Verwenden von virtuellen Gastcomputerclustern mit Storage Spaces Direct</a></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>Bereitstellung</a></h3> 
<HR />
                                        <p><a href="prestage-cluster-adds.md">Prestage-Clustercomputerobjekte in Active Directory Domain Services</a></p>
<HR />
                                        <p><a href="create-failover-cluster.md">Erstellen eines Failoverclusters</a></p> 
<HR />
                                        <p><a href="deploy-two-node-clustered-file-server.md">Bereitstellen eines Dateiservers mit zwei Knoten</a></p> 
<HR />
                                        <p><a href="manage-cluster-quorum.md">Verwalten von Quorum und Zeugen</a></p> 
<HR />
                                        <p><a href="deploy-cloud-witness.md">Bereitstellen eines Cloudzeugen</a></p>
<HR />
                                        <p><a href="file-share-witness.md">Bereitstellen eines Dateifreigabezeugen</a></p>
<HR />
                                        <p><a href="cluster-operating-system-rolling-upgrade.md">Paralleles Upgrade für Clusterbetriebssystem</a></p> 
<HR />
                                        <p><a href="upgrade-option-same-hardware.md">Upgrade eines Failoverclusters auf derselben Hardware</a></p>
<HR />
                                        <p><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\)">Bereitstellen eines von Active Directory getrennten Clusters</a></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
                     </ul>
<HR />
<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>Verwalten</h3>
<HR />
                                        <p><a href="cluster-aware-updating.md">Cluster-Aware Updating</a></p> 
<HR />
                                        <p><a href="health-service-overview.md">Zustandsdienst</a></p>
<HR />
                                        <p><a href="cluster-domain-migration.md">Clusterdomänenmigration</a></p>
<HR />
                                        <p><a href="troubleshooting-using-wer-reports.md">Problembehandlung mit der Windows-Fehlerberichterstattung</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>Tools und Einstellungen</a></h3>
<HR />
                                        <p><a href="https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps">PowerShell-Cmdlets für Failoverclustering</a></p> 
<HR />
                                        <p><a href="https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps">PowerShell-Cmdlets für das clusterfähige Aktualisieren</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>Communityressourcen</a></h3>
<HR />
                                        <p><a href="https://go.microsoft.com/fwlink/p/?LinkId=230641">Forum für hohe Verfügbarkeit (Clustering)</a></p> 
<HR />
                                        <p><a href="http://blogs.msdn.com/b/clustering/">Teamblog zu Failoverclustering und Netzwerklastenausgleich</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
