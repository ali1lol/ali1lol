local attackersRecoilPreset = {
--Attack
 
{strength = 8, horizontalStrength = 1, description = "Sledge"},
{strength = 10, horizontalStrength = 0, description = "Thatcher L85A2"},
{strength = 13, horizontalStrength = 0, description = "Thatcher AR33"},
{strength = 10, horizontalStrength = 0, description = "Ash"},
{strength = 10, horizontalStrength = 1, description = "Thermite"},
{strength = 20, horizontalStrength = 0, description = "Twitch"},
{strength = 15, horizontalStrength = -1, description = "Fuze AK-12"},
{strength = 20, horizontalStrength = -1, description = "Fuze 6P41"},
{strength = 18, horizontalStrength = 0, description = "IQ AUG"},
{strength = 7, horizontalStrength = 0, description = "IQ 556"},
{strength = 7, horizontalStrength = -1, description = "IQ G8A1"},
--{strength = 0, horizontalStrength = 0, description = "Buck"},
--{strength = 0, horizontalStrength = 0, description = "Blackbeard"},
--{strength = 0, horizontalStrength = 0, description = "Capitao"},
{strength = 16, horizontalStrength = -1, description = "Hibana"},
--{strength = 0, horizontalStrength = 0, description = "Jackal"},
--{strength = 0, horizontalStrength = 0, description = "Ying"},
--{strength = 0, horizontalStrength = 0, description = "Zofia"},
{strength = 13, horizontalStrength = 0, description = "Lion"},
--{strength = 0, horizontalStrength = 0, description = "Finka"},
--{strength = 0, horizontalStrength = 0, description = "Maverick"},
{strength = 13, horizontalStrength = -1, description = "Nomad AK-74M"},
{strength = 11, horizontalStrength = -1, description = "Nomad ARX200"},
--{strength = 0, horizontalStrength = 0, description = "Gridlock"},
{strength = 8, horizontalStrength = 0, description = "Nokk"},
{strength = 18, horizontalStrength = -1, description = "Amaru"},
--{strength = 0, horizontalStrength = 0, description = "Kali"},
{strength = 5, horizontalStrength = -1, description = "Iana ARX200"},
{strength = 9, horizontalStrength = 0, description = "Iana G36C"},
{strength = 12, horizontalStrength = -1, description = "Ace"},
--{strength = 0, horizontalStrength = 0, description = "Zero"},
--{strength = 0, horizontalStrength = 0, description = "Flores"},
--{strength = 0, horizontalStrength = 0, description = "Osa"},
--{strength = 0, horizontalStrength = 0, description = "Sens"},
--{strength = 0, horizontalStrength = 0, description = "Grim"},
--{strength = 0, horizontalStrength = 0, description = "Brava"},
--{strength = 0, horizontalStrength = 0, description = "Ram"}
}
local defendersRecoilPreset = {
--Defence 
 
{strength = 11, horizontalStrength = 0, description = "Smoke"},
{strength = 7, horizontalStrength = 0, description = "Mute"},
{strength = 6, horizontalStrength = 0, description = "Castle"},
{strength = 6, horizontalStrength = 0, description = "Pulse"},
{strength = 11, horizontalStrength = 0, description = "Doc & Rook MP5"},
{strength = 13, horizontalStrength = 0, description = "Doc & Rook P90"},
{strength = 6, horizontalStrength = 0, description = "Kapkan"},
{strength = 13, horizontalStrength = 0, description = "Tachanka 9x19VSN"},
{strength = 3, horizontalStrength = 0, description = "Tachanka DP27"},
{strength = 7, horizontalStrength = 0, description = "Jager"},
{strength = 8, horizontalStrength = 0, description = "Bandit"},
{strength = 6, horizontalStrength = 0, description = "Frost"},
--{strength = 0, horizontalStrength = 0, description = "Valkyrie"},
{strength = 4, horizontalStrength = 0, description = "Caveira"},
--{strength = 0, horizontalStrength = 0, description = "Echo"},
--{strength = 0, horizontalStrength = 0, description = "Mira"},
{strength = 7, horizontalStrength = 0, description = "Lesion"},
{strength = 9, horizontalStrength = 1, description = "Ela"},
{strength = 6, horizontalStrength = 0, description = "Vigil"},
--{strength = 0, horizontalStrength = 0, description = "Maestro"},
--{strength = 0, horizontalStrength = 0, description = "Alibi"},
--{strength = 0, horizontalStrength = 0, description = "Clash"},
--{strength = 0, horizontalStrength = 0, description = "Kaid"},
--{strength = 0, horizontalStrength = 0, description = "Mozzie"},
--{strength = 0, horizontalStrength = 0, description = "Warden"},
--{strength = 0, horizontalStrength = 0, description = "Goyo"},
--{strength = 0, horizontalStrength = 0, description = "Wamai"},
--{strength = 0, horizontalStrength = 0, description = "Oryx"},
--{strength = 0, horizontalStrength = 0, description = "Melusi"},
{strength = 7, horizontalStrength = 0, description = "Aruni"},
--{strength = 0, horizontalStrength = 0, description = "Thunderbird"},
--{strength = 0, horizontalStrength = 0, description = "Thorn"},
--{strength = 0, horizontalStrength = 0, description = "Azami"},
--{strength = 0, horizontalStrength = 0, description = "Solis"},
{strength = 8, horizontalStrength = 0, description = "Fenrir"},
 
}
 
