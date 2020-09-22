<div align="center">

## Print hexpackets with WinSock


</div>

### Description

This is a simple example of converting a string data into a hex formatted (packet) view.

This will be mostly usefull when sending and receiving data with/through WinSock!

Packet displays data in hex and 'readable' characters like the packet below,

which seems to be the text you're reading right at this time!

48 65 6C 6C 6F 2C 0D 0A 0D 0A 54 68 69 73 20 69   Hello,....This.i

73 20 61 6E 20 65 78 61 6D 70 6C 65 20 6F 66 20   s.an.example.of.

63 6F 6E 76 65 72 74 69 6E 67 20 61 20 73 74 72   converting.a.str

69 6E 67 20 64 61 74 61 20 69 6E 74 6F 20 61 20   ing.data.into.a.

68 65 78 20 66 6F 72 6D 61 74 74 65 64 20 28 70   hex.formatted.(p

61 63 6B 65 74 29 20 76 69 65 77 2E 0D 0A 54 68   acket).view...Th

69 73 20 77 69 6C 6C 20 62 65 20 6D 6F 73 74 6C   is.will.be.mostl

79 20 75 73 65 66 75 6C 6C 20 77 68 65 6E 20 73   y.usefull.when.s

65 6E 64 69 6E 67 20 61 6E 64 20 72 65 63 65 69   ending.and.recei

76 69 6E 67 20 64 61 74 61 20 77 69 74 68 2F 74   ving.data.with/t

68 72 6F 75 67 68 20 57 69 6E 53 6F 63 6B 21 0D   hrough.WinSock!.

0A 0D 0A 50 61 63 6B 65 74 20 64 69 73 70 6C 61   ...Packet.displa

79 73 20 64 61 74 61 20 69 6E 20 68 65 78 20 61   ys.data.in.hex.a

6E 64 20 27 72 65 61 64 61 62 6C 65 27 20 63 68   nd.'readable'.ch

61 72 61 63 74 65 72 73 20 6C 69 6B 65 20 74 68   aracters.like.th

65 20 70 61 63 6B 65 74 20 62 65 6C 6F 77 2C 0D   e.packet.below,.

0A 77 68 69 63 68 20 73 65 65 6D 73 20 74 6F 20   .which.seems.to.

62 65 20 74 68 65 20 74 65 78 74 20 79 6F 75 27   be.the.text.you'

72 65 20 72 65 61 64 69 6E 67 20 72 69 67 68 74   re.reading.right

20 61 74 20 74 68 69 73 20 74 69 6D 65 21      .at.this.time!
 
### More Info
 
data string (i.e.: data from WinSock (vbString))

usefull for beginners

data in Hexpacket format


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[\~:\. Jeff 'Capes' \.:\~](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jeff-capes.md)
**Level**          |Beginner
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |VB 4\.0 \(32\-bit\), VB 5\.0, VB 6\.0
**Category**       |[String Manipulation](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/string-manipulation__1-5.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jeff-capes-print-hexpackets-with-winsock__1-38285/archive/master.zip)





### Source Code

```
Public Function PrintPacket(ByVal Packet As String) As String
' input   : data string (i.e.: data from WinSock (vbString))
' output  : data in Hexpacket format [best formatted in "Courier New"]
On Error GoTo dspErr
 Dim tHex As String, tmpHex As String, _
   tChr As Integer, tmpASCII As String, _
   HexLine As String, i As Long
    For i = 1 To Len(Packet)
      tHex = Hex(Asc(Mid(Packet, i, 1)))
      tHex = String((2 - Len(tHex)), "0") & tHex
      tmpHex = tmpHex & tHex
        tChr = Asc(Mid(Packet, i, 1))
        If tChr > 126 Or tChr < 33 Then
          tmpASCII = tmpASCII & "."
        Else
          tmpASCII = tmpASCII & Mid(Packet, i, 1)
        End If
        If Len(tmpHex) = 47 Then
          HexLine = HexLine & tmpHex & Space(5) & tmpASCII & vbCrLf
          tmpHex = ""
          tmpASCII = ""
        Else
          tmpHex = tmpHex & " "
        End If
        If i >= Len(Packet) Then
          HexLine = HexLine & tmpHex & String((47 - Len(tmpHex)), " ") & Space(5) & tmpASCII & vbCrLf
        End If
      DoEvents
    Next i
  PrintPacket = HexLine
  Exit Function
dspErr:
MsgBox "Error while converting string to packet", vbCritical, "PrintPacket error"
End Function
```

