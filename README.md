-- LocalScript dentro de StarterPlayerScripts

local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- GUI inicial (tela de boas-vindas)
local introGui = Instance.new("ScreenGui", playerGui)
introGui.Name = "IntroGui"
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

-- Hub principal
local hubGui = Instance.new("ScreenGui")
hubGui.Name = "KakahHub"
hubGui.ResetOnSpawn = false
hubGui.Parent = playerGui
hubGui.Enabled = false

task.delay(7, function()
	introGui:Destroy()
	hubGui.Enabled = true
end)

-- Frame principal do Hub
local hubFrame = Instance.new("Frame")
hubFrame.Size = UDim2.new(0,900,0,500)
hubFrame.Position = UDim2.new(0.5,-450,0.5,-250)
hubFrame.BackgroundColor3 = Color3.fromRGB(255,0,0)
hubFrame.Active = true
hubFrame.Draggable = true
hubFrame.Parent = hubGui

local hubTitle = Instance.new("TextLabel")
hubTitle.Size = UDim2.new(1,0,0,50)
hubTitle.BackgroundTransparency = 1
hubTitle.Text = "Kakah Hub"
hubTitle.Font = Enum.Font.SourceSansBold
hubTitle.TextColor3 = Color3.fromRGB(255,255,255)
hubTitle.TextScaled = true
hubTitle.Parent = hubFrame

-- Função para criar páginas internas
local function createPage(name)
	local page = Instance.new("Frame")
	page.Size = hubFrame.Size
	page.Position = hubFrame.Position
	page.BackgroundColor3 = hubFrame.BackgroundColor3
	page.Visible = false
	page.Parent = hubGui

	local title = Instance.new("TextLabel")
	title.Size = UDim2.new(1,0,0,50)
	title.BackgroundTransparency = 1
	title.Text = name
	title.Font = Enum.Font.SourceSansBold
	title.TextColor3 = Color3.fromRGB(255,255,255)
	title.TextScaled = true
	title.Parent = page

	local back = Instance.new("TextButton")
	back.Size = UDim2.new(0,150,0,40)
	back.Position = UDim2.new(0,20,1,-60)
	back.BackgroundColor3 = Color3.fromRGB(0,0,0)
	back.TextColor3 = Color3.fromRGB(255,255,255)
	back.Font = Enum.Font.SourceSansBold
	back.TextScaled = true
	back.Text = "Voltar"
	back.Parent = page
	back.MouseButton1Click:Connect(function()
		page.Visible = false
		hubFrame.Visible = true
	end)

	return page
end

-- Criando páginas
local creditsPage = createPage("Créditos")
local funPage = createPage("Fun")
local avatarPage = createPage("Avatar")
local trollPage = createPage("Troll")

-- Botões do Hub principal
local function addButton(text, order, page)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(0,200,0,40)
	btn.Position = UDim2.new(0,20,0,60 + (order * 50))
	btn.BackgroundColor3 = Color3.fromRGB(0,0,0)
	btn.TextColor3 = Color3.fromRGB(255,255,255)
	btn.Font = Enum.Font.SourceSansBold
	btn.TextScaled = true
	btn.Text = text
	btn.Parent = hubFrame

	btn.MouseButton1Click:Connect(function()
		hubFrame.Visible = false
		page.Visible = true
	end)
end

addButton("Créditos",0,creditsPage)
addButton("Fun",1,funPage)
addButton("Avatar",2,avatarPage)
addButton("Troll",3,trollPage)

-- Conteúdo da página Créditos
local creators = {"Kakah","Lczin","Ninja","Lolyta"}
for i,name in ipairs(creators) do
	local lbl = Instance.new("TextLabel")
	lbl.Size = UDim2.new(0,300,0,30)
	lbl.Position = UDim2.new(0,20,0,70 + (i*35))
	lbl.BackgroundTransparency = 1
	lbl.Text = name
	lbl.TextColor3 = Color3.fromRGB(255,255,255)
	lbl.Font = Enum.Font.SourceSansBold
	lbl.TextScaled = true
	lbl.Parent = creditsPage
end

-- Botão TikTok dentro dos Créditos
local tiktokButton = Instance.new("TextButton")
tiktokButton.Size = UDim2.new(0,200,0,40)
tiktokButton.Position = UDim2.new(0,20,1,-110)
tiktokButton.BackgroundColor3 = Color3.fromRGB(0,0,0)
tiktokButton.TextColor3 = Color3.fromRGB(255,255,255)
tiktokButton.Text = "Abrir TikTok"
tiktokButton.Font = Enum.Font.SourceSansBold
tiktokButton.TextScaled = true
tiktokButton.Parent = creditsPage

tiktokButton.MouseButton1Click:Connect(function()
	pcall(function()
		setclipboard("https://www.tiktok.com/@kaykaka2?_t=ZM-8zA4oJ0BjV8&_r=1")
		game.StarterGui:SetCore("SendNotification", {
			Title = "TikTok do Kakah",
			Text = "Link copiado para área de transferência!",
			Duration = 10
		})
	end)
end)
