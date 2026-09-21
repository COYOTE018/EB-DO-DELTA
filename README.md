local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local ID_BOLA = "rbxassetid://84861533911481"
local ID_FUNDO = "rbxassetid://120671511416721"
local TOM_SCRIPT = "https://rawscripts.net/raw/Universal-Script-Auto-jjs-EB-do-delta-126144"
local KEY_URL = "https://gist.githubusercontent.com/COYOTE018/c5e666d427ec7d7ab1ef85e2a7f3c0cb/raw"
local FALLBACK_KEY = "BOBESPUNJA"

local correctKey = FALLBACK_KEY
local ok, res = pcall(function()
	return game:HttpGet(KEY_URL)
end)
if ok and res and res \~= "" and not tostring(res):find("<html") then
	correctKey = tostring(res):gsub("%s+", "")
end

if playerGui:FindFirstChild("GBDASP_GUI") then
	playerGui.GBDASP_GUI:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "GBDASP_GUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = playerGui

local function makeDraggable(frame)
	local dragging, dragStart, startPos = false, nil, nil
	frame.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = frame.Position
		end
	end)
	frame.InputEnded:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = false
		end
	end)
	UserInputService.InputChanged:Connect(function(input)
		if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
			local d = input.Position - dragStart
			frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + d.X, startPos.Y.Scale, startPos.Y.Offset + d.Y)
		end
	end)
end

local KeyFrame = Instance.new("Frame")
KeyFrame.Size = UDim2.new(0, 300, 0, 170)
KeyFrame.Position = UDim2.new(0.5, -150, 0.5, -85)
KeyFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 26)
KeyFrame.Parent = ScreenGui
Instance.new("UICorner", KeyFrame).CornerRadius = UDim.new(0, 10)

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "Digite a Key"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 20
Title.Parent = KeyFrame

local KeyBox = Instance.new("TextBox")
KeyBox.Size = UDim2.new(0.85, 0, 0, 38)
KeyBox.Position = UDim2.new(0.075, 0, 0.35, 0)
KeyBox.BackgroundColor3 = Color3.fromRGB(35, 35, 42)
KeyBox.Text = ""
KeyBox.PlaceholderText = "Key aqui..."
KeyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyBox.Font = Enum.Font.Gotham
KeyBox.TextSize = 16
KeyBox.Parent = KeyFrame
Instance.new("UICorner", KeyBox).CornerRadius = UDim.new(0, 8)

local SubmitBtn = Instance.new("TextButton")
SubmitBtn.Size = UDim2.new(0.85, 0, 0, 36)
SubmitBtn.Position = UDim2.new(0.075, 0, 0.65, 0)
SubmitBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
SubmitBtn.Text = "Confirmar"
SubmitBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
SubmitBtn.Font = Enum.Font.GothamBold
SubmitBtn.TextSize = 16
SubmitBtn.Parent = KeyFrame
Instance.new("UICorner", SubmitBtn).CornerRadius = UDim.new(0, 8)
makeDraggable(KeyFrame)

local Ball = Instance.new("TextButton")
Ball.Size = UDim2.new(0, 65, 0, 65)
Ball.Position = UDim2.new(0.85, 0, 0.4, 0)
Ball.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
Ball.Text = ""
Ball.Visible = false
Ball.Parent = ScreenGui
Instance.new("UICorner", Ball).CornerRadius = UDim.new(1, 0)

local BallImg = Instance.new("ImageLabel")
BallImg.Image = ID_BOLA
BallImg.Size = UDim2.new(1, 0, 1, 0)
BallImg.BackgroundTransparency = 1
BallImg.Parent = Ball
Instance.new("UICorner", BallImg).CornerRadius = UDim.new(1, 0)
makeDraggable(Ball)

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 480, 0, 400)
MainFrame.Position = UDim2.new(0.5, -240, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(16, 16, 20)
MainFrame.Visible = false
MainFrame.Parent = ScreenGui
Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 10)

local FundoImg = Instance.new("ImageLabel")
FundoImg.Image = ID_FUNDO
FundoImg.Size = UDim2.new(1, 0, 1, 0)
FundoImg.BackgroundTransparency = 1
FundoImg.ImageTransparency = 0.5
FundoImg.ZIndex = 0
FundoImg.Parent = MainFrame
Instance.new("UICorner", FundoImg).CornerRadius = UDim.new(0, 10)

