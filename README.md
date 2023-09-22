# Checkpoint2

Exercice 1 : Script Powershell
###
Import-Module ActiveDirectory

$PasswordInit = Function Random-Password {
    param (
        [int]$Length = 8
    )

    $Characters = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+"
    $Password = -join (Get-Random -InputObject $Characters -Count $Length)

    return $Password
}

###
$File = "C:\Users\Administrateur\Documents\Checkpoint\users.cvs"
$FileCsv = Import-Csv -Path $File -Delimiter ";" -Header "prenom", "nom", "societe", "fonction", "service", "description", "mail", "mobile", "scriptPath", "telephoneNumber" -Encoding UTF7

###
$A






Exercice 2 : Réseaux et domaine

renommer la machine Client1
![image](https://github.com/JuJuIHM/Checkpoint2/assets/137881830/db869974-4d5c-4ec1-bf1e-2aed926b8789)

