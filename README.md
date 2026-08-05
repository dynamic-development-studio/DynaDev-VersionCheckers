# DynaDev Version Checkers

Welcome to the DynaDev Version Checkers repository. This repository hosts the latest version numbers for all DynaDev RedM scripts.

## How to Set Up

1. **Create a GitHub Repository**:
   - Create a public repository on GitHub named `DynaDev-VersionCheckers`.
   - Upload all `.txt` files from this directory to that repository.

    - Use the GitHub repository name in the script URL.

---

### Version Checker Code (Lua)

Add this snippet to the bottom of your resource's `server.lua`:

```lua
local scriptName = GetCurrentResourceName()
local currentVersion = GetResourceMetadata(scriptName, 'version', 0)

Citizen.CreateThread(function()
    Citizen.Wait(5000) -- Wait for the console to settle
    
    -- GitHub raw URL configuration
    local githubRawUrl = "https://raw.githubusercontent.com/dynamic-development-studio/DynaDev-VersionCheckers/main/" .. scriptName .. ".txt"
    
    PerformHttpRequest(githubRawUrl, function(statusCode, responseText, headers)
        if statusCode == 200 then
            local latestVersion = responseText:gsub("%s+", "")
            if latestVersion ~= currentVersion then
                print("^1[DynaDev Update] ^0An update is available for ^5" .. scriptName .. "^0!")
                print("^1[DynaDev Update] ^0Current Version: ^1" .. currentVersion .. "^0 | Latest Version: ^2" .. latestVersion .. "^0")
                print("^1[DynaDev Update] ^0Please download the latest version from Tebex.")
            else
                print("^2[DynaDev] ^0" .. scriptName .. " is up to date (Version: " .. currentVersion .. ").")
            end
        else
            print("^3[DynaDev Warning] ^0Could not check version for " .. scriptName .. " (HTTP " .. tostring(statusCode) .. ")")
        end
    end, "GET", "", {})
end)
```

---

## Οδηγίες (Greek)

1. **Δημιουργία GitHub Repository**:
   - Δημιουργήστε ένα δημόσιο (public) repository στο GitHub με όνομα `DynaDev-VersionCheckers`.
   - Ανεβάστε όλα τα αρχεία `.txt` από αυτόν τον φάκελο στο repository.

    - Επικολλήστε τον στο τέλος του αρχείου `server.lua` ή σε ένα ξεχωριστό server script.