local Sidebar = Instance.new("Frame")
Sidebar.Size = UDim2.new(0, 120, 1, 0)
Sidebar.BackgroundColor3 = Color3.fromRGB(24, 24, 30)
Sidebar.BackgroundTransparency = 0.3
Sidebar.ZIndex = 2
Sidebar.Parent = MainFrame
Instance.new("UICorner", Sidebar).CornerRadius = UDim.new(0, 10)

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -130, 1, -15)
Content.Position = UDim2.new(0, 125, 0, 8)
Content.BackgroundTransparency = 1
Content.ZIndex = 3
Content.Parent = MainFrame

local ContentTitle = Instance.new("TextLabel")
ContentTitle.Size = UDim2.new(1, 0, 0, 28)
ContentTitle.BackgroundTransparency = 1
ContentTitle.Text = "Patentes"
ContentTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
ContentTitle.Font = Enum.Font.GothamBold
ContentTitle.TextSize = 18
ContentTitle.TextXAlignment = Enum.TextXAlignment.Left
ContentTitle.ZIndex = 3
ContentTitle.Parent = Content

local function createTab(name, y)
	local tab = Instance.new("TextButton")
	tab.Size = UDim2.new(1, -12, 0, 34)
	tab.Position = UDim2.new(0, 6, 0, y)
	tab.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
	tab.BackgroundTransparency = 0.2
	tab.Text = name
	tab.TextColor3 = Color3.fromRGB(220, 220, 220)
	tab.Font = Enum.Font.Gotham
	tab.TextSize = 14
	tab.ZIndex = 3
	tab.Parent = Sidebar
	Instance.new("UICorner", tab).CornerRadius = UDim.new(0, 6)
	return tab
end

local TabPatentes = createTab("Patentes", 12)
local TabPerguntas = createTab("Perguntas", 52)
local TabParkour = createTab("Parkour", 92)
local TabJJs = createTab("JJs", 132)
local TabFarm = createTab("Farm", 172)
local TabOutros = createTab("Outros", 212)
local TabClose = createTab("Fechar", 340)

local function addCopyRow(parent, text)
	local row = Instance.new("Frame")
	row.Size = UDim2.new(1, -8, 0, 28)
	row.BackgroundColor3 = Color3.fromRGB(30, 30, 38)
	row.BackgroundTransparency = 0.2
	row.ZIndex = 3
	row.Parent = parent
	Instance.new("UICorner", row).CornerRadius = UDim.new(0, 5)

	local label = Instance.new("TextLabel")
	label.Size = UDim2.new(1, -70, 1, 0)
	label.Position = UDim2.new(0, 8, 0, 0)
	label.BackgroundTransparency = 1
	label.Text = text
	label.TextColor3 = Color3.fromRGB(230, 230, 230)
	label.Font = Enum.Font.Gotham
	label.TextSize = 13
	label.TextXAlignment = Enum.TextXAlignment.Left
	label.TextTruncate = Enum.TextTruncate.AtEnd
	label.ZIndex = 4
	label.Parent = row

	local copyBtn = Instance.new("TextButton")
	copyBtn.Size = UDim2.new(0, 58, 0, 22)
	copyBtn.Position = UDim2.new(1, -64, 0.5, -11)
	copyBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 220)
	copyBtn.Text = "Copiar"
	copyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
	copyBtn.Font = Enum.Font.GothamBold
	copyBtn.TextSize = 12
	copyBtn.ZIndex = 4
	copyBtn.Parent = row
	Instance.new("UICorner", copyBtn).CornerRadius = UDim.new(0, 4)

	copyBtn.MouseButton1Click:Connect(function()
		if setclipboard then
			setclipboard(text)
			copyBtn.Text = "Copiado!"
			task.wait(1)
			copyBtn.Text = "Copiar"
		end
	end)
end

