--[[
    JOGO: FREE FIRE MAX 🏆
    PAINEL: FFH4X REGEDIT FF
    LINGUAGEM: LUAU
    USO: Roblox Studio / ambiente de testes autorizado
    DESIGN: Painel Verde em pé, esticado, com barra de categorias
    OPÇÕES: Hitbox e ESP (com nome e distância juntos)
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

local Main = Instance.new("Frame")
Main.Name = "MainPanel"
Main.Size = UDim2.fromOffset(320, 330) 
Main.Position = UDim2.new(0.5, -160, 0.5, -165)
Main.BackgroundColor3 = Color3.fromRGB(18, 20, 28)
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 14)
MainCorner.Parent = Main

local Stroke = Instance.new("UIStroke")
Stroke.Color = Color3.fromRGB(0, 200, 0) 
Stroke.Thickness = 1.5
Stroke.Parent = Main

-- Cabeçalho (Topo)
local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 82)
Header.BackgroundColor3 = Color3.fromRGB(29, 32, 43)
Header.BorderSizePixel = 0
Header.Parent = Main

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 14)
HeaderCorner.Parent = Header

local GameName = Instance.new("TextLabel")
GameName.Size = UDim2.new(1, -20, 0, 28)
GameName.Position = UDim2.fromOffset(10, 7)
GameName.BackgroundTransparency = 1
GameName.Text = "FREE FIRE MAX 🏆"
GameName.TextColor3 = Color3.fromRGB(255, 145, 45)
GameName.Font = Enum.Font.GothamBlack
GameName.TextSize = 20
GameName.Parent = Header

local PanelName = Instance.new("TextLabel")
PanelName.Size = UDim2.new(1, -20, 0, 22)
PanelName.Position = UDim2.fromOffset(10, 38)
PanelName.BackgroundTransparency = 1
PanelName.Text = "FFH4X REGEDIT FF"
PanelName.TextColor3 = Color3.fromRGB(240, 240, 245)
PanelName.Font = Enum.Font.GothamBold
PanelName.TextSize = 15
PanelName.Parent = Header

local Subtitle = Instance.new("TextLabel")
Subtitle.Size = UDim2.new(1, -20, 0, 15)
Subtitle.Position = UDim2.fromOffset(10, 61)
Subtitle.BackgroundTransparency = 1
Subtitle.Text = "PAINEL DE TESTES • LUAU"
Subtitle.TextColor3 = Color3.fromRGB(155, 160, 175)
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextSize = 10
Subtitle.Parent = Header

-- Barra de Categorias (Abas)
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

-- Área de Opções
local OptionsFrame = Instance.new("Frame")
OptionsFrame.Size = UDim2.new(1, -20, 0, 120) 
OptionsFrame.Position = UDim2.fromOffset(10, 135)
OptionsFrame.BackgroundTransparency = 1
OptionsFrame.Parent = Main

-- Criador de botões
local function CreateToggle(text, positionY, initialState, callback)
    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(1, 0, 0, 50)
    Button.Position = UDim2.fromOffset(0, positionY)
    Button.BackgroundColor3 = Color3.fromRGB(39, 43, 56)
    Button.BorderSizePixel = 0
    Button.AutoButtonColor = true
    Button.Font = Enum.Font.GothamSemibold
    Button.TextSize = 14
    Button.TextColor3 = Color3.fromRGB(245, 245, 250)
    Button.Parent = OptionsFrame

    local Corner = Instance.new("UICorner")
    Corner.CornerRadius = UDim.new(0, 8)
    Corner.Parent = Button

    local enabled = initialState

    local function Update()
        Button.Text = text .. "   [" .. (enabled and "ON" or "OFF") .. "]"
        Button.BackgroundColor3 = enabled
            and Color3.fromRGB(0, 150, 0)
            or Color3.fromRGB(39, 43, 56)
    end

    Button.Activated:Connect(function()
        enabled = not enabled
        Update()
        callback(enabled)
    end)

    Update()
    return Button
end

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

-- Opção 1: HITBOX
CreateToggle("HITBOX EXPANDER • 15", 0, false, function(state)
    HitboxEnabled = state
    for _, player in ipairs(Players:GetPlayers()) do
        if state then
            ApplyHitbox(player)
        else
            RemoveHitbox(player)
        end
    end
end)

-- Opção 2: ESP (nome e distância juntos)
CreateToggle("ESP / BOX + NOME + DISTÂNCIA", 60, false, function(state)
    ESPEnabled = state
end)

-- Botão de Fechar Painel
local CloseButtonPanel = Instance.new("TextButton")
CloseButtonPanel.Size = UDim2.new(1, -28, 0, 32)
CloseButtonPanel.Position = UDim2.fromOffset(14, 285) 
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

-- ESP de depuração (corpo + nome + distância)
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
    highlight.FillTransparency = 0.3
    highlight.OutlineTransparency = 1
    highlight.FillColor = Color3.fromRGB(0, 255, 0)
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
    label.TextColor3 = Color3.fromRGB(0, 255, 0)
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
    data.Billboard.Enabled = enabled

    if not enabled then return end

    if HitboxEnabled and root then
        root.Transparency = 1
    end

    local parts = {}
    table.insert(parts, player.DisplayName)

    if myRoot then
        local distance = (root.Position - myRoot.Position).Magnitude
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

print("FREE FIRE MAX 🏆 | FFH4X REGEDIT FF carregado! - Painel Verde em pé")