local selectedPresetIndex = 1
local selectedAttackerIndex = 1  -- Initialize the selected attacker index
local selectedDefenderIndex = 1  -- Initialize the selected defender index
local presetLocked = false
local selectedCategory = attackersRecoilPreset -- Start with attackers by default
local noRecoilEnabled = false
local isADSEnabled = true
local noDebugEnabled = true
 
 
function ApplyRecoil()
    if presetLocked then
        local recoil = selectedCategory[selectedPresetIndex]
        repeat
            MoveMouseRelative(recoil.horizontalStrength, recoil.strength)
            Sleep(14)
        until not IsMouseButtonPressed(1)
    end
end
function ToggleRecoil()
    noRecoilEnabled = not noRecoilEnabled
    UpdateLiveMenu()  -- Update the live menu
end
 
 
 
function TogglePresetLock()
    presetLocked = not presetLocked
     UpdateLiveMenu()  -- Update the live menu
end
 
function ToggleNoDebug()
    noDebugEnabled = not noDebugEnabled
    local status = noDebugEnabled and "[+] No Debug is ON" or "[-] No Debug is OFF"
    OutputLogMessage("%s\n", status)
end
 
-- Function to select the next preset for the current category (attackers or defenders)
function SelectNextPreset()
    if not presetLocked then
        if selectedCategory == attackersRecoilPreset then
            selectedAttackerIndex = (selectedAttackerIndex % #selectedCategory) + 1
            selectedPresetIndex = selectedAttackerIndex
        else
            selectedDefenderIndex = (selectedDefenderIndex % #selectedCategory) + 1
            selectedPresetIndex = selectedDefenderIndex
        end
        UpdateLiveMenu()  -- Update the live menu
    end
end
 
-- Function to select the previous preset for the current category (attackers or defenders)
function SelectPreviousPreset()
    if not presetLocked then
        if selectedCategory == attackersRecoilPreset then
            selectedAttackerIndex = selectedAttackerIndex - 1
            if selectedAttackerIndex < 1 then
                selectedAttackerIndex = #selectedCategory
            end
            selectedPresetIndex = selectedAttackerIndex
        else
            selectedDefenderIndex = selectedDefenderIndex - 1
            if selectedDefenderIndex < 1 then
                selectedDefenderIndex = #selectedCategory
            end
            selectedPresetIndex = selectedDefenderIndex
        end
        UpdateLiveMenu()  -- Update the live menu
    end
end
 
-- Function to toggle between attackers and defenders
function ToggleCategory()
    if not presetLocked then
        ClearLog()  -- Clear the log
 
        if selectedCategory == attackersRecoilPreset then
            selectedCategory = defendersRecoilPreset
            selectedPresetIndex = selectedDefenderIndex  -- Switch to the last selected defender index
        else
            selectedCategory = attackersRecoilPreset
            selectedPresetIndex = selectedAttackerIndex  -- Switch to the last selected attacker index
        end
        UpdateLiveMenu()  -- Update the live menu
    end
end
function OnEvent(event, arg)
    if (not noDebugEnabled) then
        OutputLogMessage("event = %s, arg = %s\n", event, arg)
    end
 
    if (event == "PROFILE_ACTIVATED") then
        EnablePrimaryMouseButtonEvents(true)
    end
 
   
 
    if (event == "MOUSE_BUTTON_PRESSED" and arg == 11) then
        TogglePresetLock()
    end
 
    if (event == "MOUSE_BUTTON_PRESSED") then
        if (arg == 10) then
            ToggleRecoil()
        elseif (arg == 8) then
            SelectPreviousPreset()
        elseif (arg == 7) then
            SelectNextPreset()
              elseif (arg == 9) then
            ToggleCategory()   -- Handle button 9 to switch between attackers and defenders
        end
    end
 
    if isADSEnabled then
        if (noRecoilEnabled and event == "MOUSE_BUTTON_PRESSED" and arg == 1 and IsMouseButtonPressed(3)) then
            ApplyRecoil()
        end
    else
        if (noRecoilEnabled and event == "MOUSE_BUTTON_PRESSED" and arg == 1) then
            ApplyRecoil()
        end
    end
 
   
   end
-- Function to update and display the live menu
 
-- Call the UpdateLiveMenu function initially to display the live menu
 
function UpdateLiveMenu()
 
 
   ClearLog()  -- Clear the log
    
    local recoilStatus = noRecoilEnabled and "[+] No Recoil is ON" or "[-] No Recoil is OFF"
    local presetLockStatus = presetLocked and "[+] Preset is locked" or "[-] Preset is unlocked"
    local separator = "====================================================================================="
    local logo = 
    [[ 
 ______     __     __    __     __  __     __         ______     __   __     ______  
/\  ___\   /\ \   /\ "-./  \   /\ \/\ \   /\ \       /\  __ \   /\ "-.\ \   /\__  _\ 
\ \___  \  \ \ \  \ \ \-./\ \  \ \ \_\ \  \ \ \____  \ \  __ \  \ \ \-.  \  \/_/\ \/ 
 \/\_____\  \ \_\  \ \_\ \ \_\  \ \_____\  \ \_____\  \ \_\ \_\  \ \_\\"\_\    \ \_\ 
  \/_____/   \/_/   \/_/  \/_/   \/_____/   \/_____/   \/_/\/_/   \/_/ \/_/     \/_/                            
    ]]
 
    local debugText = noDebugEnabled and "" or "DEBUG MODE"
    local selectedCategoryStatus = selectedCategory == attackersRecoilPreset and "Attackers" or "Defenders"
    local selectedPresetDescription = selectedCategory[selectedPresetIndex].description
    
    local outputText = logo .. "\n" .. separator
    outputText = outputText .. "\n " .. "                                    V1.3:R6 " .. debugText .. "\n"  -- Add "DEBUG" based on noDebugEnabled
    outputText = outputText .. "[Button 10] " .. recoilStatus .. "\n"
    outputText = outputText .. "[Button 11] " .. presetLockStatus .. "\n"
    outputText = outputText .. "[Button 9] Operator Type: " .. selectedCategoryStatus .. "\n"
    outputText = outputText .. "[Button 7 & 8 ] Selected Operator: " .. selectedPresetDescription .. "\n" .. separator .. "\n"
    
    OutputLogMessage(outputText)
    
 
end
