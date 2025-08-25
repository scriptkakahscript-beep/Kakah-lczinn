-- LocalScript dentro de StarterPlayerScripts

local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- TELA INICIAL
local introGui = Instance.new("ScreenGui", playerGui)
introGui.ResetOnSpawn = false

local introFrame = Instance.new("Frame", introGui)
introFrame.Size = UDim2.new(1,0,1,0)
introFrame.BackgroundColor3 = Color3.fromRGB(255,0,0)

local introText = Instance.new("TextLabel", introFrame)
introText.Size = UDim2.new(1,0,1,0)
introText.Text = "Seja bem-vindo ao Kakah Hub"
introText.TextColor3 = Color3.fromRGB(255,255,255)
introText.Font = Enum.Font.SourceSansBold
introText.TextScaled = true
introText.BackgroundTransparency = 1

-- HUB GUI (criado aqui para o delay funcionar)
local hubGui = Instance.new("ScreenGui", playerGui)
hubGui.ResetOnSpawn = false
hubGui.Enabled = false

task.delay(7, function()
	introGui:Destroy()
	hubGui.Enabled = true
end)

-- HUB PRINCIPAL
local hubFrame = Instance.new("Frame", hubGui)
hubFrame.Size = UDim2.new(0,900,0,500)
hubFrame.Position = UDim2.new(0.5,-450,0.5,-250)
hubFrame.BackgroundColor3 = Color3.fromRGB(255,0,0)
hubFrame.Active = true
hubFrame.Draggable = true

local hubTitle = Instance.new("TextLabel", hubFrame)
hubTitle.Size = UDim2.new(1,0,0,50)
hubTitle.BackgroundTransparency = 1
hubTitle.Text = "Kakah Hub"
hubTitle.Font = Enum.Font.SourceSansBold
hubTitle.TextColor3 = Color3.fromRGB(255,255,255)
hubTitle.TextScaled = true

-- FUNÇÃO PARA CRIAR PÁGINAS
local function createPage(name)
	local page = Instance.new("Frame", hubGui)
	page.Size = hubFrame.Size
	page.Position = hubFrame.Position
	page.BackgroundColor3 = hubFrame.BackgroundColor3
	page.Visible = false

	local title = Instance.new("TextLabel", page)
	title.Size = UDim2.new(1,0,0,50)
	title.BackgroundTransparency = 1
	title.Text = name
	title.Font = Enum.Font.SourceSansBold
	title.TextColor3 = Color3.fromRGB(255,255,255)
	title.TextScaled = true

	local back = Instance.new("TextButton", page)
	back.Size = UDim2.new(0,150,0,40)
	back.Position = UDim2.new(0,20,1,-60)
	back.BackgroundColor3 = Color3.fromRGB(0,0,0)
	back.TextColor3 = Color3.fromRGB(255,255,255)
	back.Font = Enum.Font.SourceSansBold
	back.TextScaled = true
	back.Text = "Voltar"
	back.MouseButton1Click:Connect(function()
		page.Visible = false
		hubFrame.Visible = true
	end)

	return page
end

-- CRIAR PÁGINAS
local creditsPage = createPage("Créditos")
local funPage = createPage("Fun")
local avatarPage = createPage("Avatar")
local trollPage = createPage("Troll")

-- BOTÕES DO HUB
local function addButton(text, order, page)
	local btn = Instance.new("TextButton", hubFrame)
	btn.Size = UDim2.new(0,200,0,40)
	btn.Position = UDim2.new(0,20,0,60 + (order * 50))
	btn.BackgroundColor3 = Color3.fromRGB(0,0,0)
	btn.TextColor3 = Color3.fromRGB(255,255,255)
	btn.Font = Enum.Font.SourceSansBold
	btn.TextScaled = true
	btn.Text = text
	btn.MouseButton1Click:Connect(function()
		hubFrame.Visible = false
		page.Visible = true
	end)
end

addButton("Créditos",0,creditsPage)
addButton("Fun",1,funPage)
addButton("Avatar",2,avatarPage)
addButton("Troll",3,trollPage)

-- CONTEÚDO CRÉDITOS
local creators = {"Kakah","Lczin","Ninja","Lolyta"}
for i,name in ipairs(creators) do
	local lbl = Instance.new("TextLabel", creditsPage)
	lbl.Size = UDim2.new(0,300,0,30)
	lbl.Position = UDim2.new(0,20,0,70 + (i*40))
	lbl.BackgroundTransparency = 1
	lbl.Text = name
	lbl.TextColor3 = Color3.fromRGB(255,255,255)
	lbl.Font = Enum.Font.SourceSansBold
	lbl.TextScaled = true
end

-- BOTÃO TIKTOK
local tiktokButton = Instance.new("TextButton", creditsPage)
tiktokButton.Size = UDim2.new(0,200,0,40)
tiktokButton.Position = UDim2.new(0,20,1,-110)
tiktokButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
tiktokButton.TextColor3 = Color3.fromRGB(255,255,255)
tiktokButton.Text = "Abrir TikTok"
tiktokButton.Font = Enum.Font.SourceSansBold
tiktokButton.TextScaled = true

tiktokButton.MouseButton1Click:Connect(function()
	pcall(function()
		game.StarterGui:SetCore("SendNotification", {
			Title = "TikTok do Kakah",
			Text = "👉 https://www.tiktok.com/@kaykaka2",
			Duration = 10
		})
	end)
end)
