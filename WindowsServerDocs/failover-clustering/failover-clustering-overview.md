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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848651"
---
# <a name="failover-clustering-in-windows-server"></a>Failoverclustering in Windows Server

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />

Ein Failovercluster ist eine Gruppe aus unabhängigen Computern, die miteinander interagieren, um die Verfügbarkeit und Skalierbarkeit von Clusterrollen (früher Clusteranwendungen und -dienste genannt) zu erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem oder mehreren der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort von anderen Knoten übernommen. Dieser Vorgang wird als Failover bezeichnet. Zusätzlich werden die Clusterrollen proaktiv überwacht, um sicherzustellen, dass sie ordnungsgemäß funktionieren. Funktionieren sie nicht, werden sie neu gestartet oder auf einen anderen Knoten verschoben.

Failovercluster stellen darüber hinaus Funktionen für freigegebene Clustervolumes (Cluster Shared Volume, CSV) mit einem konsistenten verteilten Namespace bereit, mit dem Clusterrollen von allen Knoten aus auf den freigegebenen Speicher zugreifen können. Das Failoverclusteringfeature sorgt dafür, dass die Unterbrechung auf Benutzerseite nur minimal ist.

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
                                        <h2><a href="whats-new-in-failover-clustering.md">Neues beim Failoverclustering</a></h2>
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
                                        <p><a href="sofs-overview.md">Dateiserver für horizontales Skalieren für Anwendungsdaten</a></p>
<HR />
                                        <p><a href="../storage/storage-spaces/understand-quorum.md">Cluster und Pool-quorum</a></p>
<HR />
                                        <p><a href="fault-domains.md">Fehlerdomänenunterstützung</a></p>
<HR />
                                        <p><a href="smb-multichannel.md">Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke</a></p>
<HR />
                                        <p><a href="vm-load-balancing-overview.md">VM-Lastenausgleich</a></p>
<HR />
                                        <p><a href="../storage/storage-spaces/cluster-sets.md">Clustersätze</a></p>
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
                                        <h3>Planen</h3>
<HR />
                                        <p><a href="clustering-requirements.md">Failoverclustering-Hardwareanforderungen und Speicheroptionen</a></p>
<HR />
                                        <p><a href="failover-cluster-csvs.md">Verwenden von freigegebenen Clustervolumes (CSV)</a></p>               
<HR />
                                        <p><a href="../storage/storage-spaces/storage-spaces-direct-in-vm.md">Verwenden von gastclustern für virtuelle Computer mit "direkte Speicherplätze"</a></p>
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
                                        <p><a href="prestage-cluster-adds.md">Vorabbereitstellen von Clustercomputerobjekten in Active Directory-Domänendienste</a></p>
<HR />
                                        <p><a href="create-failover-cluster.md">Erstellen eines Failoverclusters</a></p> 
<HR />
                                        <p><a href="deploy-two-node-clustered-file-server.md">Bereitstellen eines Dateiservers mit zwei Knoten</a></p> 
<HR />
                                        <p><a href="manage-cluster-quorum.md">Verwalten des Quorums und Zeugen</a></p> 
<HR />
                                        <p><a href="deploy-cloud-witness.md">Bereitstellen eines cloudzeugen</a></p>
<HR />
                                        <p><a href="file-share-witness.md">Bereitstellen Sie ein dateifreigabezeugen</a></p>
<HR />
                                        <p><a href="cluster-operating-system-rolling-upgrade.md">Parallele Upgrades Clusterbetriebssystem</a></p> 
<HR />
                                        <p><a href="upgrade-option-same-hardware.md">Upgrade eines Failoverclusters auf derselben hardware</a></p>
<HR />
                                        <p><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\)">Bereitstellen eines Active Directory getrennten Clusters</a></p>
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
                                        <p><a href="cluster-aware-updating.md">Clusterfähiges aktualisieren</a></p> 
<HR />
                                        <p><a href="health-service-overview.md">Integritätsdienst</a></p>
<HR />
                                        <p><a href="cluster-domain-migration.md">Clusterdomäne migration</a></p>
<HR />
                                        <p><a href="troubleshooting-using-wer-reports.md">Problembehandlung mithilfe der Windows-Fehlerberichterstattung</a></p> 
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
                                        <p><a href="https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps">Failoverclustering PowerShell-Cmdlets</a></p> 
<HR />
                                        <p><a href="https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps">Beachten Sie PowerShell-Cmdlets aktualisieren-Cluster</a></p> 
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
                                        <p><a href="http://blogs.msdn.com/b/clustering/">Laden von Failoverclustering und Netzwerklastenausgleichs-Teamblog</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
