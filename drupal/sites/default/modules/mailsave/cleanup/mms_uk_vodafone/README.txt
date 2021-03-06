mms_uk_vodafone
---------------
This is a prototype module to try and clean up messages that are posted via
the MMS feature of a mobile phone. The emails generated this way typically
contain additional logos from the service provider, and possible additional
text.

hook_mailsave_clean is triggered by mailsave before it calls hook_mailsave.
You can therefore intercept the node and the email attachments before
other modules begin processing.

By implementing hook_mailsave_clean in a module you can therefore discard
additional images that are attached and modify the text of the node.

hook_mailsave_clean passes the node, but also information about the mailbox
and the email that is currently in use. In the case of vodafone an email
can be identified as originating from them as the sending email will be
<yourphonenumber>@mms.vodafone.co.uk. By looking for mms.vodafone.co.uk with
a regex we know we have a vodafone message.

Vodafone add a logo (vodafone.gif), lots of text, and assign a general
email title "You have received a new a message". The logo is discarded by
calling mailsave_discard_attachment(), and the spare text is rejected with
a regex. The title is adjusted to take the body text, trimmed to 60
characters.

; $Id: README.txt,v 1.1 2007/05/27 23:45:40 stuartgreenfield Exp $