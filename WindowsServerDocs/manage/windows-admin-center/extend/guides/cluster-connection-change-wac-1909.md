---
title: Änderungen der Änderungen am Cluster Verbindungstyp im Windows Admin Center v1909
description: Änderungen der Änderungen am Cluster Verbindungstyp im Windows Admin Center v1909
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 10/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a07b30517f0d45b7e6f4f41f0ef9a6549e6e2117
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952771"
---
# <a name="cluster-connection-type-changes-in-windows-admin-center-v1909"></a>Änderungen der Änderungen am Cluster Verbindungstyp im Windows Admin Center v1909

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

> [!IMPORTANT]
> In diesem Dokument werden die Änderungen beschrieben, die von Entwicklern der Windows Admin Center-Erweiterung benötigt werden, die Windows Admin Center-Tools für Failovercluster-und hyperkonvergierte Clusterlösungen (HCI) entwickeln. Dies ist eine obligatorische Änderung, die erforderlich ist, damit Ihre Erweiterung mit Windows Admin Center kompatibel ist v1909 Vorschauversion und zukünftige allgemein verfügbare Versionen.

Im Windows Admin Center v1909 haben wir die beiden unterschiedlichen Cluster Verbindungstypen (Failovercluster und hyperkonvergierte Cluster Verbindungen) in einem einzigen Cluster Verbindungstyp vereinheitlicht. Benutzer müssen die Konfiguration eines Clusters nicht mehr im Voraus identifizieren, um zu entscheiden, welcher Verbindungstyp dem Cluster hinzugefügt werden soll, und den Cluster nicht zweimal als unterschiedliche Verbindungstypen hinzufügen, um Zugriff auf die verschiedenen Toolsets zu erhalten. Cluster können nun als "Windows Server-Cluster" hinzugefügt werden, und die entsprechenden Tools werden geladen. Dies hängt in erster Linie davon ab, ob direkte Speicherplätze aktiviert ist.

Da dies eine Änderung in der Verbindungstyp Definition erforderte und die Entscheidung, wie Cluster bezogene Tools geladen werden sollen, benötigt werden, benötigen Erweiterungen, die Tools für Cluster (HCI-oder nicht-HCI-Cluster oder beides) bereitstellen, die in der Implementierung beschriebenen Änderungen. untenstehende.

## <a name="manifestjson---solutionsids-and-connectiontypes"></a>Manifest. JSON-solutionsids und connectiontypes

Wenn Sie das Tool zuvor für einen Failovercluster oder einen HCI-Cluster Verbindungstyp angezeigt haben, hätten Sie eine der folgenden Definitionen in der ```manifest.json```-Datei verwendet.

Für Failovercluster:
``` json
    {
        "entryPointType": "tool",
        "name": "MyToolName",
        "urlName": "MyToolUrl",
        "displayName": "MyToolDisplayName",
        "description": "MyToolDescription",
        "icon": "MyToolIcon",
        "path": "MyToolPath",
        "iframeId": "MyToolIframeId",
        "requirements": [
        {
            "solutionIds": [
                "msft.sme.failover-cluster!failover-cluster"
            ],
            "connectionTypes": [
                "msft.sme.connection-type.cluster"
            ]
        }
        ]
    }
```

Für HCI-Cluster hätte der hervorgehobene obige Abschnitt durch Folgendes ersetzt:
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster"
        ]
    }
    ]
```

In Windows Admin Center 1909 und höher wurden die beiden solutionids und connectiontypes durch Folgendes ersetzt:
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.cluster"
        ]
    }
    ]
```

Dies sind die einzigen Cluster bezogenen solutionids und connectiontypes-Typen, die ab jetzt unterstützt werden. Wenn das Tool nur mit dem Typ "solutionids" und "connectiontypes" definiert ist, wird es für jede beliebige failoverclusterverbindung geladen, unabhängig davon, ob es sich um einen HCI-Cluster handelt. Wenn Sie möchten, dass Ihr Tool nur für HCI-Cluster oder nicht-HCI-Cluster verfügbar ist, müssen Sie zusätzlich die neuen Inventur Eigenschaften verwenden, die im folgenden Abschnitt beschrieben werden.

## <a name="manifestjson--inventory-properties"></a>Manifest. JSON – Inventur Eigenschaften
Beim Herstellen einer Verbindung mit einem Server oder Cluster wird von Windows Admin Center ein Satz von Inventur Eigenschaften abgefragt, die Sie zum Erstellen von Bedingungen verwenden können, um zu bestimmen, wann das Tool verfügbar sein sollte. (Weitere Informationen finden Sie im Abschnitt "Inventur Eigenschaften" im [Steuerelement Sichtbarkeits](dynamic-tool-display.md) Dokument für weitere Informationen). In Windows Admin Center v1909 haben wir dieser Liste zwei neue Eigenschaften hinzugefügt, mit denen bestimmt werden kann, ob es sich bei einem Cluster um einen hyperkonvergenten Cluster handelt. 

