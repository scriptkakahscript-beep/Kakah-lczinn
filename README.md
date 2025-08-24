--// LocalScript - Kakah Hub Unificado com Fly

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criação do GUI principal
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Painel principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 900, 0, 300)
frame.Position = UDim2.new(0.5, -450, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui

-- Estilo
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

-- Botão Minimizar
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 40, 0, 40)
toggleButton.Position = UDim2.new(1, -45, 0, 5)
toggleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.Text = "-"
toggleButton.Font = Enum.Font.SourceSansBold
toggleButton.TextScaled = true
toggleButton.Parent = frame

toggleButton.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)

-- Texto inicial
local contentLabel = Instance.new("TextLabel")
contentLabel.Size = UDim2.new(1, -20, 0, 40)
contentLabel.Position = UDim2.new(0, 10, 0, 50)
contentLabel.BackgroundTransparency = 1
contentLabel.Text = "Bem-vindo ao Kakah Hub!"
contentLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
contentLabel.TextScaled = true
contentLabel.TextWrapped = true
contentLabel.Parent = frame

-- // ABA DO FLY
local flyFrame = Instance.new("Frame")
flyFrame.Size = UDim2.new(0, 300, 0, 180)
flyFrame.Position = UDim2.new(0, 20, 0, 100)
flyFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
flyFrame.Parent = frame

Instance.new("UICorner", flyFrame).CornerRadius = UDim.new(0, 8)

local flyTitle = Instance.new("TextLabel")
flyTitle.Size = UDim2.new(1, 0, 0, 30)
flyTitle.BackgroundTransparency = 1
flyTitle.Text = "✈️ Fly Controller"
flyTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
flyTitle.TextScaled = true
flyTitle.Font = Enum.Font.SourceSansBold
flyTitle.Parent = flyFrame

-- Botão ligar/desligar fly
local flyButton = Instance.new("TextButton")
flyButton.Size = UDim2.new(0, 260, 0, 40)
flyButton.Position = UDim2.new(0, 20, 0, 40)
flyButton.Text = "Ativar Fly"
flyButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
flyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
flyButton.Font = Enum.Font.SourceSansBold
flyButton.TextScaled = true
flyButton.Parent = flyFrame
Instance.new("UICorner", flyButton).CornerRadius = UDim.new(0, 6)

-- Caixa para velocidade
local speedBox = Instance.new("TextBox")
speedBox.Size = UDim2.new(0, 260, 0, 40)
speedBox.Position = UDim2.new(0, 20, 0, 100)
speedBox.PlaceholderText = "Velocidade (padrão 50)"
speedBox.Text = ""
speedBox.TextColor3 = Color3.fromRGB(255, 255, 255)
speedBox.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
speedBox.Font = Enum.Font.SourceSans
speedBox.TextScaled = true
speedBox.Parent = flyFrame
Instance.new("UICorner", speedBox).CornerRadius = UDim.new(0, 6)

-- Variáveis Fly
local flying = false
local speed = 50
local hrp

local function getHRP()
    local char = player.Character or player.CharacterAdded:Wait()
    return char:WaitForChild("HumanoidRootPart")
end

local function fly()
    hrp = getHRP()
    local bv = Instance.new("BodyVelocity")
    bv.MaxForce = Vector3.new(4000, 4000, 4000)
    bv.Parent = hrp

    while flying and bv.Parent do
        RunService.Heartbeat:Wait()
        local move = Vector3.zero

        if UIS:IsKeyDown(Enum.KeyCode.W) then
            move += workspace.CurrentCamera.CFrame.LookVector * speed
        end
        if UIS:IsKeyDown(Enum.KeyCode.S) then
            move -= workspace.CurrentCamera.CFrame.LookVector * speed
        end
        if UIS:IsKeyDown(Enum.KeyCode.A) then
            move -= workspace.CurrentCamera.CFrame.RightVector * speed
        end
        if UIS:IsKeyDown(Enum.KeyCode.D) then
            move += workspace.CurrentCamera.CFrame.RightVector * speed
        end
        if UIS:IsKeyDown(Enum.KeyCode.Space) then
            move += Vector3.new(0, speed, 0)
        end
        if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then
            move -= Vector3.new(0, speed, 0)
        end

        bv.Velocity = move
    end

    bv:Destroy()
end

local function toggleFly()
    flying = not flying
    if flying then
        flyButton.Text = "Desativar Fly"
        fly()
    else
        flyButton.Text = "Ativar Fly"
    end
end

-- Conectar botões
flyButton.MouseButton1Click:Connect(toggleFly)

speedBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local val = tonumber(speedBox.Text)
        if val and val > 0 and val <= 200 then
            speed = val
        else
            speedBox.Text = ""
            speed = 50
        end
    end
end)

-- Hotkey Fly (F)
UIS.InputBegan:Connect(function(input, processed)
    if not processed and input.KeyCode == Enum.KeyCode.F then
        toggleFly()
    end
end)
