local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()
local Window = Rayfield:CreateWindow({
    Name = "Rayfield Example Window",
    LoadingTitle = "Rayfield Interface Suite",
    LoadingSubtitle = "by Sirius",
    ConfigurationSaving = {
       Enabled = true,
       FolderName = nil, -- Create a custom folder for your hub/game
       FileName = "Big Hub"
    },
})local Tab = Window:CreateTab("Tab Example", 4483362458) -- Title, Image
local Section = Tab:CreateSection("Section Example")
local Toggle = Tab:CreateToggle({
   Name = "Toggle Example",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(highlightAllPlayers)
   -- The function that takes place when the toggle is pressed
   -- The variable (Value) is a boolean on whether the toggle is true or false
   end,
   

})
local function highlightAllPlayers()
    for _, player in ipairs(Players:GetPlayers()) do
        local character = player.Character or player.CharacterAdded:Wait()
        if character then
            -- Create a Highlight object
            local highlight = Instance.new("Highlight")
            highlight.Parent = character
            highlight.Adornee = character
            highlight.FillColor = Color3.new(1, 1, 0) -- Yellow color
            highlight.FillTransparency = 0.5 -- Semi-transparent
            highlight.OutlineColor = Color3.new(0, 0, 0) -- Black outline
            highlight.OutlineTransparency = 0 -- Fully visible outline
            
            -- Optional: Remove the highlight after a duration
            wait(5) -- Highlight lasts for 5 seconds
            highlight:Destroy()
        end
    end
end
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local localPlayer = Players.LocalPlayer
local camera = workspace.CurrentCamera

local targetPlayer = nil

-- Function to get the closest player
local function getClosestPlayer()
    local closestPlayer = nil
    local closestDistance = math.huge

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= localPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local distance = (player.Character.HumanoidRootPart.Position - localPlayer.Character.HumanoidRootPart.Position).magnitude
            
            if distance < closestDistance then
                closestDistance = distance
                closestPlayer = player
            end
        end
    end

    return closestPlayer
end

-- Function to lock on to the target
local function lockOn()
    targetPlayer = getClosestPlayer()
    if targetPlayer then
        print("Locked on to: " .. targetPlayer.Name)
        -- Optional: You can add visual feedback here (like a GUI or highlight)
    else
        print("No player to lock on to.")
    end
end

-- Function to reset the lock-on
local function resetLockOn()
    targetPlayer = nil
    print("Lock-on reset.")
end

-- Input handling
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed then
        if input.KeyCode == Enum.KeyCode.L then -- Press 'L' to lock on
            lockOn()
        elseif input.KeyCode == Enum.KeyCode.R then -- Press 'R' to reset lock-on
            resetLockOn()
        end
    end
end)

-- Optional: Update camera to follow the target
game:GetService("RunService").RenderStepped:Connect(function()
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        camera.CFrame = CFrame.new(camera.CFrame.Position, targetPlayer.Character.HumanoidRootPart.Position)
    end
end)
local Tab = Window:CreateTab("Tab Example", 4483362458) -- Title, Image
local Section = Tab:CreateSection("Section Example")
local Toggle = Tab:CreateToggle({
   Name = "Toggle Example",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(autoFarm)
   -- The function that takes place when the toggle is pressed
   -- The variable (Value) is a boolean on whether the toggle is true or false
   end,
   

})
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local waitTime = 1 -- Time to wait between actions

-- Function to simulate collecting resources
local function collectItems()
    local collectibles = workspace:GetChildren()
    local nearestCollectible = nil
    local closestDistance = math.huge

    for _, item in ipairs(collectibles) do
        if item:IsA("Part") and item.Name == "Collectible" then -- Adjust based on your collectible's name
            local distance = (item.Position - character.HumanoidRootPart.Position).magnitude
            if distance < closestDistance then
                closestDistance = distance
                nearestCollectible = item
            end
        end
    end
    
    if nearestCollectible then
        humanoid:MoveTo(nearestCollectible.Position)

        -- Wait until reached (simple version, consider using a better method)
        wait(1) -- Adjust this time as necessary to ensure player reaches it

        -- Simulate collecting (replace with your actual collection logic)
        print("Collected: " .. nearestCollectible.Name)
        nearestCollectible:Destroy() -- Or call your collect function
    end
end

-- Function to defeat the nearest enemy
local function defeatEnemies()
    local enemies = workspace:GetChildren()
    local nearestEnemy = nil
    local closestDistance = math.huge

    for _, enemy in ipairs(enemies) do
        if enemy:IsA("Model") and enemy:FindFirstChild("Humanoid") and enemy.Name == "Enemy" then -- Adjust based on your enemy's name
            local distance = (enemy.HumanoidRootPart.Position - character.HumanoidRootPart.Position).magnitude
            if distance < closestDistance then
                closestDistance = distance
                nearestEnemy = enemy
            end
        end
    end
    
    if nearestEnemy then
        humanoid:MoveTo(nearestEnemy.HumanoidRootPart.Position)

        -- Wait until reached
        wait(1) -- Adjust this time as necessary to ensure player reaches it

        -- Simulate attacking (replace this with your actual attack logic)
        print("Defeated: " .. nearestEnemy.Name)
        nearestEnemy:FindFirstChild("Humanoid"):TakeDamage(10) -- Example damage amount
    end
end

-- Main auto-farming function
local function autoFarm()
    while true do
        wait(waitTime) -- Wait before the next action

        -- Collect items
        collectItems()

        -- Defeat enemies
        defeatEnemies()
    end
end

-- Start the auto-farming process
autoFarm()