### <a name="iss2denabled"></a>isS2dEnabled
Technisch gesehen wird ein hyperkonvergierter Cluster als Failovercluster mit aktiviertem direkte Speicherplätze (S2D) definiert. Wenn Sie möchten, dass das Tool nur für hyperkonvergierte Cluster verfügbar ist, d. h., wenn S2D aktiviert ist, fügen Sie die folgende Inventur Bedingung hinzu:
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.cluster"
        ],
        "conditions": [
        {
            "inventory": {
                "isS2dEnabled": {
                    "type": "boolean",
                    "operator": "is"
                }
            }
        }
        ]
    }
    ]
```
> [!TIP] 
> Wenn Sie möchten, dass das Tool nur verfügbar ist, wenn S2D nicht aktiviert ist, ändern Sie den Wert "Operator" in "Not".

### <a name="isbritannicaenabled"></a>isbritannicaaktivierte
Wenn Sie von der SDDC-Verwaltungs Cluster Ressource abhängig sind und das SDDC-Objektmodell verwenden, können Sie außerdem die folgende Bedingung überprüfen:
``` json
    "conditions": [
        {
            "inventory": {
                "isS2dEnabled": {
                    "type": "boolean",
                    "operator": "is"
                },
                "isBritannicaEnabled": {
                    "type": "boolean",
                    "operator": "is"
                }
            }
        }
    ]
```

## <a name="backward-compatibility-to-support-previous-versions-of-windows-admin-center"></a>Abwärtskompatibilität zur Unterstützung früherer Versionen von Windows Admin Center
Um sicherzustellen, dass die Erweiterung weiterhin mit älteren Versionen des Windows Admin Centers funktioniert, z. b. mit der v1904 GA-Version, können die vorherigen Definitionen von solutionids und connectiontypes zusammen mit der neuen Definition verwendet werden. Sehen Sie sich das folgende Beispiel an, um das Tool nur für HCI-Cluster in allen Versionen von Windows Admin Center anzuzeigen.
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster"
        ]
    },
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC",
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster",
            "msft.sme.connection-type.cluster"
        ],
        "conditions": [
            {
                "inventory": {
                    "isS2dEnabled": {
                        "type": "boolean",
                        "operator": "is"
                    }
                }
            }
        ]
    }
    ]
```

## <a name="known-issue-appcontextserviceactiveconnectionishyperconvergedclusterisfailovercluster-is-not-set-properly-in-windows-admin-center-v1909"></a>Bekanntes Problem: Appcontextservice. ActiveConnection. ishyperkonvergedcluster/isfailovercluster ist im Windows Admin Center nicht ordnungsgemäß festgelegt v1909
Eine Regression von kürzlich vorgenommenen Änderungen besteht darin, dass die ```AppContextService.activeConnection.isHyperConvergedCluster/isFailoverCluster```-Eigenschaften nicht ordnungsgemäß im Windows Admin Center festgelegt sind v1909 und immer false ist. Dies wird in der nächsten Version, v1910, korrigiert, wird aber auch als veraltet eingestuft und ist nicht mehr in der folgenden GA-Version in 2020 verfügbar. In Zukunft können Sie dies durch den folgenden Code ersetzen und ```this.connectHCI``` verwenden.
```
    import { ClusterInventoryCache } from '@msft-sme/core';

    constructor(
        ...
        private appContextService: AppContextService,
        ...
    ) {
        ...
        this.clusterInventoryCache = new ClusterInventoryCache(
            this.appContextService,
            <SharedCacheOptions>{ expiration: Constants.sharedCacheExpiration }
        );

         this.isBritannicEnabled().subscribe(result => this.connectHCI = result);
    }

    private isBritannicEnabled(): Observable<boolean> {
        return this.clusterInventoryCache.query(this.getClusterInventoryQueryParameters())
        .pipe(
            map(inventory => {
                return inventory.instance.isBritannicaEnabled;
        }));
    }

    private getClusterInventoryQueryParameters(): ClusterInventoryParams {
        const nodeName = this.appContextService.activeConnection.validNodeName;
        const endpoint = this.appContextService.authorizationManager.getJeaEndpoint(nodeName);
        const options = { powerShellEndpoint: endpoint };
        return {
            name: nodeName,
            requestOptions: options
        };
    }
```