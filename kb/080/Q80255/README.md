---
layout: page
title: "Q80255: PC Gen: Contents of Modem Script File DEFAULT.MDM"
permalink: /kb/080/Q80255/
---

## Q80255: PC Gen: Contents of Modem Script File DEFAULT.MDM

{% raw %}

	Article: Q80255
	Product(s): Microsoft Mail For PC Networks
	Version(s): WINDOWS:2.1e
	Operating System(s): 
	Keyword(s): 
	Last Modified: 30-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Mail for PC Networks, version 2.1e 
	-------------------------------------------------------------------------------
	
	The following is the contents of the Microsoft Mail version 2.1d
	modem script file DEFAULT.MDM, which can be compiled with SCRCOMP.EXE:
	
	  ;********************************************************************
	  ;
	  ;                    Microsoft Mail Script File
	  ;
	  ;       Filename: default.mdm
	  ;       Date    : March 21, 1990
	  ;       Script  : Standard script file for Hayes-compatible modems
	  ;
	  ;     This script file contains the standard modem setup strings used
	  ;  by the External, Transmit and Listen programs. There are five
	  ;  procedures defined in this script file for setting up the modem and
	  ;  for connecting to a remote External machine.
	  ;
	  ;     The modem setup strings used here will be adequate for most
	  ;  people but there may be some changes required if you are dialing
	  ;  overseas and require a longer wait for Carrier Detect (S7 register)
	  ;  or if you wish to change the speaker volume. Note that if you used
	  ;  the -Innn option in version 1.0 or 2.0 that you will have to modify
	  ;  the S7 register and recompile this script file.
	  ;
	  ;     Consult your modem manual for more information on setup options.
	  ;
	  ;  Script procedures defined:
	  ;       INITIALIZE
	  ;       RESET
	  ;       CALL
	  ;       ANSWER
	  ;       DISCONNECT
	  ;
	  ;  Return codes for External, Transmit, Listen:
	  ;       0  - OK
	  ;       1  - CONNECT 300
	  ;       2  - not defined
	  ;       3  - NO CARRIER
	  ;       4  - ERROR
	  ;       5  - CONNECT 1200
	  ;       6  - not defined
	  ;       7  - BUSY
	  ;       8  - NO ANSWER
	  ;       9  - not defined
	  ;      10  - CONNECT 2400
	  ;      11  - not defined
	  ;      12  - CONNECT 9600 (high speed connection)
	  ;
	  ;********************************************************************
	
	  INITIALIZE:
	          title "Default Script"
	
	          $attempts = 5
	
	  init_retry:
	          sendln "ATZ"           ; reset modem to default settings
	          wait 2
	          waitrsp 1
	
	          if ("0" isin response)
	              goto reset_okay
	
	          if ("OK" isin response)
	              {
	  reset_okay:
	              sendln "ATE0V0X1"
	              wait 1
	              waitrsp 1
	
	              if ("0^M" isin response)
	                  {
	                  sendln "ATS0=0S7=45S9=6S10=50S12=50"
	                  waitrsp 1
	                  if (response = "0^M")
	                      return 0
	                  }
	               }
	          dec $attempts
	          if ($attempts > 0)
	                  goto init_retry
	
	          return 4
	
	  RESET:
	          sendln "ATZ"           ; reset modem to default settings
	          wait 2
	          waitrsp 1
	
	          if ("0" isin response)
	              goto reset_okay
	
	          if ("OK" isin response)
	              {
	  reset_okay:
	              sendln "ATE0V0X1"
	              wait 1
	              waitrsp 1
	
	              if ("0^M" isin response)
	                  {
	                  sendln "ATS0=0S7=45S9=6S10=50S12=50"
	                  waitrsp 1
	                  if (response = "0^M")
	                      return 0
	                  else
	                      return 4
	
	                  }
	               }
	
	          return 4
	
	  CALL:
	          $ret = 8               ; set default ret code to "no answer"
	
	          clearrsp               ; clear the response buffer
	
	          echo 0                 ; do not display phone number
	
	          sendln "ATD" + dial_mode + phone_number  ; execute the dial up
	
	          echo 1                 ; turn echo back on
	
	          waitrsp 120            ; wait up to 2 minutes for return code
	                                 ;    from modem
	
	          if (response = "1^M")
	            {
	            baud 300
	            display ">>> CONNECT 300 <<<"
	            $ret = 1
	            }
	          else if (response = "3^M")
	            {
	            display ">>> NO CARRIER <<<"
	            $ret = 8             ; no answer
	            }
	          else if (response = "5^M")
	            {
	            baud 1200
	            display ">>> CONNECT 1200 <<<"
	            $ret = 5
	            }
	          else if (response = "10^M")
	            {
	            baud 2400
	            display ">>> CONNECT 2400 <<<"
	            $ret = 10
	            }
	
	          return $ret            ; return connect baud rate to
	                                 ;    application
	
	  ANSWER:
	          $ret = 8               ; set default ret code to "no answer"
	
	          waitrsp 1              ; see if phone is ringing
	
	          if (response = "2^M")  ; 2 is numeric form of "RING"
	              {
	              if (listen = 1)    ; see if Listen program is running or
	                  sendln "ATD"   ; not answer phone in originate mode
	                                 ;    (Listen)
	              else
	                  sendln "ATA"   ; answer the phone normally
	
	              waitrsp 120        ; wait up to 2 minutes for return code
	                                 ;    from modem
	
	              if (response = "1^M")
	                {
	                baud 300
	                display ">>> CONNECT 300 <<<"
	                $ret = 1
	                }
	              else if (response = "3^M")
	                {
	                display ">>> NO CARRIER <<<"
	                $ret = 8             ; no answer or no connect
	                }
	              else if (response = "5^M")
	                {
	                baud 1200
	                display ">>> CONNECT 1200 <<<"
	                $ret = 5
	                }
	              else if (response = "10^M")
	                {
	                baud 2400
	                display ">>> CONNECT 2400 <<<"
	                $ret = 10
	                }
	              }
	
	          return $ret            ; return connect baud rate to
	                                 ;    application
	
	  DISCONNECT:
	          wait 2                 ; wait 2 seconds
	
	          send "+++"             ; send escape sequence to put modem
	                                 ;    back to command state
	          wait 2                 ; wait 2 seconds
	
	          clearrsp               ; clear the response buffer
	
	          sendln "ATH0"          ; hang up the phone
	
	          waitrsp 1              ; wait for a response
	
	          if (response != "0^M") ; if hang up failed, drop DTR to force
	                                 ;    hang up
	              {
	              DTR 0              ; drop DTR to reset modem
	              wait 2             ; some modems require a delay here
	              DTR 1              ; raise DTR
	              clearrsp           ; clear response buffer
	              }
	
	          return 0               ; always return OK
	
	Additional query words: 2.10 2.1 2.10e
	
	======================================================================
	Keywords          :  
	Technology        : kbMailSearch kbZNotKeyword3 kbMailPCN210e
	Version           : WINDOWS:2.1e
	
	=============================================================================
	

{% endraw %}
