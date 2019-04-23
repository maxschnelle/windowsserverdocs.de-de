---
title: Azure-Hybridvorteil für Windows Server
description: Verwenden Ihrer lokalen Windows Server-Lizenzen zum Speichern auf Azure-VMs
ms.prod: windows-server
ms.date: 11/10/2017
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.openlocfilehash: 62821abc6c9eec660fa6af832bb1aba151708021
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884081"
---
# <a name="azure-hybrid-benefit-for-windows-server"></a>Azure-Hybridvorteil für Windows Server

>Gilt für: Windows Server

## <a name="benefit-description-rules-and-use-cases"></a>Beschreibung des Vorteils, Regeln und Anwendungsfälle

Mit dem Azure-Hybridvorteil für Windows Server können Sie auf Windows Server-VMs in Azure bis zu 40 % sparen, indem Sie Ihre vorhandenen Windows Server-Lizenzen mit Software Assurance nutzen.  Mit diesem Vorteil müssen Kunden nur die Infrastrukturkosten des virtuellen Computers bezahlen, da die Lizenzierung für Windows Server durch die Software Assurance-Leistung abgedeckt ist.  Der Vorteil gilt für Standard- und Datacenter-Editionen der Versionen 2008R2, 2012, 2012R2 und 2016 von Windows Server.  Dieser Vorteil ist in allen Regionen und unabhängigen Clouds verfügbar.


![Bild 1](media/ahb01.png)

Um den Vorteil nutzen zu können, benötigen Sie eine aktive Software Assurance- oder Abonnement-Lizenz wie EAS, SCE-Abonnement oder Open Value-Abonnement für ihre Windows Server-Lizenzen.  

Jede Windows Server 2-Prozessorlizenz mit SA/Abonnement und jede Gruppe von 16 Windows Server Core-Lizenzen mit SA/Abonnement berechtigt den Kunden, Windows Server in Microsoft Azure auf bis zu 16 virtuellen Kernen zu benutzen, die über maximal zwei Azure-Basisinstanzen (virtuelle Computer) zugeordnet sind. Jeder zusätzliche Satz von 8 Core Lizenzen mit SA/Abonnement berechtigt zur Nutzung von bis zu 8 virtuellen Kernen und einer Basisinstanz (VM).

| Lizenz mit SA/Abonnement            | VMs und Kerne            | Nutzungsmöglichkeiten                                |
|-----------------------------------------|----------------------------------|-----------------------------------------------------|
| WS-Datacenter (16 Kerne oder ein 2-Prozessorlizenz)  | Bis zu zwei VMs und bis zu 16 Kerne | VMs sowohl lokal als auch in Azure ausführbar  |
| WS-Standard (16 Kerne oder eine 2-Prozessorlizenz)    | Bis zu zwei VMs und bis zu 16 Kerne | VMs entweder lokal oder in Azure ausführbar |

VMs, die den Azure-Hybridvorteil verwenden, können in Azure nur während der SA/Abonnement-Laufzeit ausgeführt werden. Zum Ende der SA/Abonnement-Laufzeit hat der Kunde die Wahl, SA bzw. Abonnement zu erneuern, den Hybridvorteil für die entsprechende VM zu deaktivieren oder die Breitstellung dieser VM aufzuheben. 

### <a name="savings-examples"></a>Beispiele für Einsparungen 

![Bild 2](media/ahb02.png)
 
Im Folgenden finden Sie eine Referenztabelle, die Ihnen die Vorteilsregelungen verdeutlicht. In der grünen Spalte steht die Anzahl VMs gleichen Typs, und in der blauen Zeile die Kerndichte jeder VM. Die gelben Zellen enthalten die Anzahl der 2-Prozessorlizenzen (oder Gruppen von 16 Kernen), die benötigt werden, um eine bestimmte Anzahl von VMs mit einer bestimmten Kerndichte bereitzustellen. 

Referenztabelle – Anforderungen für Windows Server mit SA:

![Bild 3](media/ahb03.png)
 
Der Azure-Hybridvorteil für Windows Server ermöglicht auch die flexible Ausführung von Konfigurationen gemäß Ihren Anforderungen sowie die Kombination von VMs verschiedener Typen.

Beispielkonfigurationen für mehrere Lizenzpositionen:

![Abbildung 4](media/ahb04.png)
![Bild 5](media/ahb05.png)

 
Weitere Informationen über den Azure-Hybridvorteil für Windows Server finden Sie auf der gleichnamigen Website.

## <a name="how-to-maintain-compliance"></a>Sicherstellen der Compliance

Kunden, die den Azure-Hybridvorteil für ihre Windows Server-VMs nutzen möchten, müssen die Anzahl der berechtigten Lizenzen und die jeweilige Laufzeit von SA bzw. Abonnement vor der Aktivierung des Vorteils überprüfen und die oben aufgeführten Richtlinien anwenden, um die richtige Anzahl von VMs bereitzustellen. Wenn bereits VMs mit dem Azure-Hybridvorteil ausgeführt werden, müssen Sie die Anzahl der ausgeführten Einheiten ermitteln und überprüfen, ob entsprechende aktive SA-Lizenzen vorhanden sind.  Wenden Sie sich an Ihren Microsoft Enterprise Agreement-Lizenzierungsspezialisten, um Ihren SA-Lizenzstatus überprüfen zu lassen.
Zum Anzeigen und Zählen aller virtuellen Computer, die mit dem Azure-Hybridvorteil für Windows Server in einem Abonnement bereitgestellt wurden, können Sie einen der folgenden Schritte ausführen:

