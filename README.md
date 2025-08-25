-- LocalScript - Kakah Hub Completo com FunPage e AvatarPage

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local RunService = game:GetService("RunService")

-- ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Tela de introdução
local introFrame = Instance.new("Frame")
introFrame.Size = UDim2.new(1,0,1,0)
introFrame.BackgroundColor3 = Color3.fromRGB(255,0,0)
introFrame.Parent = screenGui

local introText = Instance.new("TextLabel")
introText.Size = UDim2.new(1,0,1,0)
introText.BackgroundTransparency = 1
introText.Text = "Seja bem-vindo ao Kakah Hub"
introText.TextColor3 = Color3.fromRGB(255,255,255)
introText.TextScaled = true
introText.Font = Enum.Font.SourceSansBold
introText.Parent = introFrame

-- Ícone do Hub
local hubIcon = Instance.new("TextButton")
hubIcon.Size = UDim2.new(0,50,0,50)
hubIcon.Position = UDim2.new(0,20,0,20)
hubIcon.BackgroundColor3 = Color3.fromRGB(0,0,0)
hubIcon.Text = "☰"
hubIcon.TextColor3 = Color3.fromRGB(255,255,255)
hubIcon.Font = Enum.Font.SourceSansBold
hubIcon.TextScaled = true
hubIcon.Parent = screenGui

-- Hub principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0,900,0,500)
frame.Position = UDim2.new(0.5,-450,0.25,0)
frame.BackgroundColor3 = Color3.fromRGB(255,0,0)
frame.Active = true
frame.Draggable = true
frame.Visible = false
frame.Parent = screenGui

Instance.new("UICorner", frame).CornerRadius = UDim.new(0,12)
local UIStroke = Instance.new("UIStroke", frame)
UIStroke.Thickness = 2
UIStroke.Color = Color3.fromRGB(255,255,255)

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,-50,0,40)
title.Position = UDim2.new(0,10,0,0)
title.BackgroundTransparency = 1
title.Text = "🔥 Kakah Hub"
title.TextColor3 = Color3.fromRGB(255,255,255)
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.Parent = frame

-- Botão fechar
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0,40,0,40)
closeButton.Position = UDim2.new(1,-45,0,5)
closeButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
closeButton.TextColor3 = Color3.fromRGB(255,255,255)
closeButton.Text = "X"
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextScaled = true
closeButton.Parent = frame

closeButton.MouseButton1Click:Connect(function()
    frame.Visible = false
end)

-- Lista de criadores
local creators = {"Kakah","ajuntantes lczin","Ninja","Lolyta"}
local creatorsLabel = Instance.new("TextLabel")
creatorsLabel.Size = UDim2.new(1,-20,0,120)
creatorsLabel.Position = UDim2.new(0,10,0,50)
creatorsLabel.BackgroundTransparency = 1
creatorsLabel.TextColor3 = Color3.fromRGB(255,255,255)
creatorsLabel.TextScaled = true
creatorsLabel.TextWrapped = true
creatorsLabel.Font = Enum.Font.SourceSans
creatorsLabel.TextYAlignment = Enum.TextYAlignment.Top
creatorsLabel.Parent = frame

local text = "👑 Criadores:\n"
for _,name in ipairs(creators) do
    text = text..name.."\n"
end
creatorsLabel.Text = text

-- Aba Fun
local funButton = Instance.new("TextButton")
funButton.Size = UDim2.new(0,100,0,40)
funButton.Position = UDim2.new(0,10,0,180)
funButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
funButton.TextColor3 = Color3.fromRGB(255,255,255)
funButton.Text = "Fun"
funButton.Font = Enum.Font.SourceSansBold
funButton.TextScaled = true
funButton.Parent = frame

-- FunPage (vermelha, tamanho quase todo o Hub)
local funPage = Instance.new("Frame")
funPage.Size = UDim2.new(1,-20,1,-50)
funPage.Position = UDim2.new(0,10,0,50)
funPage.BackgroundColor3 = Color3.fromRGB(255,0,0)
funPage.Visible = false
funPage.Parent = frame
Instance.new("UICorner", funPage).CornerRadius = UDim.new(0,10)

