# Automatic-Mail-with-Powershell
With this script you can easiely send automated Mails
# Path to the file containing email addresses
$emailfile = "<Path to your TXT file with email addresses>"

# Example of a list of accepted domains
$acceptedDomains = @("<Domain>")

# Sender information
$smtpServer = "<SMTP server>"
$smtpSubject = "Test Email"
$smtpBody = "This is a test email sent automatically."
$emailfrom = "<Sender email address>"

# Read email addresses from the file
$emailadressen = Get-Content -Path $emailfile

# Loop through each email address
foreach ($emailTo in $emailadressen) {
    # Extract the domain from the email address
    $domainTo = $emailTo.Split('@')[1]

    # Check if the domain is in the list of accepted domains
    if ($acceptedDomains -contains $domainTo) {
        try {
            # Send the email
            Send-MailMessage -From $emailfrom -To $emailTo -Subject $smtpSubject -Body $smtpBody -SmtpServer $smtpServer -UseSsl

            # Output message after sending
            Write-Host "Email successfully sent to: $emailTo"
        }
        catch {
            Write-Host "Error sending email to: $emailTo. Error: $_"
        }
    } else {
        Write-Host "Invalid domain for email address: $emailTo"
    }
}
