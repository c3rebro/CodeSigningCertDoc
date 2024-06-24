
# CodeSigningCertDoc
How to create a SelfSigned Code Signing Certificate from PowerShell under Windows 10 / 11:

(Replace the variables to your needs)


    $params = @{
        Type = 'CodeSigning'
        Container = 'test*'
        Subject = 'CN=Your Name'
        TextExtension = @(
            '2.5.29.37={text}1.3.6.1.5.5.7.3.3',
            '2.5.29.17={text}upn=mail@example.com' )
        KeyUsage = 'DigitalSignature'
        KeySpec="Signature"
        KeyUsageProperty="Sign"
        Friendlyname="Your Company"
        KeyAlgorithm = 'RSA'
        KeyLength = 2048
        HashAlgorithm="SHA256"
        Provider="Microsoft Enhanced RSA and AES Cryptographic Provider"
        NotAfter = (Get-Date).AddMonths(120)
    }
    
    $selfSignedRootCA = New-SelfSignedCertificate @params 
    
    $CertPassword = ConvertTo-SecureString -String "YourPassword" -Force -AsPlainText
    $selfSignedRootCA | Export-PfxCertificate -FilePath C:\YourCert.pfx -Password $CertPassword
    

