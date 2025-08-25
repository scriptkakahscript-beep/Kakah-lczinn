--// LocalScript - Kakah Hub com tela de introdução em imagem e ícone de abrir/fechar

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criação do ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.IgnoreGuiInset = true
screenGui.Parent = playerGui

-- ======================
-- Tela de introdução com imagem
-- ======================
local introImage = Instance.new("ImageLabel")
introImage.Size = UDim2.new(1, 0, 1, 0) -- cobre toda a tela
introImage.Position = UDim2.new(0, 0, 0, 0)
introImage.BackgroundTransparency = 1
introImage.Image = "126845736505633" -- coloque o Asset ID da imagem
introImage.ZIndex = 10
introImage.Parent = screenGui

local introText = Instance.new("TextLabel")
introText.Size = UDim2.new(1, 0, 1, 0)
introText.Position = UDim2.new(0, 0, 0, 0)
introText.BackgroundTransparency = 1
introText.Text = "Seja bem-vindo ao Kakah Hub"
introText.TextColor3 = Color3.fromRGB(255, 255, 255)
introText.TextScaled = true
introText.Font = Enum.Font.SourceSansBold
introText.ZIndex = 11
introText.Parent = introImage

-- ======================
-- Painel principal do Hub
-- ======================
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 900, 0, 500)
frame.Position = UDim2.new(0.5, -450, 0.25, 0)
frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
frame.Active = true
frame.Draggable = true
frame.Visible = false -- começa invisível, será mostrado após introdução
frame.ZIndex = 5
frame.Parent = screenGui

-- Estilo do Hub
local UICorner = Instance.new("UICorner", frame)
UICorner.CornerRadius = UDim.new(0, 12)

local UIStroke = Instance.new("UIStroke", frame)
UIStroke.Thickness = 2
UIStroke.Color = Color3.fromRGB(255, 255, 255)

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -50, 0, 40)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "🔥 Kakah Hub"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.ZIndex = 12
title.Parent = frame

-- Botão interno de fechar
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 40, 0, 40)
closeButton.Position = UDim2.new(1, -45, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Text = "X"
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextScaled = true
closeButton.ZIndex = 13
closeButton.Parent = frame

closeButton.MouseButton1Click:Connect(function()
    frame.Visible = false
end)

-- Texto de boas-vindas dentro do hub
local contentLabel = Instance.new("TextLabel")
contentLabel.Size = UDim2.new(1, -20, 0, 40)
contentLabel.Position = UDim2.new(0, 10, 0, 50)
contentLabel.BackgroundTransparency = 1
contentLabel.Text = "Bem-vindo ao Kakah Hub!"
contentLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
contentLabel.TextScaled = true
contentLabel.TextWrapped = true
contentLabel.ZIndex = 12
contentLabel.Parent = frame

-- ======================
-- Ícone para abrir/fechar hub
-- ======================
local hubIcon = Instance.new("TextButton")
hubIcon.Size = UDim2.new(0, 50, 0, 50)
hubIcon.Position = UDim2.new(0, 20, 0, 20)
hubIcon.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
hubIcon.Text = "☰"
hubIcon.TextColor3 = Color3.fromRGB(255, 255, 255)
hubIcon.Font = Enum.Font.SourceSansBold
hubIcon.TextScaled = true
hubIcon.ZIndex = 14
hubIcon.Parent = screenGui

hubIcon.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)

-- ======================
-- Remove a tela de introdução após 7 segundos e mostra o hub
-- ======================
task.delay(7, function()
    if introImage then
        introImage:Destroy()
    end
    frame.Visible = true -- abre o hub automaticamente
end)
