local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criação do ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui
screenGui.IgnoreGuiInset = true -- garante que fique no topo

-- ======================
-- Tela de introdução
-- ======================
local introFrame = Instance.new("Frame")
introFrame.Size = UDim2.new(1, 0, 1, 0)
introFrame.Position = UDim2.new(0, 0, 0, 0)
introFrame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
introFrame.ZIndex = 10 -- fica acima de tudo
introFrame.Parent = screenGui

local introText = Instance.new("TextLabel")
introText.Size = UDim2.new(1, 0, 1, 0)
introText.Position = UDim2.new(0, 0, 0, 0)
introText.BackgroundTransparency = 1
introText.Text = "Seja bem-vindo ao Kakah Hub"
introText.TextColor3 = Color3.fromRGB(255, 255, 255)
introText.TextScaled = true
introText.Font = Enum.Font.SourceSansBold
introText.ZIndex = 11 -- acima do Frame
introText.Parent = introFrame

-- Remove a tela após 7 segundos
task.delay(7, function()
    if introFrame then
        introFrame:Destroy()
    end
end)

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
hubIcon.Parent = screenGui
hubIcon.ZIndex = 12 -- acima da tela de introdução

-- ======================
-- Painel principal do Hub
-- ======================
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 900, 0, 500)
frame.Position = UDim2.new(0.5, -450, 0.25, 0)
frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
frame.Active = true
frame.Draggable = true
frame.Visible = false
frame.Parent = screenGui
frame.ZIndex = 5

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
contentLabel.Parent = frame

-- Função para abrir/fechar pelo ícone
hubIcon.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)