local PatentesScroll = Instance.new("ScrollingFrame")
PatentesScroll.Size = UDim2.new(1, 0, 1, -35)
PatentesScroll.Position = UDim2.new(0, 0, 0, 32)
PatentesScroll.BackgroundTransparency = 1
PatentesScroll.ScrollBarThickness = 4
PatentesScroll.Visible = true
PatentesScroll.ZIndex = 3
PatentesScroll.Parent = Content
local PatentesList = Instance.new("UIListLayout")
PatentesList.Padding = UDim.new(0, 4)
PatentesList.Parent = PatentesScroll

local hierarchy = {
	{cat = "Criador", items = {"[CR] Criador", "[SCR] Sub Criador"}},
	{cat = "Administração", items = {"[ADM-G] Administrador Geral", "[ADM] Administrador", "[SUP-ADM] Supervisor Administrativo", "[MOD] Moderador"}},
	{cat = "Supremacia", items = {"[SC] Sócios"}},
	{cat = "Alto Comando", items = {"[CMT] Comandante", "[SCMT] Subcomandante"}},
	{cat = "Oficiais da Elite", items = {"[ER] Elite Real", "[ES] Elite Secreta", "[EM] Elite Militar"}},
	{cat = "Oficiais Generais", items = {"[GEN EX] General de Exército", "[GEN DV] General de Divisão", "[GEN BDA] General de Brigada"}},
	{cat = "Oficiais Superiores", items = {"[CEL] Coronel", "[TEN-CEL] Tenente Coronel", "[MAJ] Major"}},
	{cat = "Oficiais Intermediários", items = {"[CAP] Capitão"}},
	{cat = "Oficiais Subalternos", items = {"[1º TEN] Primeiro Tenente", "[2º TEN] Segundo Tenente", "[ASP] Aspirante a Oficial"}},
	{cat = "Praças Especiais", items = {"[CT] Cadete"}},
	{cat = "Graduados", items = {"[ST] Subtenente", "[1º SGT] Primeiro Sargento", "[2º SGT] Segundo Sargento", "[3º SGT] Terceiro Sargento"}},
	{cat = "Praças", items = {"[CB] Cabo", "[SLD] Soldado", "[REC] Recruta"}}
}

for _, section in ipairs(hierarchy) do
	local catLabel = Instance.new("TextLabel")
	catLabel.Size = UDim2.new(1, -8, 0, 22)
	catLabel.BackgroundTransparency = 1
	catLabel.Text = section.cat
	catLabel.TextColor3 = Color3.fromRGB(0, 170, 255)
	catLabel.Font = Enum.Font.GothamBold
	catLabel.TextSize = 13
	catLabel.TextXAlignment = Enum.TextXAlignment.Left
	catLabel.ZIndex = 3
	catLabel.Parent = PatentesScroll
	for _, item in ipairs(section.items) do
		addCopyRow(PatentesScroll, item)
	end
end
PatentesList:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
	PatentesScroll.CanvasSize = UDim2.new(0, 0, 0, PatentesList.AbsoluteContentSize.Y + 20)
end)
PatentesScroll.CanvasSize = UDim2.new(0, 0, 0, PatentesList.AbsoluteContentSize.Y + 20)

local PerguntasScroll = Instance.new("ScrollingFrame")
PerguntasScroll.Size = UDim2.new(1, 0, 1, -35)
PerguntasScroll.Position = UDim2.new(0, 0, 0, 32)
PerguntasScroll.BackgroundTransparency = 1
PerguntasScroll.ScrollBarThickness = 4
PerguntasScroll.Visible = false
PerguntasScroll.ZIndex = 3
PerguntasScroll.Parent = Content
local PerguntasList = Instance.new("UIListLayout")
PerguntasList.Padding = UDim.new(0, 4)
PerguntasList.Parent = PerguntasScroll

local siglas = {
	{"AMAN", "Academia de Agulhas Negras"},
	{"E.P.C", "Escola Preparatória de Coronéis"},
	{"APG", "Academia Preparatória de Generais"},
	{"BIP", "Batalhão de Infantaria Paraquedistas"},
	{"BPE", "Batalhão da Polícia do Exército"},
	{"BFE", "Batalhão de Forças Especiais"},
	{"BAC", "Batalhão de Ações de Comandos"},
	{"CIE", "Centro de Inteligência do Exército"},
	{"CIGS", "Centro de Instrução de Guerras na Selva"},
	{"CYBER", "Comando de Defesa Cibernética"},
	{"BI-CAAT", "Batalhão de Infantaria da Caatinga"},
	{"REC-MEC", "Regimento da Cavalaria Mecânica"}
}
for _, data in ipairs(siglas) do
	addCopyRow(PerguntasScroll, data[1] .. ": " .. data[2])
