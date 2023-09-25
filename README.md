# Checkpoint2

Exercice 1 : Script Powershell
###
Import-Module ActiveDirectory

$PasswordInit = Function New-RandomPassword {
    [CmdletBinding()]
    param 
    (
        [Parameter(Mandatory=$true)][int]$Length,
        [Parameter(Mandatory=$false)][int]$Uppercase=1,
        [Parameter(Mandatory=$false)][int]$Digits=1,
        [Parameter(Mandatory=$false)][int]$SpecialCharacters=1,
    )
}

Begin {
        $Lowercase = $Length - $SpecialCharacters - $Uppercase - $Digits
        $ArrayUpperCharacters = @('A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z')
        $ArrayLowerCharacters = @('a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z')
$ArraySpecialCharacters = @('!','@','#','$','%','^','&','*','(',')','_','+')
}

Process {
        [string]$NewPassword = $ArrayLowerCharacters | Get-Radom -Count $Lowercase
        $NewPassword += 0..9 | Get-Random -Count $Digits
        $NewPassword += $ArrayUpperCharacters | Get-Random -Count $Uppercase
        $NewPassword += $ArraySpecialCharacters | Get-Random -Count $SpecialCharacters

$NewPassword = $NewPassword.Replace(' ','')

$charactersArray = $NewPassword.ToCharArray()
$scrambledStringArray = $characterArray | Get Random -Count $charactersArray.Length
$NewRandomPassword = -join $scrambleStringArray
}

End {
        Return $NewRandomPassword
    }
}

$NouveauMotDePasse = New-RandomPassword -Length 14 -Uppercase 3 -Digits 4 -SpecialCharacters 4

###
$File = "C:\Users\Administrateur\Documents\Checkpoint\users.cvs"
$FileCsv = Import-Csv 
-Path $File -Delimiter ";" -Header "prenom", "nom", "societe", "fonction", "service", "description", "mail", "mobile", "scriptPath", "telephoneNumber" -Encoding UTF7

###
$ADUsers = Get-AdUser -Filter * -Properties SamAccountName

Foreach (User in $FileCsv)
{
    $SamAccountName = "$(User.prenom) , $($User.nom)"
    $ResCheckADUsers | Where {$_.SamAccountName -eq $SamAccountName}
    If ($ResCheckADUser -eq $null)
    {
        ###
        Write-Host "Compte $SamAccountName à Crée"

        ###
        $Password = $NouveauMotDePasse
        $Email = "à faire plus tard"
        $MobilePhone = $User.telephoneNumber
        $Title = $User.fonction
        $Department = $User.service
        $Description = $User.description
        $ScriptPath = $User.scriptPath
        $UserPrincipalName = "$SamAccountName@sweetcakes.net"
        $Name= "$($User.prenom) $(User.nom)"
        $OfficePhone = $User.mobile
        $GivenName = $User.prenom
        $Surname = $User.nom
        $DisplayName = $SamAccountName
        $Path = "OU=$($User.service) ,OU=Utilisateurs,DC=Sweetcakes,DC=net"
        $Company = $User.societe

        ###
        New-ADUser
            -SamAccountName $SamAccountName `
            -UserPrincipalName $UserPrincipalName `
            -Name $Name `
            -GivenName $GivenName `
            -Surname $Surname `
            -Enabled $True `
            -DisplayName $DisplayName `
            -Path $Path `
            -Company $Company `
            -OfficePhone $OfficePhone `
            -MobilePhone $MobilePhone `
            -Title $Title `
            -Department $Department `
            -AccountPassword $AccountPassword `
            -ChangePasswordAtLogon $True `
            -Description $User.description `
            -ScriptPath $ScripthPath `

    Write-Host "Le compte $Name a été crée `nLe mot de passe est $Password"
    }
    Else
    {
        ###
        Write-Host "Le compte $Name est déjà crée"
    }
}


Exercice 2 : Réseaux et domaine

renommer la machine Client1
![image](https://github.com/JuJuIHM/Checkpoint2/assets/137881830/db869974-4d5c-4ec1-bf1e-2aed926b8789)

