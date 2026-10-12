--[[
    JOGO: FREE FIRE MAX 🏆
    PAINEL: FFH4X REGEDIT FF
    LINGUAGEM: LUAU
    USO: Roblox Studio / ambiente de testes autorizado
    DESIGN: Personalizado no estilo PAINEL FREESTYLE (Free Fire)
]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

local HitboxEnabled = false
local ESPEnabled = false

-- Interface
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FFH4X_REGEDIT_FF"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

-- Painel Principal (Ajustado para 2 opções)
local Main = Instance.new("Frame")
Main.Name = "MainPanel"
Main.Size = UDim2.fromOffset(320, 295) 
Main.Position = UDim2.new(0.5, -160, 0.5, -147)
Main.BackgroundColor3 = Color3.fromRGB(10, 10, 10) 
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = Main

local Stroke = Instance.new("UIStroke")
Stroke.Color = Color3.fromRGB(0, 200, 0) 
Stroke.Thickness = 1.5
Stroke.Parent = Main

-- Cabeçalho (Barra superior)
local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 40)
Header.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Header.BorderSizePixel = 0
Header.Parent = Main

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = Header

-- Ícone e Título do Cabeçalho
local HeaderIcon = Instance.new("ImageLabel")
HeaderIcon.Size = UDim2.fromOffset(20, 20)
HeaderIcon.Position = UDim2.fromOffset(10, 10)
HeaderIcon.BackgroundTransparency = 1
HeaderIcon.Image = "rbxassetid://6031091004"
HeaderIcon.ImageColor3 = Color3.fromRGB(0, 255, 0)
HeaderIcon.Parent = Header

local HeaderTitle = Instance.new("TextLabel")
HeaderTitle.Size = UDim2.new(1, -40, 1, 0)
HeaderTitle.Position = UDim2.fromOffset(35, 0)
HeaderTitle.BackgroundTransparency = 1
HeaderTitle.Text = "PAINEL FREESTYLE - @ARMIN_14331"
HeaderTitle.TextColor3 = Color3.fromRGB(0, 255, 0) 
HeaderTitle.Font = Enum.Font.GothamBold
HeaderTitle.TextSize = 12
HeaderTitle.TextXAlignment = Enum.TextXAlignment.Left
HeaderTitle.Parent = Header

-- Botão de Fechar (X no canto superior direito)
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.fromOffset(30, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.BackgroundTransparency = 1
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 16
CloseButton.Parent = Header

-- Sub-cabeçalho (Informações do painel)
local SubHeader = Instance.new("Frame")
SubHeader.Size = UDim2.new(1, -20, 0, 45)
SubHeader.Position = UDim2.fromOffset(10, 45)
SubHeader.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
SubHeader.BorderSizePixel = 0
SubHeader.Parent = Main

local SubHeaderCorner = Instance.new("UICorner")
SubHeaderCorner.CornerRadius = UDim.new(0, 8)
SubHeaderCorner.Parent = SubHeader

local GameName = Instance.new("TextLabel")
GameName.Size = UDim2.new(1, -10, 0, 18)
GameName.Position = UDim2.fromOffset(5, 4)
GameName.BackgroundTransparency = 1
GameName.Text = "FREE FIRE MAX 🏆"
GameName.TextColor3 = Color3.fromRGB(255, 145, 45)
GameName.Font = Enum.Font.GothamBlack
GameName.TextSize = 14
GameName.Parent = SubHeader

local PanelName = Instance.new("TextLabel")
PanelName.Size = UDim2.new(1, -10, 0, 15)
PanelName.Position = UDim2.fromOffset(5, 22)
PanelName.BackgroundTransparency = 1
PanelName.Text = "FFH4X REGEDIT FF  |  Criado por: ARMIN_14331"
PanelName.TextColor3 = Color3.fromRGB(200, 200, 200)
PanelName.Font = Enum.Font.GothamBold
PanelName.TextSize = 10
PanelName.Parent = SubHeader

-- Barra de Abas (Personalizada)
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -20, 0, 30)
TabBar.Position = UDim2.fromOffset(10, 95)
TabBar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
TabBar.BorderSizePixel = 0
TabBar.Parent = Main

local TabCorner = Instance.new("UICorner")
TabCorner.CornerRadius = UDim.new(0, 6)
TabCorner.Parent = TabBar

local tabBtnPrincipal = Instance.new("TextButton")
tabBtnPrincipal.Size = UDim2.new(0, 75, 1, -4)
tabBtnPrincipal.Position = UDim2.new(0, 2, 0, 2)
tabBtnPrincipal.BackgroundColor3 = Color3.fromRGB(0, 180, 0)
tabBtnPrincipal.BorderSizePixel = 0
tabBtnPrincipal.Text = "Principal"
tabBtnPrincipal.TextColor3 = Color3.fromRGB(255, 255, 255)
tabBtnPrincipal.Font = Enum.Font.GothamBold
tabBtnPrincipal.TextSize = 10
tabBtnPrincipal.Parent = TabBar

