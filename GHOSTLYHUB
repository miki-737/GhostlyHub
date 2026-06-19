--// 👻 GHOSTLYHUB MENU (LOCKED NAME VERSION)
--// SOLO EDITABLE POR EL CREADOR

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer

------------------------------------------------
-- 🔒 CONFIG (SOLO EL CREADOR PUEDE EDITAR ESTO)
------------------------------------------------
local MENU_NAME = "GhostlyHub 👻" -- ❌ NO EDITABLE IN-GAME
local OPEN_KEY = Enum.KeyCode.F4

------------------------------------------------
-- STATES
------------------------------------------------
local flying = false
local noclip = false
local invisible = false
local flySpeed = 50

------------------------------------------------
-- REMOTE AUTO
------------------------------------------------
local remote = ReplicatedStorage:FindFirstChild("GhostlyHubRemote")
if not remote then
    remote = Instance.new("RemoteEvent")
    remote.Name = "GhostlyHubRemote"
    remote.Parent = ReplicatedStorage
end

------------------------------------------------
-- GUI
------------------------------------------------
local gui = Instance.new("ScreenGui")
gui.Name = "GhostlyHub"
gui.Parent = player:WaitForChild("PlayerGui")

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 420, 0, 320)
main.Position = UDim2.new(0.5, -210, 0.5, -160)
main.BackgroundColor3 = Color3.fromRGB(15,15,15)
main.Active = true
main.Draggable = true
main.Parent = gui

Instance.new("UICorner", main)

TweenService:Create(main, TweenInfo.new(0.3, Enum.EasingStyle.Back), {
    Size = main.Size
}):Play()

------------------------------------------------
-- 👻 LOGO TOGGLE (IMAGEN)
------------------------------------------------
local logo = Instance.new("ImageButton")
logo.Size = UDim2.new(0, 60, 0, 60)
logo.Position = UDim2.new(0, 10, 0, 10)

logo.Image = "rbxassetid://132405189693372"

logo.BackgroundColor3 = Color3.fromRGB(25,25,25)
logo.ScaleType = Enum.ScaleType.Fit
logo.Parent = gui

Instance.new("UICorner", logo)

logo.MouseButton1Click:Connect(function()
    main.Visible = not main.Visible
end)

------------------------------------------------
-- 🏷️ TITLE (NO SE PUEDE CAMBIAR EN JUEGO)
------------------------------------------------
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,0,0,40)
title.BackgroundTransparency = 1
title.Text = MENU_NAME
title.TextColor3 = Color3.fromRGB(180,0,255)
title.TextScaled = true
title.Parent = main

------------------------------------------------
-- BUTTON CREATOR
------------------------------------------------
local function button(text, y)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0, 180, 0, 30)
    b.Position = UDim2.new(0, 10, 0, y)
    b.Text = text
    b.BackgroundColor3 = Color3.fromRGB(30,30,30)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = main
    Instance.new("UICorner", b)

    b.MouseEnter:Connect(function()
        TweenService:Create(b, TweenInfo.new(0.1), {Size = UDim2.new(0,190,0,32)}):Play()
    end)

    b.MouseLeave:Connect(function()
        TweenService:Create(b, TweenInfo.new(0.1), {Size = UDim2.new(0,180,0,30)}):Play()
    end)

    return b
end

------------------------------------------------
-- 🎒 GIVE SYSTEM
------------------------------------------------
local giveBox = Instance.new("TextBox")
giveBox.Size = UDim2.new(0, 200, 0, 30)
giveBox.Position = UDim2.new(0, 210, 0, 60)
giveBox.PlaceholderText = "give espada 3"
giveBox.Parent = main
Instance.new("UICorner", giveBox)

local giveBtn = button("GIVE", 60)

giveBtn.MouseButton1Click:Connect(function()
    local args = string.split(giveBox.Text, " ")
    if args[1] == "give" then
        remote:FireServer("give", args[2], tonumber(args[3]) or 1)
    end
end)

------------------------------------------------
-- ✈️ FLY
------------------------------------------------
local flyBtn = button("FLY", 110)

local speedBox = Instance.new("TextBox")
speedBox.Size = UDim2.new(0, 200, 0, 30)
speedBox.Position = UDim2.new(0, 210, 0, 110)
speedBox.PlaceholderText = "velocidad 1-100"
speedBox.Parent = main
Instance.new("UICorner", speedBox)

flyBtn.MouseButton1Click:Connect(function()
    flying = not flying
end)

------------------------------------------------
-- 👁️ INVISIBLE
------------------------------------------------
local invisBtn = button("INVISIBLE", 150)

invisBtn.MouseButton1Click:Connect(function()
    invisible = not invisible
    local char = player.Character
    if not char then return end

    for _,v in pairs(char:GetDescendants()) do
        if v:IsA("BasePart") or v:IsA("Decal") then
            v.Transparency = invisible and 1 or 0
        end
    end
end)

------------------------------------------------
-- 🚪 NOCLIP
------------------------------------------------
local noclipBtn = button("NOCLIP", 190)

noclipBtn.MouseButton1Click:Connect(function()
    noclip = not noclip
end)

------------------------------------------------
-- 🔁 LOOP
------------------------------------------------
RunService.RenderStepped:Connect(function()
    local char = player.Character
    if not char then return end

    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end

    flySpeed = tonumber(speedBox.Text) or 50
    flySpeed = math.clamp(flySpeed, 1, 100)

    if flying then
        hrp.Velocity = workspace.CurrentCamera.CFrame.LookVector * flySpeed
    end

    if noclip then
        for _,v in pairs(char:GetDescendants()) do
            if v:IsA("BasePart") then
                v.CanCollide = false
            end
        end
    end
end)

------------------------------------------------
-- 🎮 OPEN KEY
------------------------------------------------
UIS.InputBegan:Connect(function(input)
    if input.KeyCode == OPEN_KEY then
        main.Visible = not main.Visible
    end
end)
