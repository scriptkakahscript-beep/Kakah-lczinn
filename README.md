-- LocalScript - Kakah Hub com abertura automática após introdução

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Tela de introdução
local introFrame = Instance.new("Frame")
introFrame.Size = UDim2.new(1, 0, 1, 0)
introFrame.Position = UDim2.new(0, 0, 0, 0)
introFrame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
introFrame.Parent = screenGui

local introText = Instance.new("TextLabel")
introText.Size = UDim2.new(1, 0, 1, 0)
introText.BackgroundTransparency = 1
introText.Text = "Seja bem-vindo ao Kakah Hub"
introText.TextColor3 = Color3.fromRGB(255, 255, 255)
introText.TextScaled = true
introText.Font = Enum.Font.SourceSansBold
introText.Parent = introFrame

-- Ícone do Hub
local hubIcon = Instance.new("TextButton")
hubIcon.Size = UDim2.new(0, 50, 0, 50)
hubIcon.Position = UDim2.new(0, 20, 0, 20)
hubIcon.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
hubIcon.Text = "☰"
hubIcon.TextColor3 = Color3.fromRGB(255, 255, 255)
hubIcon.Font = Enum.Font.SourceSansBold
hubIcon.TextScaled = true
hubIcon.Parent = screenGui

-- Painel do Hub
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 900, 0, 500)
frame.Position = UDim2.new(0.5, -450, 0.25, 0)
frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
frame.Active = true
frame.Draggable = true
frame.Visible = false -- começa fechado
frame.Parent = screenGui

Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 12)
local UIStroke = Instance.new("UIStroke", frame)
UIStroke.Thickness = 2
UIStroke.Color = Color3.fromRGB(255, 255, 255)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -50, 0, 40)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "🔥 Kakah Hub"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.Parent = frame

local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 40, 0, 40)
closeButton.Position = UDim2.new(1, -45, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Text = "X"
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextScaled = true
closeButton.Parent = frame

closeButton.MouseButton1Click:Connect(function()
    frame.Visible = false
end)

local contentLabel = Instance.new("TextLabel")
contentLabel.Size = UDim2.new(1, -20, 0, 40)
contentLabel.Position = UDim2.new(0, 10, 0, 50)
contentLabel.BackgroundTransparency = 1
contentLabel.Text = "Bem-vindo ao Kakah Hub!"
contentLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
contentLabel.TextScaled = true
contentLabel.TextWrapped = true
contentLabel.Font = Enum.Font.SourceSansBold
contentLabel.Parent = frame

-- Lista dinâmica de criadores
local creators = {"Kakah", "ajuntantes lczin", "Ninja", "Lolyta"}

local creatorsLabel = Instance.new("TextLabel")
creatorsLabel.Size = UDim2.new(1, -20, 0, 120)
creatorsLabel.Position = UDim2.new(0, 10, 0, 100)
creatorsLabel.BackgroundTransparency = 1
creatorsLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
creatorsLabel.TextScaled = true
creatorsLabel.TextWrapped = true
creatorsLabel.Font = Enum.Font.SourceSans
creatorsLabel.TextYAlignment = Enum.TextYAlignment.Top
creatorsLabel.Parent = frame

-- Monta o texto automaticamente
local text = "👑 Criadores:\n"
for _, name in ipairs(creators) do
    text = text .. name .. "\n"
end
creatorsLabel.Text = text

-- Função do ícone
hubIcon.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)

-- Depois de 7 segundos, remove a tela de introdução e abre o Hub automaticamente
delay(7, function()
    introFrame:Destroy()
    frame.Visible = true
end)