local tCornerPrincipal = Instance.new("UICorner")
tCornerPrincipal.CornerRadius = UDim.new(0, 4)
tCornerPrincipal.Parent = tabBtnPrincipal

local tabTextInfo = Instance.new("TextLabel")
tabTextInfo.Size = UDim2.new(1, -85, 1, -4)
tabTextInfo.Position = UDim2.new(0, 80, 0, 2)
tabTextInfo.BackgroundTransparency = 1
tabTextInfo.Text = "mais opções chegaram"
tabTextInfo.TextColor3 = Color3.fromRGB(200, 200, 200)
tabTextInfo.Font = Enum.Font.GothamSemibold
tabTextInfo.TextSize = 10
tabTextInfo.TextXAlignment = Enum.TextXAlignment.Left
tabTextInfo.Parent = TabBar

-- Área de Opções (Lista de botões - Apenas 2 opções)
local OptionsFrame = Instance.new("Frame")
OptionsFrame.Size = UDim2.new(1, -20, 0, 115) 
OptionsFrame.Position = UDim2.fromOffset(10, 135)
OptionsFrame.BackgroundTransparency = 1
OptionsFrame.Parent = Main

-- Criador de botões no estilo do vídeo (Círculo + Texto)
local function CreateFreeFireToggle(text, positionY, initialState, callback)
    local ItemFrame = Instance.new("Frame")
    ItemFrame.Size = UDim2.new(1, 0, 0, 45)
    ItemFrame.Position = UDim2.fromOffset(0, positionY)
    ItemFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    ItemFrame.BorderSizePixel = 0
    ItemFrame.Parent = OptionsFrame

    local ItemCorner = Instance.new("UICorner")
    ItemCorner.CornerRadius = UDim.new(0, 8)
    ItemCorner.Parent = ItemFrame

    local Circle = Instance.new("Frame")
    Circle.Size = UDim2.fromOffset(16, 16)
    Circle.Position = UDim2.fromOffset(10, 14)
    Circle.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    Circle.BorderSizePixel = 0
    Circle.Parent = ItemFrame

    local CircleCorner = Instance.new("UICorner")
    CircleCorner.CornerRadius = UDim.new(1, 0)
    CircleCorner.Parent = Circle

    local Label = Instance.new("TextLabel")
    Label.Size = UDim2.new(1, -40, 1, 0)
    Label.Position = UDim2.fromOffset(35, 0)
    Label.BackgroundTransparency = 1
    Label.Text = text
    Label.TextColor3 = Color3.fromRGB(255, 255, 255)
    Label.Font = Enum.Font.GothamSemibold
    Label.TextSize = 13
    Label.TextXAlignment = Enum.TextXAlignment.Left
    Label.Parent = ItemFrame

    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(1, 0, 1, 0)
    Button.BackgroundTransparency = 1
    Button.Text = ""
    Button.Parent = ItemFrame

    local enabled = initialState

    local function Update()
        if enabled then
            Label.TextColor3 = Color3.fromRGB(0, 255, 0) 
            Circle.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        else
            Label.TextColor3 = Color3.fromRGB(255, 255, 255) 
            Circle.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
        end
    end

    Button.Activated:Connect(function()
        enabled = not enabled
        Update()
        callback(enabled)
    end)

    Update()
    return Button
end

-- ==========================================
-- MANTENDO A LÓGICA ORIGINAL INTACTA
-- ==========================================

-- Lógica de Hitbox
local OriginalSizes = {}

local function ApplyHitbox(player)
    if player == LocalPlayer then return end
    local char = player.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if hrp then
        if not OriginalSizes[player] then
            OriginalSizes[player] = hrp.Size
        end
        hrp.Size = Vector3.new(15, 15, 15)
        hrp.CanCollide = false
        hrp.Transparency = 0.5
    end
end

local function RemoveHitbox(player)
    local char = player.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if hrp then
        if OriginalSizes[player] then
            hrp.Size = OriginalSizes[player]
            OriginalSizes[player] = nil
        else
            hrp.Size = Vector3.new(2, 2, 1)
        end
        hrp.CanCollide = true
        hrp.Transparency = 1
    end
end

-- Opção 1: HITBOX (Aqui foi alterado o título para "HitBox")
CreateFreeFireToggle("HitBox", 0, false, function(state)
    HitboxEnabled = state
    for _, player in ipairs(Players:GetPlayers()) do
        if state then
            ApplyHitbox(player)
        else
            RemoveHitbox(player)
        end
    end
end)

-- Opção 2: ESP (Aqui foi alterado o título para "ESP")
CreateFreeFireToggle("ESP", 55, false, function(state)
    ESPEnabled = state
end)

