-- [[ REDZ REPLICA - ESTÁVEL PARA DELTA ]] --

-- SEGURANÇA BÁSICA
if not game:IsLoaded() then game.Loaded:Wait() end
pcall(function()
    local mt = getrawmetatable(game)
    setreadonly(mt, false)
    local old = mt.__namecall
    mt.__namecall = newcclosure(function(self, ...)
        local method = getnamecallmethod()
        if method == "Kick" or method == "kick" then return nil end
        return old(self, ...)
    end)
    setreadonly(mt, true)
end)

-- INTERFACE ORION (MAIS LEVE QUE A KAVO)
local OrionLib = loadstring(game:HttpGet(('https://githubusercontent.com')))()
local Window = OrionLib:MakeWindow({Name = "REDz REPLICA - ULTIMATE", HidePremium = false, SaveConfig = true, ConfigFolder = "RedzConfig"})

-- ABA DE FARM
local FarmTab = Window:MakeTab({Name = "Auto Farm", Icon = "rbxassetid://4483345998", PremiumOnly = false})

FarmTab:AddToggle({
    Name = "Smart Fast Attack",
    Default = false,
    Callback = function(Value)
        _G.FastAttack = Value
        spawn(function()
            while _G.FastAttack do
                task.wait(0.05)
                pcall(function()
                    game:GetService("VirtualUser"):CaptureController()
                    game:GetService("VirtualUser"):ClickButtonLeft(Vector2.new(0, 0))
                end)
            end
        end)
    end    
})

FarmTab:AddToggle({
    Name = "Bring Mob (Puxar)",
    Default = false,
    Callback = function(Value)
        _G.BringMob = Value
        spawn(function()
            while _G.BringMob do
                task.wait(0.1)
                for _, v in pairs(game.Workspace.Enemies:GetChildren()) do
                    if v:FindFirstChild("HumanoidRootPart") then
                        v.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -7)
                        v.HumanoidRootPart.CanCollide = false
                    end
                end
            end
        end)
    end    
})

-- ABA DE STATUS
local StatTab = Window:MakeTab({Name = "Status", Icon = "rbxassetid://4483345998", PremiumOnly = false})

StatTab:AddToggle({
    Name = "Auto Stats (Melee)",
    Default = false,
    Callback = function(Value)
        _G.AutoStats = Value
        while _G.AutoStats do
            task.wait(1)
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Melee", 1)
        end
    end    
})

-- ABA DE TELEPORTES
local TpTab = Window:MakeTab({Name = "Teleportes", Icon = "rbxassetid://4483345998", PremiumOnly = false})

TpTab:AddButton({
    Name = "Teleport Blue Gear (Mirage)",
    Callback = function()
        for _, v in pairs(game.Workspace:GetDescendants()) do
            if v.Name == "Blue Gear" or v.Name == "Gear" then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame
            end
        end
    end    
})

TpTab:AddButton({
    Name = "Mansão (Sea 3)",
    Callback = function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-12463, 332, -7549)
    end    
})

OrionLib:Init()
