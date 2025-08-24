-- Kakah Hub com Aimbot (para uso no SEU JOGO no Roblox Studio)

local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

-- GUI
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local ToggleButton = Instance.new("TextButton")

ScreenGui.Name = "KakahHub"
ScreenGui.Parent = player:WaitForChild("PlayerGui")

-- Painel principal
MainFrame.Size = UDim2.new(0, 250, 0, 150)
MainFrame.Position = UDim2.new(0.3, 0, 0.3, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

-- Título
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.BackgroundColor3 = Color3.fromRGB(50, 0, 0)
Title.Text = "Kakah Hub - Aimbot"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextScaled = true
Title.Parent = MainFrame

-- Botão
ToggleButton.Size = UDim2.new(0.8, 0, 0.4, 0)
ToggleButton.Position = UDim2.new(0.1, 0, 0.4, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Text = "Ligar Aimbot"
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextScaled = true
ToggleButton.Parent = MainFrame

-- Função Aimbot
local ativo = false
local RunService = game:GetService("RunService")

local function getNearestTarget()
    local closest, dist = nil, math.huge
    for _, enemy in pairs(game.Players:GetPlayers()) do
        if enemy ~= player and enemy.Character and enemy.Character:FindFirstChild("Head") then
            local head = enemy.Character.Head
            local pos, onScreen = workspace.CurrentCamera:WorldToViewportPoint(head.Position)
            if onScreen then
                local mag = (Vector2.new(pos.X, pos.Y) - Vector2.new(mouse.X, mouse.Y)).Magnitude
                if mag < dist then
                    dist = mag
                    closest = head
                end
            end
        end
    end
    return closest
end

RunService.RenderStepped:Connect(function()
    if ativo then
        local target = getNearestTarget()
        if target then
            workspace.CurrentCamera.CFrame = CFrame.new(workspace.CurrentCamera.CFrame.Position, target.Position)
        end
    end
end)

-- Toggle do botão
ToggleButton.MouseButton1Click:Connect(function()
    ativo = not ativo
    if ativo then
        ToggleButton.Text = "Desligar Aimbot"
        print("Aimbot ativado!")
    else
        ToggleButton.Text = "Ligar Aimbot"
        print("Aimbot desativado!")
    end
end)
