﻿---
external help file: powershai-help.xml
schema: 2.0.0
powershai: true
---

# Send-PowershaiChat

## SYNOPSIS <!--!= @#Synop !-->
Invia un messaggio in una chat di Powershai

## DESCRIPTION <!--!= @#Desc !-->
Questo cmdlet consente di inviare un nuovo messaggio al LLM del provider corrente.  
Per impostazione predefinita, invia nella chat attiva. Puoi sovrascrivere la chat usando il parametro -Chat.  Se non c'è una chat attiva, userà quella predefinita.  

Diversi parametri della chat influenzano il modo in cui questo comando funziona. Guarda il comando Get-PowershaiChatParameter per maggiori informazioni sui parametri della chat.  
Oltre ai parametri della chat, i parametri del comando stesso possono sovrascrivere il comportamento.  Per maggiori dettagli, consulta la documentazione di ogni parametro di questo cmdlet usando get-help.  

Per semplicità, e per mantenere la riga di comando pulita, consentendo all'utente di concentrarsi maggiormente sul prompt e sui dati, sono disponibili alcuni alias.  
Questi alias possono attivare determinati parametri.
Sono:
	ia|ai
		Abbreviazione di "Intelligenza Artificiale" in italiano. Questo è un semplice alias e non cambia alcun parametro. Aiuta a ridurre notevolmente la riga di comando.
	
	iat|ait
		Lo stesso di Send-PowershaAIChat -Temporary
		
	io|ao
		Lo stesso di Send-PowershaAIChat -Object

L'utente può creare i propri alias. Ad esempio:
	Set-Alias ki ia # DEfine l'alias per il tedesco!
	Set-Alias kit iat # DEfine l'alias kit per iat, rendendo il comportamento identico a iat (chat temporanea) quando si usa kit!

## SYNTAX <!--!= @#Syntax !-->

```
Send-PowershaiChat [[-prompt] <Object>] [-SystemMessages <Object>] [-context <Object>] [-ForEach] [-Json] [-Object] [-PrintContext] [-Forget] [-Snub] [-Temporary] 
[-DisableTools] [-FormatterFunc <Object>] [-FormatterParams <Object>] [-PassThru] [-Lines] [<CommonParameters>]
```

## PARAMETERS <!--!= @#Params !-->

### -prompt
il prompt da inviare al modello

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 1
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -SystemMessages
Messaggio di sistema da includere

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: @()
Accept pipeline input: false
Accept wildcard characters: false
```

### -context
Il contesto 
Questo parametro è per essere usato preferibilmente dal pipeline.
Farà in modo che il comando metta i dati in tag <contexto></contexto> e li inietti insieme nel prompt.

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: 
Accept pipeline input: true (ByValue)
Accept wildcard characters: false
```

### -ForEach
Forza il cmdlet a eseguire per ogni oggetto del pipeline
Per impostazione predefinita, accumula tutti gli oggetti in un array, converte l'array in stringa e lo invia tutto insieme al LLM.

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -Json
Abilita la modalità json 
in questa modalità i risultati restituiti saranno sempre un JSON.
Il modello corrente deve supportare!

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -Object
Modalità Object!
in questa modalità la modalità JSON verrà attivata automaticamente!
Il comando non scriverà nulla sullo schermo e restituirà i risultati come un oggetto!
Che verranno rimandati al pipeline!

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -PrintContext
Mostra i dati di contesto inviati al LLM prima della risposta!
È utile per depennare cosa viene iniettato di dati nel prompt.

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -Forget
Non inviare le conversazioni precedenti (la cronologia del contesto), ma includere il prompt e la risposta nella cronologia del contesto.

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -Snub
Ignora la risposta del LLM e non includere il prompt nella cronologia del contesto

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -Temporary
Non inviare la cronologia e non includere la risposta e il prompt.  
È lo stesso di passare -Forget e -Snub insieme.

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -DisableTools
Disabilita la chiamata di funzione per questa esecuzione solo!

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: NoCalls,NoTools,nt
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -FormatterFunc
Cambia il formatter del contesto per questo
Guarda di più in Format-PowershaiContext

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -FormatterParams
Parametri del formatter del contesto modificato.

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -PassThru
Restituisce i messaggi al pipeline, senza scrivere direttamente sullo schermo!
Questa opzione presuppone che l'utente sarà responsabile della destinazione corretta del messaggio!
L'oggetto passato al pipeline avrà le seguenti proprietà:
	text 			- Il testo (o il passaggio) del testo restituito dal modello 
	formatted		- Il testo formattato, incluso il prompt, come se fosse scritto direttamente sullo schermo (senza i colori)
	event			- L'evento. Indica l'evento che ha generato. Sono gli stessi eventi documentati in Invoke-AiChatTools
	interaction 	- L'oggetto interaction generato da Invoke-AiChatTools

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -Lines
Restituisce un array di righe 
Se la modalità stream è attivata, restituirà una riga alla volta!

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```




<!--PowershaiAiDocBlockStart-->
_Tradotto automaticamente tramite PowerShell e IA. 
_
<!--PowershaiAiDocBlockEnd-->