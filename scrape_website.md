Someone from a discord chat asked if someone can get information from a website with a public directory

```powershell
$r1 = Invoke-WebRequest -Uri "https://associationdatabase.com/aws/MIA/pt/sp/public_members_directory" -Method Get

# Extract the action URL for the form
$formAction = $r1.Forms[0].Action

# If the form action is a relative path, concatenate with the base URI
if (-not [Uri]::IsWellFormedUriString($formAction, [UriKind]::Absolute)) {
    write-host "Relative path detected"
    $formAction = [Uri]::new($r1.BaseResponse.ResponseUri, $formAction).AbsoluteUri
} else {
    write-host "Absolute path detected"
}

# POST request with the form data
$response = Invoke-WebRequest -Uri $formAction -Method Post -Body $formFields -WebSession $r1.Session

# The resulting HTML is stored in $response
$directoryhtml = $response.Content

# Export to html file
$directoryhtml | Out-File -FilePath "C:\temp\directory.html"
```

```python

```

```powershell
# import the json file and convert to pscustomobjects
$stonejson = gc .\directoryoutfile.json | ConvertFrom-Json
$stonejson
```