end
PerguntasList:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
	PerguntasScroll.CanvasSize = UDim2.new(0, 0, 0, PerguntasList.AbsoluteContentSize.Y + 20)
end)
PerguntasScroll.CanvasSize = UDim2.new(0, 0, 0, PerguntasList.AbsoluteContentSize.Y + 20)

local ParkourContent = Instance.new("Frame")
ParkourContent.Size = UDim2.new(1, 0, 1, -35)
ParkourContent.Position = UDim2.new(0, 0, 0, 32)
ParkourContent.BackgroundTransparency = 1
ParkourContent.Visible = false
ParkourContent.ZIndex = 3
ParkourContent.Parent = Content

local ParkourBtn = Instance.new("TextButton")
ParkourBtn.Size = UDim2.new(0.9, 0, 0, 42)
ParkourBtn.Position = UDim2.new(0.05, 0, 0.1, 0)
ParkourBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
ParkourBtn.Text = "Parkour Auxiliar: OFF"
ParkourBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ParkourBtn.Font = Enum.Font.GothamBold
ParkourBtn.TextSize = 15
ParkourBtn.ZIndex = 3
ParkourBtn.Parent = ParkourContent
Instance.new("UICorner", ParkourBtn).CornerRadius = UDim.new(0, 8)

local parkourEnabled = false
ParkourBtn.MouseButton1Click:Connect(function()
	parkourEnabled = not parkourEnabled
	ParkourBtn.Text = parkourEnabled and "Parkour Auxiliar: ON" or "Parkour Auxiliar: OFF"
	ParkourBtn.BackgroundColor3 = parkourEnabled and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(40, 40, 50)
end)

local JJsContent = Instance.new("Frame")
JJsContent.Size = UDim2.new(1, 0, 1, -35)
JJsContent.Position = UDim2.new(0, 0, 0, 32)
JJsContent.BackgroundTransparency = 1
JJsContent.Visible = false
JJsContent.ZIndex = 3
JJsContent.Parent = Content

local JJsBtn = Instance.new("TextButton")
JJsBtn.Size = UDim2.new(0.9, 0, 0, 42)
JJsBtn.Position = UDim2.new(0.05, 0, 0.1, 0)
JJsBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
JJsBtn.Text = "AUTO JJS: OFF"
JJsBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
JJsBtn.Font = Enum.Font.GothamBold
JJsBtn.TextSize = 15
JJsBtn.ZIndex = 3
JJsBtn.Parent = JJsContent
Instance.new("UICorner", JJsBtn).CornerRadius = UDim.new(0, 8)

local tomCarregado = false
JJsBtn.MouseButton1Click:Connect(function()
	if tomCarregado then return end
	JJsBtn.Text = "AUTO JJS: ON"
	JJsBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
	tomCarregado = true
	pcall(function()
		loadstring(game:HttpGet(TOM_SCRIPT))()
	end)
end)

local FarmContent = Instance.new("Frame")
FarmContent.Size = UDim2.new(1, 0, 1, -35)
FarmContent.Position = UDim2.new(0, 0, 0, 32)
FarmContent.BackgroundTransparency = 1
FarmContent.Visible = false
FarmContent.ZIndex = 3
FarmContent.Parent = Content