-- Botão Voltar FunPage
local backButton = Instance.new("TextButton")
backButton.Size = UDim2.new(0,100,0,40)
backButton.Position = UDim2.new(1,-120,0,10)
backButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
backButton.TextColor3 = Color3.fromRGB(255,255,255)
backButton.Text = "Voltar"
backButton.Font = Enum.Font.SourceSansBold
backButton.TextScaled = true
backButton.Parent = funPage

backButton.MouseButton1Click:Connect(function()
    funPage.Visible = false
end)

-- Botões Noclip e Speed na FunPage
local noclipButton = Instance.new("TextButton")
noclipButton.Size = UDim2.new(0,150,0,50)
noclipButton.Position = UDim2.new(0,20,0,70)
noclipButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
noclipButton.TextColor3 = Color3.fromRGB(255,255,255)
noclipButton.Text = "Noclip"
noclipButton.Font = Enum.Font.SourceSansBold
noclipButton.TextScaled = true
noclipButton.Parent = funPage

local speedButton = Instance.new("TextButton")
speedButton.Size = UDim2.new(0,150,0,50)
speedButton.Position = UDim2.new(0,200,0,70)
speedButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
speedButton.TextColor3 = Color3.fromRGB(255,255,255)
speedButton.Text = "Speed"
speedButton.Font = Enum.Font.SourceSansBold
speedButton.TextScaled = true
speedButton.Parent = funPage

-- Noclip toggle
local noclipEnabled = false
noclipButton.MouseButton1Click:Connect(function()
    noclipEnabled = not noclipEnabled
    noclipButton.Text = noclipEnabled and "Noclip ON" or "Noclip OFF"
end)

RunService.Stepped:Connect(function()
    if noclipEnabled and player.Character then
        for _,part in ipairs(player.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)

-- Speed toggle até 100
local speedValue = 50
speedButton.MouseButton1Click:Connect(function()
    speedValue = speedValue + 10
    if speedValue > 100 then speedValue = 16 end
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = speedValue
    end
    speedButton.Text = "Speed: "..speedValue
end)

-- Toggle FunPage
funButton.MouseButton1Click:Connect(function()
    funPage.Visible = not funPage.Visible
end)

-- ---------------------
-- Aba Avatar
-- ---------------------
local avatarButton = Instance.new("TextButton")
avatarButton.Size = UDim2.new(0,100,0,40)
avatarButton.Position = UDim2.new(0,10,0,230)
avatarButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
avatarButton.TextColor3 = Color3.fromRGB(255,255,255)
avatarButton.Text = "Avatar"
avatarButton.Font = Enum.Font.SourceSansBold
avatarButton.TextScaled = true
avatarButton.Parent = frame

-- AvatarPage
local avatarPage = Instance.new("Frame")
avatarPage.Size = UDim2.new(1,-20,1,-50)
avatarPage.Position = UDim2.new(0,10,0,50)
avatarPage.BackgroundColor3 = Color3.fromRGB(255,0,0)
avatarPage.Visible = false
avatarPage.Parent = frame
Instance.new("UICorner", avatarPage).CornerRadius = UDim.new(0,10)

-- Botão Voltar AvatarPage
local avatarBackButton = Instance.new("TextButton")
avatarBackButton.Size = UDim2.new(0,100,0,40)
avatarBackButton.Position = UDim2.new(1,-120,0,10)
avatarBackButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
avatarBackButton.TextColor3 = Color3.fromRGB(255,255,255)
avatarBackButton.Text = "Voltar"
avatarBackButton.Font = Enum.Font.SourceSansBold
avatarBackButton.TextScaled = true
avatarBackButton.Parent = avatarPage

avatarBackButton.MouseButton1Click:Connect(function()
    avatarPage.Visible = false
end)

-- Toggle AvatarPage
avatarButton.MouseButton1Click:Connect(function()
    avatarPage.Visible = not avatarPage.Visible
end)

-- Abrir Hub após introdução
delay(7,function()
    introFrame:Destroy()
    frame.Visible = true
end)

-- Abrir/fechar Hub pelo ícone
hubIcon.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)
