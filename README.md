-- LocalScript - Kakah Hub com abas internas e FunPage grande

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Tela de introdução
local introFrame = Instance.new("Frame")
introFrame.Size = UDim2.new(1,0,1,0)
introFrame.Position = UDim2.new(0,0,0,0)
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

-- Painel principal do Hub
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
