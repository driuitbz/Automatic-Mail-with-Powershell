
# Load the WPF-Assembly
Add-Type -AssemblyName "System.Windows.Forms"

# Create a GUI window:
$Form = New-Object System.Windows.Forms.Form
$Form.Text = 'E-Mail Address Input'
$Form.Size = New-Object System.Drawing.Size(600, 400)
$Form.StartPosition = 'CenterScreen'  # The window will always appear centered on the screen

# Create a label for the sender's email address:
$LabelFrom = New-Object System.Windows.Forms.Label
$LabelFrom.Text = 'Sender E-Mail Address:'
$LabelFrom.Location = New-Object System.Drawing.Point(10, 30)
$LabelFrom.Size = New-Object System.Drawing.Size(350, 30)
$LabelFrom.Font = New-Object System.Drawing.Font("Arial", 10)

# Create a text box for the sender's email address:
$TextBoxFrom = New-Object System.Windows.Forms.TextBox
$TextBoxFrom.Location = New-Object System.Drawing.Point(10, 60)
$TextBoxFrom.Size = New-Object System.Drawing.Size(350, 30)
$TextBoxFrom.Font = New-Object System.Drawing.Font("Arial", 20)

# Create a label for the recipient's email address:
$LabelTo = New-Object System.Windows.Forms.Label
$LabelTo.Text = 'Recipient E-Mail Address:'
$LabelTo.Location = New-Object System.Drawing.Point(10, 100)
$LabelTo.Size = New-Object System.Drawing.Size(350, 30)
$LabelTo.Font = New-Object System.Drawing.Font("Arial", 10)

# Create a text box for the recipient's email address:
$TextBoxTo = New-Object System.Windows.Forms.TextBox
$TextBoxTo.Location = New-Object System.Drawing.Point(10, 130)
$TextBoxTo.Size = New-Object System.Drawing.Size(350, 30)
$TextBoxTo.Font = New-Object System.Drawing.Font("Arial", 20)

# Create a button to send the email:
$Button = New-Object System.Windows.Forms.Button
$Button.Text = 'Send E-Mail'
$Button.Location = New-Object System.Drawing.Point(200, 220)
$Button.Size = New-Object System.Drawing.Size(200, 50)
$Button.Font = New-Object System.Drawing.Font("Arial", 10)
$Button.Add_Click({
    $emailFrom = $TextBoxFrom.Text
    $emailTo = $TextBoxTo.Text
    
  # Example list of accepted domains
    $acceptedDomains = @("<domain>")

  # Extract the domain from the recipient's email address
    $domainTo = $emailTo.Split('@')[1]

  # Check if the domain is in the list of accepted domains
    if ($acceptedDomains -contains $domainTo) {
        # Sending the email using Send-MailMessage
        $smtpServer = "<Your SMTP Server>"
        $smtpSubject = "<Subject that you wish>"
        $smtpBody = "<Content in the mail that you wish>"
        
  # Send the email
        Send-MailMessage -From $emailFrom -To $emailTo -Subject $smtpSubject -Body $smtpBody -SmtpServer $smtpServer

        # Display a success message
        [System.Windows.Forms.MessageBox]::Show("E-Mail was sent successfully.")
        $Form.Close()
    }
    else {
        [System.Windows.Forms.MessageBox]::Show("Invalid E-Mail Addresses.")
    }
})

# Add the components to the form
$Form.Controls.Add($LabelFrom)
$Form.Controls.Add($TextBoxFrom)
$Form.Controls.Add($LabelTo)
$Form.Controls.Add($TextBoxTo)
$Form.Controls.Add($Button)

# Display the form
$Form.ShowDialog() 
