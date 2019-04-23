---
title: Verwalten von-Bde-tpm
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2b8390d49257c3c6acd9ed4fd45773e5a65aac4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840581"
---
# <a name="manage-bde-tpm"></a>Verwalten von-Bde: Tpm

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

> [!IMPORTANT]
> Mit diesem Befehl wird für die Verwendung auf Computern unter Windows 8, Windows Server 2012 oder höher nicht unterstützt. Für solche Computer können Sie die [TPM-Verwaltungs-Cmdlets für Windows PowerShell](https://technet.microsoft.com/library/jj603116.aspx).
Wenn Sie diesen Befehl auf Computer unter Windows 7 oder Windows Server 2008 verwenden, können Sie weiterhin des Computers Trusted Platform Module (TPM) mit folgendem Befehl konfigurieren. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).
## <a name="syntax"></a>Syntax
```
manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-Aktivieren|Ermöglicht, und aktiviert das TPM und Zulassen von TPM-Besitzerkennwort festgelegt werden. Sie können auch **-t** als eine verkürzte Version des mit diesem Befehl.|
|-takeownership|Wird der TPM-Besitzrechte durch Festlegen eines Kennworts Besitzer an. Sie können auch **- e/a** als eine verkürzte Version des mit diesem Befehl.|
|<OwnerPassword>|Stellt die, das Sie, für das TPM angeben-Besitzerkennwort dar.|
|-computername|Gibt an, dass diese verwalten-bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Zeigt Hilfe an der Eingabeaufforderung abgeschlossen werden.|
## <a name="BKMK_Examples"></a>Beispiele für
Das folgende Beispiel veranschaulicht die Verwendung der **- Tpm** Befehl aus, um das TPM einzuschalten.
```
manage-bde  tpm -turnon
```
Das folgende Beispiel veranschaulicht die Verwendung der ** Tpm ** Befehl aus, um den Besitz des TPM übernehmen, und legen das Kennwort des Besitzers auf 0wnerP@ss.
```
manage-bde  tpm  takeownership 0wnerP@ss
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
