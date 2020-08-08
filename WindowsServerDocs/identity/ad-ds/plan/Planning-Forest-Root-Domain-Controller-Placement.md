---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 125aa57086a396c643cc3c042376b7fecc17ede8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970967"
---
# <a name="planning-forest-root-domain-controller-placement"></a>Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zum Erstellen von Vertrauens Pfaden für Clients, die auf Ressourcen in anderen Domänen als ihren eigenen zugreifen müssen, sind Gesamtstruktur-Stamm Domänen Controller erforderlich. Platzieren Sie Gesamtstruktur-Stamm Domänen Controller an Hub-Standorten und an Standorten, die Daten Center hosten Wenn Benutzer an einem bestimmten Speicherort auf Ressourcen aus anderen Domänen am gleichen Speicherort zugreifen müssen und die Netzwerkverfügbarkeit zwischen dem Rechenzentrum und dem Speicherort des Benutzers unzuverlässig ist, können Sie entweder einen Gesamtstruktur-Stamm Domänen Controller am Standort hinzufügen oder eine Vertrauensstellung zwischen den beiden Domänen erstellen. Es ist kostengünstiger, eine Vertrauensstellung zwischen den Domänen zu erstellen, es sei denn, Sie haben andere Gründe, einen Gesamtstruktur-Stamm Domänen Controller an diesem Speicherort zu platzieren.

Vertrauens Stellungen helfen bei der Optimierung von Authentifizierungsanforderungen von Benutzern, die sich in einer der beiden Domänen befinden. Weitere Informationen zu Verknüpfungs Vertrauensstellungen zwischen Domänen finden Sie im Artikel grundlegendes [zum Erstellen einer Vertrauensstellungs Abkürzung](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc754538(v=ws.11)).

Ein Arbeitsblatt, das Sie bei der Dokumentation der Platzierung des Stamm Domänen Controllers Ihres Gesamtstruktur-Stamm Verzeichnisses unterstützt, finden Sie unter [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Download Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip und Öffnen von "Domänen Controller Platzierung" (DSSTOPO_4.doc).

Sie müssen diese Informationen beachten, wenn Sie die Stamm Domäne der Gesamtstruktur erstellen. Weitere Informationen zum Bereitstellen der Stamm Domäne der Gesamtstruktur finden Sie unter Bereitstellen [einer Windows Server 2008](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))-Gesamtstruktur-Stamm Domäne.
