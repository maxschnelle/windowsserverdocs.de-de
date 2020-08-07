---
title: Schritt 9 Edge1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a0e21b9b0a0d926d2d4d166fbe3c87fee6c340fc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955198"
---
# <a name="step-9-configure-edge1"></a>Schritt 9 Edge1 konfigurieren

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die folgenden Prozeduren werden auf dem Edge1-Server ausgeführt:

1. Konfigurieren Sie die DNS-Server auf Edge1. Es ist erforderlich, den DNS-Server in der corp2.Corp.contoso.com-Domäne auf Edge1 zu konfigurieren.

2. Konfigurieren Sie das Routing zwischen Subnetzen. Konfigurieren Sie das Routing auf Edge1, um die Kommunikation zwischen den Subnetzen Corpnet und 2-Corpnet zu ermöglichen.

## <a name="configure-the-dns-servers-on-edge1"></a><a name="IPv6"></a>Konfigurieren der DNS-Server auf Edge1

1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **Corpnet**auf den Link.

2.  Klicken Sie im Fenster Netzwerkverbindungen mit der rechten Maustaste auf **Corpnet**, und klicken Sie dann auf **Eigenschaften**.

3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.

4.  Geben Sie im **alternativen DNS-Server** **10.2.0.1 bis**ein. ein, und klicken Sie dann auf **OK**.

5.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.

6.  Geben Sie im **alternativen DNS-Server** **2001: db8:2:: 1 ein** , und klicken Sie dann auf **OK**.

7.  Klicken Sie im Dialogfeld **Corpnet-Eigenschaften** auf **Schließen**.

8.  Schließen Sie das Fenster **Netzwerkverbindungen**.

## <a name="configure-routing-between-subnets"></a><a name="ConfigRouting"></a>Konfigurieren des Routings zwischen Subnetzen

1.  Geben Sie auf dem **Start** Bildschirm**cmd.exe**ein, klicken Sie mit der rechten Maustaste auf **cmd**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

2.  Geben Sie im Eingabe Aufforderungs Fenster die folgenden Befehle ein. Drücken Sie nach dem Eingeben der einzelnen Befehle die EINGABETASTE.

    ```
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe
    ```

3.  Schließen Sie das Eingabeaufforderungsfenster.



