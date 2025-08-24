-- LocalScript

local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criação do GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.Parent = playerGui

-- Painel principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 450, 0, 250)
frame.Position = UDim2.new(0.5, -225, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- todo vermelho
frame.Visible = true
frame.Parent = screenGui

-- Título do painel
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundTransparency = 1
title.Text = "Kakah Hub"
title.TextColor3 = Color3.fromRGB(255, 255, 255) -- branco
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.Parent = frame

-- Botão de fechar/abrir
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 40, 0, 40)
toggleButton.Position = UDim2.new(1, -45, 0, 5)
toggleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.Text = "X"
toggleButton.Font = Enum.Font.SourceSansBold
toggleButton.TextScaled = true
toggleButton.Parent = frame

-- Função de abrir/fechar
toggleButton.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)

-- Exemplo de conteúdo interno do hub (pode colocar funções depois)
local contentLabel = Instance.new("TextLabel")
contentLabel.Size = UDim2.new(1, -20, 1, -60)
contentLabel.Position = UDim2.new(0, 10, 0, 50)
contentLabel.BackgroundTransparency = 1
contentLabel.Text = "Bem-vindo ao Kakah Hub!"
contentLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
contentLabel.TextScaled = true
contentLabel.TextWrapped = true
contentLabel.Parent = frame

-- // Fly GUI para Roblox Brookhaven
-- Nome: Kakah Fly Hub

-- Cria ScreenGui
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local ToggleButton = Instance.new("TextButton")
local SpeedSlider = Instance.new("TextBox")
local CloseButton = Instance.new("TextButton")
local UICorner = Instance.new("UICorner")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.Size = UDim2.new(0, 200, 0, 140)
Frame.Position = UDim2.new(0.3, 0, 0.3, 0)
Frame.Active = true
Frame.Draggable = true -- 🔥 arrastável

UICorner.Parent = Frame

-- Botão ligar/desligar fly
ToggleButton.Parent = Frame
ToggleButton.Size = UDim2.new(0, 180, 0, 40)
ToggleButton.Position = UDim2.new(0, 10, 0, 30)
ToggleButton.Text = "Ativar Fly"
ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Caixa para velocidade
SpeedSlider.Parent = Frame
SpeedSlider.Size = UDim2.new(0, 180, 0, 40)
SpeedSlider.Position = UDim2.new(0, 10, 0, 80)
SpeedSlider.PlaceholderText = "Velocidade (padrão 50)"
SpeedSlider.Text = ""

-- Botão fechar
CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(0, 25, 0, 25)
CloseButton.Position = UDim2.new(1, -30, 0, 5)
CloseButton.Text = "X"
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Variáveis
local flying = false
local speed = 50
local plr = game.Players.LocalPlayer
local char = plr.Character or plr.CharacterAdded:Wait()
local hrp = char:WaitForChild("HumanoidRootPart")
local UIS = game:GetService("UserInputService")

-- Função do Fly
local function fly()
    local bv = Instance.new("BodyVelocity")
    bv.Velocity = Vector3.new(0,0,0)
    bv.MaxForce = Vector3.new(4000,4000,4000)
    bv.Parent = hrp

    while flying do
        task.wait()
        local move = Vector3.new(0,0,0)
        if UIS:IsKeyDown(Enum.KeyCode.W) then
            move = move + (workspace.CurrentCamera.CFrame.LookVector * speed)
        end
        if UIS:IsKeyDown(Enum.KeyCode.S) then
            move = move - (workspace.CurrentCamera.CFrame.LookVector * speed)
        end
        if UIS:IsKeyDown(Enum.KeyCode.A) then
            move = move - (workspace.CurrentCamera.CFrame.RightVector * speed)
        end
        if UIS:IsKeyDown(Enum.KeyCode.D) then
            move = move + (workspace.CurrentCamera.CFrame.RightVector * speed)
        end
        if UIS:IsKeyDown(Enum.KeyCode.Space) then
            move = move + Vector3.new(0,speed,0)
        end
        if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then
            move = move - Vector3.new(0,speed,0)
        end
        bv.Velocity = move
    end
    hrp:FindFirstChildOfClass("BodyVelocity"):Destroy()
end

-- Função para trocar estado do fly
local function toggleFly()
    flying = not flying
    if flying then
        ToggleButton.Text = "Desativar Fly"
        fly()
    else
        ToggleButton.Text = "Ativar Fly"
    end
end

-- Botão ativar/desativar
ToggleButton.MouseButton1Click:Connect(toggleFly)

-- Alterar velocidade
SpeedSlider.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local val = tonumber(SpeedSlider.Text)
        if val and val > 0 and val <= 100 then
            speed = val
        else
            SpeedSlider.Text = ""
            speed = 50
        end
    end
end)

-- Fechar GUI
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- HOTKEY (tecla F)
UIS.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == Enum.KeyCode.F then
        toggleFly()
    end
end)