1. Konfigurieren Sie das Microsoft Azure-Portal so, dass die Verwendung des Azure-Hybridvorteils für Windows Server in der Spalte „Azure-Hybridvorteil” der Listenansicht des Abschnitts für virtuelle Computer im Microsoft Azure-Portal angezeigt wird. 

    ![Bild 6](media/ahb06.png)

2.  Verwenden Sie PowerShell, um den Azure-Hybridvorteil für Windows Server-Verwendung aufzulisten:

    ```
    $vms = Get-AzureRMVM 
    foreach ($vm in $vms) {"VM Name: " + $vm.Name, "   Azure Hybrid Benefit for Windows Server: "+ $vm.LicenseType}
    ```

3.  Entnehmen Sie Ihrer Microsoft Azure-Rechnung, wie viele virtuelle Computer mit dem Azure-Hybridvorteil für Windows Server ausgeführt werden. Die Anzahl der Instanzen mit dem Vorteil ist unter „Zusätzliche Informationen” angegeben:

    ```
    "{"ImageType":"WindowsServerBYOL","ServiceType":"Standard_A1","VMName":"","UsageType":"ComputeHR"}" 
    ```

Bitte beachten Sie, dass die Abrechnung nicht in Echtzeit erfolgt. Eine mit dem Hybridvorteil aktivierte VM wird erst nach einigen Stunden auf der Rechnung angezeigt.
Anschließend können Sie die Ergebnisse in das **Azure Hybrid Benefit for Windows Server SA Count Tool** eintragen, um die Anzahl der WS-Lizenzen zu ermitteln, die durch SA oder Abonnement abgedeckt sind.

Achten Sie darauf, eine Inventur für jedes Abonnement ausführen, das Sie besitzen, um einen umfassenden Überblick über Ihren Lizenzstatus zu generieren.

[Azure Hybrid Vorteil WS-Sacount-Tool](http://download.microsoft.com/download/7/1/2/712FEFF0-155C-4ABF-96C0-CE4EC4DB0516/Azure_Hybrid_Benefit_Windows_Server_SA_Count_Tool.xlsx)

Wenn Sie die oben genannten Schritte ausgeführt und bestätigt haben, dass Sie für die Anzahl der Azure-Hybridvorteil-Instanzen, die Sie ausführen, vollständig lizenziert sind, ist keine weitere Aktion erforderlich. Wenn Sie festgestellt haben, dass Sie inkrementelle VMs mit dem Vorteil abdecken können, möchten Sie wahrscheinlich Ihre Kosten weiter optimieren, indem Sie den Vorteil auch für Instanzen verwenden, die mit vollen Kosten ausgeführt werden.

Wenn Sie nicht genügend berechtigte Windows Server-Lizenzen für die bereits bereitgestellten VMs besitzen, müssen Sie entweder zusätzliche Windows Server-Lizenzen erwerben, die mit Software Assurance über einen der unten aufgeführten Kanäle abgedeckt sind, oder Windows Server-VMs zu regulären Stundensätzen erwerben oder den Azure-Hybridvorteil für einige VMs deaktivieren. Bitte beachten Sie, dass Sie Core-Lizenzen in Stufen von 8 Kernen erwerben können, um sich für jede weitere Azure-Hybridvorteil-VM zu qualifizieren. 

Windows Server Software Assurance-Lizenzen und/oder Abonnements können über einen der folgenden Microsoft-Lizenzierungskanäle erworben werden:

| Kanal                      | Öffnen     | OVS      | Select oder Select Plus  | MPSA       | EA/EAS   |
|------------------------------|----------|----------|-----------------------|-----------|----------|
| Typische Größe (Anzahl Geräte)  | 5-250    | 5-250    | >250                  | >250      | >500     |
| SA/Abonnement            | Optional | Eingeschlossen | Optional              | Optional  | Eingeschlossen |

Microsoft behält sich das Recht vor, jederzeit zu überprüfen, ob der Endkunde berechtigt ist, den Azure-Hybridvorteil zu nutzen 

## <a name="deployment-guidance"></a>Bereitstellungsanleitung 

Wir haben für unsere Kunden, die berechtigte Lizenzen besitzen (unabhängig davon, wo diese gekauft wurden), vorgefertigte Galerie-Images bereitgestellt. Außerdem haben berechtigte Partner die Möglichkeit, die Bereitstellungen für Kunden durchzuführen. 

Anweisungen für alle verfügbaren Bereitstellungsoptionen finden Sie [hier](https://azure.microsoft.com/pricing/hybrid-use-benefit/), einschließlich: 
-   Detailliertes Video, in dem die neue Bereitstellungsmethode mit vorgefertigten Galerie-Images erläutert wird
-   Ausführliche Anweisungen zum Hochladen einer kundenspezifischen VM 
-   Detaillierte Informationen zum Migrieren von vorhandenen virtuellen Computern mithilfe von Azure Site Recovery und PowerShell. 