-- Botão de Fechar Painel (Ajustado para cima)
local CloseButtonPanel = Instance.new("TextButton")
CloseButtonPanel.Size = UDim2.new(1, -28, 0, 32)
CloseButtonPanel.Position = UDim2.fromOffset(14, 255) 
CloseButtonPanel.BackgroundColor3 = Color3.fromRGB(115, 43, 43)
CloseButtonPanel.Text = "FECHAR PAINEL"
CloseButtonPanel.TextColor3 = Color3.new(1, 1, 1)
CloseButtonPanel.Font = Enum.Font.GothamBold
CloseButtonPanel.TextSize = 12
CloseButtonPanel.Parent = Main

local CloseCornerPanel = Instance.new("UICorner")
CloseCornerPanel.CornerRadius = UDim.new(0, 8)
CloseCornerPanel.Parent = CloseButtonPanel

CloseButtonPanel.Activated:Connect(function()
    ScreenGui:Destroy()
end)

-- Botão de Fechar do Cabeçalho (X)
CloseButton.Activated:Connect(function()
    ScreenGui:Destroy()
end)

-- ==========================================
-- LÓGICA DO ESP DE DEPURAÇÃO (BOX E ARCO-ÍRIS)
-- ==========================================
local Tracked = {}

local function RemoveESP(player)
    local data = Tracked[player]
    if not data then return end

    if data.Highlight then data.Highlight:Destroy() end
    if data.Billboard then data.Billboard:Destroy() end

    Tracked[player] = nil
end

local function SetupESP(player)
    if player == LocalPlayer or Tracked[player] then return end

    local character = player.Character
    if not character then return end

    local head = character:FindFirstChild("Head")
    if not head then return end

    local highlight = Instance.new("Highlight")
    highlight.Name = "FFH4X_DebugHighlight"
    highlight.Adornee = character
    highlight.FillTransparency = 1 
    highlight.OutlineTransparency = 0 
    highlight.OutlineColor = Color3.fromRGB(255, 255, 255) 
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop 
    highlight.Enabled = false
    highlight.Parent = character

    local billboard = Instance.new("BillboardGui")
    billboard.Name = "FFH4X_DebugLabel"
    billboard.Adornee = head
    billboard.Size = UDim2.fromOffset(190, 35)
    billboard.StudsOffset = Vector3.new(0, 2.5, 0)
    billboard.AlwaysOnTop = true
    billboard.Enabled = false
    billboard.Parent = PlayerGui

    local label = Instance.new("TextLabel")
    label.Name = "Info"
    label.Size = UDim2.fromScale(1, 1)
    label.BackgroundTransparency = 1
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextStrokeTransparency = 0.3
    label.Font = Enum.Font.GothamBold
    label.TextSize = 12
    label.Parent = billboard

    Tracked[player] = {
        Highlight = highlight,
        Billboard = billboard,
        Label = label
    }
end

local function UpdateESP(player)
    local data = Tracked[player]
    if not data then return end

    local character = player.Character
    local head = character and character:FindFirstChild("Head")
    local root = character and character:FindFirstChild("HumanoidRootPart")

    local myCharacter = LocalPlayer.Character
    local myRoot = myCharacter and myCharacter:FindFirstChild("HumanoidRootPart")

    local enabled = ESPEnabled and root ~= nil and head ~= nil

    data.Highlight.Enabled = enabled
    data.Billboard.Enabled = enabled -- Agora Nomes e Distância estão embutidos no ESP

    if not enabled then return end

    -- EFEITO ARCO-ÍRIS (Colorido Mudando)
    local hue = tick() % 1
    local rainbowColor = Color3.fromHSV(hue, 1, 1)
    data.Highlight.OutlineColor = rainbowColor
    data.Label.TextColor3 = rainbowColor

    local parts = {}
    -- Sempre mostra o nome
    table.insert(parts, player.DisplayName)

    -- Sempre mostra a distância
    if myRoot then
        local distance = (root.Position - myRoot.Position).Magnitude
        -- AQUI FOI FEITA A ALTERAÇÃO: De "%d studs" para "%d De Distância"
        table.insert(parts, string.format("%d De Distância", distance))
    end

    data.Label.Text = table.concat(parts, " | ")
end

local function TrackPlayer(player)
    player.CharacterAdded:Connect(function()
        task.wait(1)
        RemoveESP(player)
        SetupESP(player)
        
        if HitboxEnabled then
            ApplyHitbox(player)
        end
    end)

    if player.Character then
        SetupESP(player)
    end
end

for _, player in Players:GetPlayers() do
    TrackPlayer(player)
end

Players.PlayerAdded:Connect(TrackPlayer)
Players.PlayerRemoving:Connect(function(player)
    RemoveESP(player)
    OriginalSizes[player] = nil
end)

RunService.RenderStepped:Connect(function()
    for player in pairs(Tracked) do
        UpdateESP(player)
    end
end)

print("FREE FIRE MAX 🏆 | FFH4X REGEDIT FF carregado! - Painel Finalizado") 
