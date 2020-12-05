# Signature API requirement
Signature is the mail address available for the invite (FROM).
But due to the mail server constrain we can't have invalid email address which will block our mail server.
We also need to give option to send emails from special email ids like `STG_HR`.
So, before sending out from any email, they need to validate it through API.


## Data flow for this
- Signature creation from UI
- Signature data goes to backend
- Sends mail to that email address with OTP (Valid for 24 hours)
- From UI user enters the OTP and validate
- Will have option to choose from  owned email addresses

## Entity diagram (Tentative)
```jdl
entity Signature {
    email String required pattern(/^[^@\s]+@[^@\s]+\.[^@\s]+$/) 
    name String required
    replyEmail String pattern(/^[^@\s]+@[^@\s]+\.[^@\s]+$/) 
    replyName String
    status ValidationStatus
    createdBy User_ID(manyone relationship)
}
entity SignatureValidation {
	otp String
    createdtime ZonedDateTime
    validTill ZonedDateTime
    status ValidationStatus
    Signature_id (Oneto one)
}
enum ValidationStatus {
	VARIFIED, PENDING, REJECTED
}
```



