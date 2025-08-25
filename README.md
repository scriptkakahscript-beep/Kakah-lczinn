-- LocalScript - Kakah Hub Final com Fun

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- GUI
local playerGui = player:WaitForChild("PlayerGui")
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KakahHubGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Intro
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
local stroke = Instance.new("UIStroke", frame)
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(255,255,255)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,-50,0,40)
title.Position = UDim2.new(0,10,0,0)
title.BackgroundTransparency = 1
title.Text = "🔥 Kakah Hub"
title.TextColor3 = Color3.fromRGB(255,255,255)
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.Parent = frame

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

-- Função criar página
local function createPage(name, buttonY)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0,120,0,40)
    button.Position = UDim2.new(0,10,0,buttonY)
    button.BackgroundColor3 = Color3.fromRGB(0,0,0)
    button.TextColor3 = Color3.fromRGB(255,255,255)
    button.Text = name
    button.Font = Enum.Font.SourceSansBold
    button.TextScaled = true
    button.Parent = frame

    local page = Instance.new("Frame")
    page.Size = UDim2.new(1,-20,1,-50)
    page.Position = UDim2.new(0,10,0,50)
    page.BackgroundColor3 = Color3.fromRGB(255,0,0)
    page.Visible = false
    page.Parent = frame
    Instance.new("UICorner", page).CornerRadius = UDim.new(0,10)

    local back = Instance.new("TextButton")
    back.Size = UDim2.new(0,100,0,40)
    back.Position = UDim2.new(1,-120,0,10)
    back.BackgroundColor3 = Color3.fromRGB(0,0,0)
    back.TextColor3 = Color3.fromRGB(255,255,255)
    back.Text = "Voltar"
    back.Font = Enum.Font.SourceSansBold
    back.TextScaled = true
    back.Parent = page
    back.MouseButton1Click:Connect(function()
        page.Visible = false
    end)

    button.MouseButton1Click:Connect(function()
        page.Visible = not page.Visible
    end)

    return page
end

-- Créditos
local creditsPage = createPage("Créditos",130)
local creators = {"Kakah","ajuntantes lczin","Ninja","Lolyta"}
local creditsLabel = Instance.new("TextLabel")
creditsLabel.Size = UDim2.new(1,-20,1,-50)
creditsLabel.Position = UDim2.new(0,10,0,50)
creditsLabel.BackgroundTransparency = 1
creditsLabel.TextColor3 = Color3.fromRGB(255,255,255)
creditsLabel.TextSize = 30
creditsLabel.Font = Enum.Font.SourceSans
creditsLabel.TextYAlignment = Enum.TextYAlignment.Top
creditsLabel.Text = "👑 Criadores:\n"..table.concat(creators, "\n")
creditsLabel.Parent = creditsPage

local tiktokButton = Instance.new("TextButton")
tiktokButton.Size = UDim2.new(0,200,0,40)
tiktokButton.Position = UDim2.new(1,-220,0,50)
tiktokButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
tiktokButton.TextColor3 = Color3.fromRGB(255,255,255)
tiktokButton.Text = "TikTok do Kakah"
tiktokButton.Font = Enum.Font.SourceSansBold
tiktokButton.TextScaled = true
tiktokButton.Parent = creditsPage
tiktokButton.MouseButton1Click:Connect(function()
    if setclipboard then
        setclipboard("https://www.tiktok.com/@kaykaka2")
    end
end)

-- Fun
local funPage = createPage("Fun",180)

-- Botão Speed
local speedOn = false
local speedButton = Instance.new("TextButton")
speedButton.Size = UDim2.new(0,200,0,40)
speedButton.Position = UDim2.new(0,20,0,60)
speedButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
speedButton.TextColor3 = Color3.fromRGB(255,255,255)
speedButton.Text = "Ativar Speed"
speedButton.Font = Enum.Font.SourceSansBold
speedButton.TextScaled = true
speedButton.Parent = funPage
speedButton.MouseButton1Click:Connect(function()
    speedOn = not speedOn
    humanoid.WalkSpeed = speedOn and 100 or 16
    speedButton.Text = speedOn and "Desativar Speed" or "Ativar Speed"
end)

-- Botão Jump
local jumpOn = false
local jumpButton = Instance.new("TextButton")
jumpButton.Size = UDim2.new(0,200,0,40)
jumpButton.Position = UDim2.new(0,20,0,110)
jumpButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
jumpButton.TextColor3 = Color3.fromRGB(255,255,255)
jumpButton.Text = "Ativar Super Jump"
jumpButton.Font = Enum.Font.SourceSansBold
jumpButton.TextScaled = true
jumpButton.Parent = funPage
jumpButton.MouseButton1Click:Connect(function()
    jumpOn = not jumpOn
    humanoid.JumpPower = jumpOn and 200 or 50
    jumpButton.Text = jumpOn and "Desativar Super Jump" or "Ativar Super Jump"
end)

-- Botão Rainbow Name
local rainbowOn = false
local rainbowButton = Instance.new("TextButton")
rainbowButton.Size = UDim2.new(0,200,0,40)
rainbowButton.Position = UDim2.new(0,20,0,160)
rainbowButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
rainbowButton.TextColor3 = Color3.fromRGB(255,255,255)
rainbowButton.Text = "Ativar Rainbow Name"
rainbowButton.Font = Enum.Font.SourceSansBold
rainbowButton.TextScaled = true
rainbowButton.Parent = funPage

rainbowButton.MouseButton1Click:Connect(function()
    rainbowOn = not rainbowOn
    rainbowButton.Text = rainbowOn and "Desativar Rainbow Name" or "Ativar Rainbow Name"
    if rainbowOn then
        spawn(function()
            local head = character:WaitForChild("Head")
            local billboard = head:FindFirstChild("BillboardGui")
            if not billboard then
                billboard = Instance.new("BillboardGui", head)
                billboard.Size = UDim2.new(0,200,0,50)
                billboard.AlwaysOnTop = true
                local nameLabel = Instance.new("TextLabel", billboard)
                nameLabel.Size = UDim2.new(1,0,1,0)
                nameLabel.BackgroundTransparency = 1
                nameLabel.Font = Enum.Font.SourceSansBold
                nameLabel.TextScaled = true
                nameLabel.Text = player.Name
                nameLabel.Name = "NameLabel"
            end
            local label = billboard:FindFirstChild("NameLabel")
            while rainbowOn and label do
                for i = 0,1,0.01 do
                    label.TextColor3 = Color3.fromHSV(i,1,1)
                    task.wait(0.05)
                end
            end
        end)
    end
end)

-- Avatar
local avatarPage = createPage("Avatar",230)

-- Ícone
local hubIcon = Instance.new("TextButton")
hubIcon.Size = UDim2.new(0,50,0,50)
hubIcon.Position = UDim2.new(0,20,0,20)
hubIcon.BackgroundColor3 = Color3.fromRGB(0,0,0)
hubIcon.Text = "☰"
hubIcon.TextColor3 = Color3.fromRGB(255,255,255)
hubIcon.Font = Enum.Font.SourceSansBold
hubIcon.TextScaled = true
hubIcon.Parent = screenGui
hubIcon.ZIndex = 10
hubIcon.Visible = false

hubIcon.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
    if not frame.Visible then
        funPage.Visible = false
        avatarPage.Visible = false
        creditsPage.Visible = false
    end
end)

-- Mostrar ícone depois da intro
delay(7,function()
    introFrame:Destroy()
    hubIcon.Visible = true
end)
