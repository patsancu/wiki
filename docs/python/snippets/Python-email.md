### Email
#### One way
```
#!/usr/bin/env python
import smtplib
import sys


GMAIL_SMTP_SERVER = "smtp.gmail.com"
GMAIL_SMTP_PORT = 587

GMAIL_EMAIL = "GMAIL_ADDRESS"
GMAIL_PASSWORD = "GMAIL_PW"


def initialize_smtp_server():
    '''
    This function initializes and greets the smtp server.
    It logs in using the provided credentials and returns
    the smtp server object as a result.
    '''
    smtpserver = smtplib.SMTP(GMAIL_SMTP_SERVER, GMAIL_SMTP_PORT)
    smtpserver.ehlo()
    smtpserver.starttls()
    smtpserver.ehlo()
    smtpserver.login(GMAIL_EMAIL, GMAIL_PASSWORD)
    return smtpserver


def send_thank_you_mail(email):
    to_email = email
    from_email = GMAIL_EMAIL
    subj = "Thanks for being an active commenter"
    # The header consists of the To and From and Subject lines
    # separated using a newline character
    header = "To:%s\nFrom:%s\nSubject:%s \n" % (to_email,
            from_email, subj)
    # Hard-coded templates are not best practice.
    msg_body = """
    Hi %s,
    Thank you very much for your repeated comments on our service.
    The interaction is much appreciated.
    Thank You.""" % email
    content = msg_body
    smtpserver = initialize_smtp_server()
    smtpserver.sendmail(from_email, to_email, content)
    smtpserver.close()


if __name__ == "__main__":
    # for every line of input.
    for email in sys.stdin.readlines():
            send_thank_you_mail(email)

```

#### or another, more CLI

```python
#!/usr/bin/env python
import smtplib
import sys

from optparse import OptionParser

def initialize_smtp_server(smtpserver, smtpport, email, pwd):
    '''
    This function initializes and greets the SMTP server.
    It logs in using the provided credentials and returns the
    SMTP server object as a result.
    '''
    smtpserver = smtplib.SMTP(smtpserver, smtpport)
    smtpserver.ehlo()
    smtpserver.starttls()
    smtpserver.ehlo()
    smtpserver.login(email, pwd)
    return smtpserver


def send_thank_you_mail(email, smtpserver):
    to_email = email
    from_email = GMAIL_EMAIL
    subj = "Thanks for being an active commenter"
    # The header consists of the To and From and Subject lines
    # separated using a newline character.
    header = "To:%s\nFrom:%s\nSubject:%s \n" % (to_email,
            from_email, subj)
    # Hard-coded templates are not best practice.
    msg_body = """
    Hi %s,
    Thank you very much for your repeated comments on our service.
    The interaction is much appreciated.
    Thank You.""" % email
    content = header + "\n" + msg_body
    smtpserver.sendmail(from_email, to_email, content)


if __name__ == "__main__":
    usage = "usage: %prog [options]"
    parser = OptionParser(usage=usage)
    parser.add_option("--email", dest="email",
            help="email to login to smtp server")
    parser.add_option("--pwd", dest="pwd",
            help="password to login to smtp server")
    parser.add_option("--smtp-server", dest="smtpserver",
            help="smtp server url", default="smtp.gmail.com")
    parser.add_option("--smtp-port", dest="smtpserverport",
            help="smtp server port", default=587)
    options, args = parser.parse_args()

    if not (options.email or options.pwd):
            parser.error("Must provide both an email and a password")

    smtpserver = initialize_smtp_server(options.stmpserver,
            options.smtpserverport, options.email, options.pwd)

    # for every line of input.
    for email in sys.stdin.readlines():
            send_thank_you_mail(email, smtpserver)
    smtpserver.close()

```
