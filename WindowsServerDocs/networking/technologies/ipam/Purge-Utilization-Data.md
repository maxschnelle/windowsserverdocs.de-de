---
title: Endgültiges Löschen von Nutzungsdaten
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab2bd3ad1ef8965400e09fa74c6eb89ffc5ebcef
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283845"
---
# <a name="purge-utilization-data"></a>Endgültiges Löschen von Nutzungsdaten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, Informationen zum Löschen von Nutzungsdaten aus der IPAM-Datenbank.  

Sie müssen ein Mitglied sein **IPAM-Administratoren**, dem lokalen Computer **Administratoren** oder einer gleichwertigen Gruppe, um dieses Verfahren auszuführen.

## <a name="to-purge-the-ipam-database"></a>So löschen Sie die IPAM-Datenbank  
1. Öffnen Sie Server-Manager, und navigieren Sie dann auf die IPAM-Client-Schnittstelle.
2. Suchen Sie einen der folgenden Speicherorte: **IP-Adressblöcke**, **IP-Adressbestand**, oder **IP-Adressbereichsgruppen**.  
3. Klicken Sie auf **Aufgaben**, und klicken Sie dann auf **Löschen von Nutzungsdaten**. Die **Löschen von Nutzungsdaten** Dialogfeld wird geöffnet.
4. In **löschen Sie alle Auslastung Daten am oder vor**, klicken Sie auf **wählen Sie ein Datum**.
5. Wählen Sie das Datum, die für das Sie alle Datenbankdatensätze auf und vor diesem Datum löschen möchten.
6. Klicken Sie auf **OK**. IPAM löscht alle Datensätze, die Sie angegeben haben.