local Lixos = {
	Vector3.new(470.87, 3.04, -885.88),
	Vector3.new(377.87, 3.04, -940.65),
	Vector3.new(225.02, 3.04, -974.52),
	Vector3.new(102.27, 3.04, -889.48),
	Vector3.new(-160.73, 3.04, -803.28),
	Vector3.new(-389.38, 3.04, -1075.70),
	Vector3.new(-421.97, 3.04, -970.06),
}
local Lixeira = Vector3.new(-394.31, 3.04, -779.87)
local Foice = Vector3.new(-351.95, 3.12, -631.06)
local Gramas = {
	Vector3.new(82.63, 3.00, -671.36), Vector3.new(-45.00, 3.00, -671.39),
	Vector3.new(-15.39, 3.00, -619.51), Vector3.new(218.96, 3.00, -758.32),
	Vector3.new(112.01, 3.00, -652.70), Vector3.new(123.73, 3.00, -741.72),
	Vector3.new(51.76, 3.00, -1001.02), Vector3.new(173.18, 3.00, -987.78),
	Vector3.new(175.72, 3.00, -931.94), Vector3.new(120.00, 3.00, -848.69),
	Vector3.new(54.60, 3.00, -780.14), Vector3.new(10.21, 3.00, -744.73),
}
local CaixaPega = Vector3.new(77.48, 3.04, -429.99)
local CaixaEntrega = Vector3.new(440.87, 3.85, -224.70)
local autoLixo, autoGrama, autoCaixa = false, false, false

local function teleportTo(pos)
	local char = player.Character
	local hrp = char and char:FindFirstChild("HumanoidRootPart")
	if hrp then
		hrp.CFrame = CFrame.new(pos + Vector3.new(0, 3, 0))
	end
end

local function activateNearPrompts()
	local char = player.Character
	local hrp = char and char:FindFirstChild("HumanoidRootPart")
	if not hrp then return end
	for _ = 1, 3 do
		for _, obj in pairs(workspace:GetDescendants()) do
			if obj:IsA("ProximityPrompt") and obj.Enabled then
				local parent = obj.Parent
				if parent and parent:IsA("BasePart") and (parent.Position - hrp.Position).Magnitude < 15 then
					pcall(function()
						fireproximityprompt(obj)
					end)
				end
			end
		end
		task.wait(0.25)
	end
end

local function startAutoLixo()
	task.spawn(function()
		while autoLixo do
			for i = 1, #Lixos do
				if not autoLixo then break end
				teleportTo(Lixos[i])
				task.wait(1)
				activateNearPrompts()
				task.wait(1.2)
				teleportTo(Lixeira)
				task.wait(1)
				activateNearPrompts()
				task.wait(1.2)
			end
		end
	end)
end

local function startAutoGrama()
	task.spawn(function()
		teleportTo(Foice)
		task.wait(1.2)
		activateNearPrompts()
		task.wait(1.5)
		while autoGrama do
			for i = 1, #Gramas do
				if not autoGrama then break end
				teleportTo(Gramas[i])
				task.wait(1)
				activateNearPrompts()
				task.wait(1.2)
			end
		end
	end)
end

local function startAutoCaixa()
	task.spawn(function()
		while autoCaixa do
			teleportTo(CaixaPega)
			task.wait(1)
			activateNearPrompts()
			task.wait(1.2)
			teleportTo(CaixaEntrega)
			task.wait(1)
			activateNearPrompts()
			task.wait(1.2)
			task.wait(30)
		end
	end)
end

local function createFarmBtn(text, y)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(0.9, 0, 0, 40)
	btn.Position = UDim2.new(0.05, 0, 0, y)
	btn.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
	btn.Text = text
	btn.TextColor3 = Color3.fromRGB(255, 255, 255)
	btn.Font = Enum.Font.GothamBold
	btn.TextSize = 14
	btn.ZIndex = 3
	btn.Parent = FarmContent
	Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 8)
	return btn
end

local LixoBtn = createFarmBtn("AUTO LIXO: OFF", 30)
local GramaBtn = createFarmBtn("AUTO GRAMA: OFF", 80)
local CaixaBtn = createFarmBtn("AUTO CAIXA: OFF", 130)

LixoBtn.MouseButton1Click:Connect(function()
	autoLixo = not autoLixo
	LixoBtn.Text = autoLixo and "AUTO LIXO: ON" or "AUTO LIXO: OFF"
	LixoBtn.BackgroundColor3 = autoLixo and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(40, 40, 50)
	if autoLixo then startAutoLixo() end
end)

GramaBtn.MouseButton1Click:Connect(function()
	autoGrama = not autoGrama
	GramaBtn.Text = autoGrama and "AUTO GRAMA: ON" or "AUTO GRAMA: OFF"
	GramaBtn.BackgroundColor3 = autoGrama and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(40, 40, 50)
	if autoGrama then startAutoGrama() end
end)

CaixaBtn.MouseButton1Click:Connect(function()
	autoCaixa = not autoCaixa
	CaixaBtn.Text = autoCaixa and "AUTO CAIXA: ON" or "AUTO CAIXA: OFF"
	CaixaBtn.BackgroundColor3 = autoCaixa and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(40, 40, 50)
	if autoCaixa then startAutoCaixa() end
end)

local OutrosContent = Instance.new("Frame")
OutrosContent.Size = UDim2.new(1, 0, 1, -35)
OutrosContent.Position = UDim2.new(0, 0, 0, 32)
OutrosContent.BackgroundTransparency = 1
OutrosContent.Visible = false
OutrosContent.ZIndex = 3
OutrosContent.Parent = Content

local ChatBtn = Instance.new("TextButton")
ChatBtn.Size = UDim2.new(0.9, 0, 0, 42)
ChatBtn.Position = UDim2.new(0.05, 0, 0.1, 0)
ChatBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
ChatBtn.Text = "LIBERAR CHAT"
ChatBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ChatBtn.Font = Enum.Font.GothamBold
ChatBtn.TextSize = 15
ChatBtn.ZIndex = 3
ChatBtn.Parent = OutrosContent
Instance.new("UICorner", ChatBtn).CornerRadius = UDim.new(0, 8)

ChatBtn.MouseButton1Click:Connect(function()
	pcall(function()
		game:GetService("StarterGui"):SetCoreGuiEnabled(Enum.CoreGuiType.Chat, true)
	end)
	pcall(function()
		game:GetService("StarterGui"):SetCore("ChatActive", true)
	end)
	ChatBtn.Text = "CHAT LIBERADO"
	ChatBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
	task.wait(1.5)
	ChatBtn.Text = "LIBERAR CHAT"
	ChatBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
end)

local function showTab(name)
	PatentesScroll.Visible = name == "Patentes"
	PerguntasScroll.Visible = name == "Perguntas"
	ParkourContent.Visible = name == "Parkour"
	JJsContent.Visible = name == "JJs"
	FarmContent.Visible = name == "Farm"
	OutrosContent.Visible = name == "Outros"
	ContentTitle.Text = name

	TabPatentes.BackgroundColor3 = name == "Patentes" and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(35, 35, 45)
	TabPerguntas.BackgroundColor3 = name == "Perguntas" and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(35, 35, 45)
	TabParkour.BackgroundColor3 = name == "Parkour" and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(35, 35, 45)
	TabJJs.BackgroundColor3 = name == "JJs" and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(35, 35, 45)
	TabFarm.BackgroundColor3 = name == "Farm" and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(35, 35, 45)
	TabOutros.BackgroundColor3 = name == "Outros" and Color3.fromRGB(0, 140, 255) or Color3.fromRGB(35, 35, 45)
end

TabPatentes.MouseButton1Click:Connect(function() showTab("Patentes") end)
TabPerguntas.MouseButton1Click:Connect(function() showTab("Perguntas") end)
TabParkour.MouseButton1Click:Connect(function() showTab("Parkour") end)
TabJJs.MouseButton1Click:Connect(function() showTab("JJs") end)
TabFarm.MouseButton1Click:Connect(function() showTab("Farm") end)
TabOutros.MouseButton1Click:Connect(function() showTab("Outros") end)
TabClose.MouseButton1Click:Connect(function() MainFrame.Visible = false end)
makeDraggable(MainFrame)

SubmitBtn.MouseButton1Click:Connect(function()
	if KeyBox.Text == correctKey then
		KeyFrame.Visible = false
		Ball.Visible = true
	else
		KeyBox.Text = ""
		KeyBox.PlaceholderText = "Key errada!"
	end
end)

Ball.MouseButton1Click:Connect(function()
	MainFrame.Visible = not MainFrame.Visible
	if MainFrame.Visible then
		showTab("Patentes")
	end
end)
