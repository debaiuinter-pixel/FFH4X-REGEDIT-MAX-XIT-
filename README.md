--[[
    VERSÃO ULTRA-LEVE PARA DELTA EXECUTOR
    ALTERAÇÃO: Painel horizontal (deitado) + Título da Hitbox encurtado
]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local LocalPlayer = Players.LocalPlayer

-- Variáveis
local HitboxEnabled = false
local ESPEnabled = false
local InfJumpEnabled = false
local SpinningEnabled = false
local SpeedEnabled = false
local CurrentSpeed = 16
local SpinAngle = 0
local SPIN_SPEED = 720

-- ==========================================
-- 1. CRIA A INTERFACE PRIMEIRO
-- ==========================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "PainelDeltaLeve"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.DisplayOrder = 999
ScreenGui.Parent = game:GetService("CoreGui")

-- Botão de Abrir
local OpenBtn = Instance.new("TextButton")
OpenBtn.Size = UDim2.fromOffset(55, 55)
OpenBtn.Position = UDim2.new(0.5, -27, 0.5, -27)
OpenBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
OpenBtn.Text = ""
OpenBtn.Active = true
OpenBtn.Draggable = true
OpenBtn.Parent = ScreenGui
OpenBtn.Visible = true

local OpenBtnCorner = Instance.new("UICorner")
OpenBtnCorner.CornerRadius = UDim.new(0, 10)
OpenBtnCorner.Parent = OpenBtn

-- Emoji de Caveira
local SkullEmoji = Instance.new("TextLabel")
SkullEmoji.Size = UDim2.new(1, 0, 0, 30)
SkullEmoji.Position = UDim2.new(0, 0, 0, 2)
SkullEmoji.BackgroundTransparency = 1
SkullEmoji.Text = "💀"
SkullEmoji.TextColor3 = Color3.fromRGB(255, 255, 255)
SkullEmoji.Font = Enum.Font.GothamBlack
SkullEmoji.TextSize = 24
SkullEmoji.Parent = OpenBtn

-- Nome FFH4X
local NomeFF = Instance.new("TextLabel")
NomeFF.Size = UDim2.new(0.5, 0, 0, 16)
NomeFF.Position = UDim2.new(0, 0, 1, -18)
NomeFF.BackgroundTransparency = 1
NomeFF.Text = "FF"
NomeFF.TextColor3 = Color3.fromRGB(255, 0, 0)
NomeFF.Font = Enum.Font.GothamBlack
NomeFF.TextSize = 14
NomeFF.TextXAlignment = Enum.TextXAlignment.Right
NomeFF.Parent = OpenBtn

local NomeH4X = Instance.new("TextLabel")
NomeH4X.Size = UDim2.new(0.5, 0, 0, 16)
NomeH4X.Position = UDim2.new(0.5, 0, 1, -18)
NomeH4X.BackgroundTransparency = 1
NomeH4X.Text = "H4X"
NomeH4X.TextColor3 = Color3.fromRGB(255, 255, 255)
NomeH4X.Font = Enum.Font.GothamBlack
NomeH4X.TextSize = 14
NomeH4X.TextXAlignment = Enum.TextXAlignment.Left
NomeH4X.Parent = OpenBtn

-- Painel Principal (HORIZONTAL - DEITADO)
local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(520, 260)
Main.Position = UDim2.new(0.5, -260, 0.5, -130)
Main.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
Main.BorderSizePixel = 2
Main.BorderColor3 = Color3.fromRGB(200, 0, 0)
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui
Main.Visible = false

-- Barra Vermelha do Topo
local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 30)
TopBar.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
TopBar.BorderSizePixel = 0
TopBar.Parent = Main

-- Título
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundTransparency = 1
Title.Text = "PAINEL FREESTYLE"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 16
Title.Parent = TopBar

-- Botão de Fechar (X do Painel)
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.fromOffset(30, 30)
CloseBtn.Position = UDim2.new(1, -35, 0, 0)
CloseBtn.BackgroundTransparency = 1
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 18
CloseBtn.Parent = TopBar

-- ==========================================
-- 2. LAYOUT HORIZONTAL
-- ==========================================

-- Coluna Esquerda (Categoria "Início")
local LeftColumn = Instance.new("Frame")
LeftColumn.Size = UDim2.new(0, 100, 1, -70)
LeftColumn.Position = UDim2.fromOffset(5, 35)
LeftColumn.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
LeftColumn.BorderSizePixel = 0
LeftColumn.Parent = Main

local LeftCorner = Instance.new("UICorner")
LeftCorner.CornerRadius = UDim.new(0, 6)
LeftCorner.Parent = LeftColumn

local BtnInicio = Instance.new("TextButton")
BtnInicio.Size = UDim2.new(1, -10, 0, 35)
BtnInicio.Position = UDim2.fromOffset(5, 5)
BtnInicio.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
BtnInicio.Text = "Início"
BtnInicio.TextColor3 = Color3.fromRGB(255, 255, 255)
BtnInicio.Font = Enum.Font.GothamBold
BtnInicio.TextSize = 13
BtnInicio.Parent = LeftColumn

local BtnInicioCorner = Instance.new("UICorner")
BtnInicioCorner.CornerRadius = UDim.new(0, 6)
BtnInicioCorner.Parent = BtnInicio

local TextoAviso = Instance.new("TextLabel")
TextoAviso.Size = UDim2.new(1, -10, 0, 40)
TextoAviso.Position = UDim2.fromOffset(5, 50)
TextoAviso.BackgroundTransparency = 1
TextoAviso.Text = "Mais opções irão chegar!"
TextoAviso.TextColor3 = Color3.fromRGB(200, 200, 200)
TextoAviso.Font = Enum.Font.GothamSemibold
TextoAviso.TextSize = 10
TextoAviso.TextWrapped = true
TextoAviso.Parent = LeftColumn

-- Coluna Central (Opções 1, 2, 3)
local CenterColumn = Instance.new("Frame")
CenterColumn.Size = UDim2.new(0, 205, 1, -70)
CenterColumn.Position = UDim2.new(0, 110, 0, 35)
CenterColumn.BackgroundTransparency = 1
CenterColumn.Parent = Main

-- Coluna Direita (Opções 4, 5)
local RightColumn = Instance.new("Frame")
RightColumn.Size = UDim2.new(0, 200, 1, -70)
RightColumn.Position = UDim2.new(0, 320, 0, 35)
RightColumn.BackgroundTransparency = 1
RightColumn.Parent = Main

-- ==========================================
-- 3. LÓGICA DOS BOTÕES
-- ==========================================

local function CriarBotao(texto, parente, posY, callback)
    local Btn = Instance.new("TextButton")
    Btn.Size = UDim2.new(1, -10, 0, 40)
    Btn.Position = UDim2.fromOffset(5, posY)
    Btn.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    Btn.Text = texto .. " [OFF]"
    Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    Btn.Font = Enum.Font.GothamSemibold
    Btn.TextSize = 12
    Btn.Parent = parente

    local BtnCorner = Instance.new("UICorner")
    BtnCorner.CornerRadius = UDim.new(0, 6)
    BtnCorner.Parent = Btn
    
    local ativo = false
    Btn.MouseButton1Click:Connect(function()
        ativo = not ativo
        if ativo then
            Btn.Text = texto .. " [ON]"
            Btn.TextColor3 = Color3.fromRGB(0, 255, 0)
        else
            Btn.Text = texto .. " [OFF]"
            Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        end
        callback(ativo)
    end)
    return Btn
end

-- Função central para aplicar Hitbox
local function AplicarEfeitos(p)
    if p == LocalPlayer then return end
    local char = p.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    
    if hrp then
        if HitboxEnabled then
            hrp.Size = Vector3.new(21, 21, 21)
            hrp.CanCollide = false
            if ESPEnabled then
                hrp.Transparency = 1
            else
                hrp.Transparency = 0.5
            end
        else
            hrp.Size = Vector3.new(2, 2, 1)
            hrp.CanCollide = true
            hrp.Transparency = 1
        end
    end
end

-- 1. Hitbox (TÍTULO ENCURTADO)
CriarBotao("HitBox (Com Expansão Invisível)", CenterColumn, 5, function(state)
    HitboxEnabled = state
    for _, p in ipairs(Players:GetPlayers()) do
        AplicarEfeitos(p)
    end
end)

-- 2. ESP
CriarBotao("ESP", CenterColumn, 50, function(state)
    ESPEnabled = state
    for _, p in ipairs(Players:GetPlayers()) do
        AplicarEfeitos(p)
    end
end)

-- 3. Speed
local SpeedFrame = Instance.new("Frame")
SpeedFrame.Size = UDim2.new(1, -10, 0, 40)
SpeedFrame.Position = UDim2.fromOffset(5, 95)
SpeedFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
SpeedFrame.Parent = CenterColumn

local SpeedCorner = Instance.new("UICorner")
SpeedCorner.CornerRadius = UDim.new(0, 6)
SpeedCorner.Parent = SpeedFrame

local SpeedBtn = Instance.new("TextButton")
SpeedBtn.Size = UDim2.new(0, 130, 1, 0)
SpeedBtn.BackgroundTransparency = 1
SpeedBtn.Text = "Speed (Com \"Fake lag\") [OFF]"
SpeedBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedBtn.Font = Enum.Font.GothamSemibold
SpeedBtn.TextSize = 10
SpeedBtn.Parent = SpeedFrame

local SpeedInput = Instance.new("TextBox")
SpeedInput.Size = UDim2.new(0, 55, 0, 28)
SpeedInput.Position = UDim2.new(1, -60, 0.5, -14)
SpeedInput.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
SpeedInput.TextColor3 = Color3.fromRGB(0, 255, 0)
SpeedInput.Text = "16"
SpeedInput.Font = Enum.Font.GothamBold
SpeedInput.TextSize = 12
SpeedInput.Parent = SpeedFrame

SpeedInput.FocusLost:Connect(function()
    local val = tonumber(SpeedInput.Text)
    if val then
        val = math.clamp(val, 16, 130)
        SpeedInput.Text = tostring(val)
        CurrentSpeed = val
        if SpeedEnabled then
            local char = LocalPlayer.Character
            if char then
                local hum = char:FindFirstChildOfClass("Humanoid")
                if hum then hum.WalkSpeed = CurrentSpeed end
            end
        end
    else
        SpeedInput.Text = "16"
        CurrentSpeed = 16
    end
end)

SpeedBtn.MouseButton1Click:Connect(function()
    SpeedEnabled = not SpeedEnabled
    if SpeedEnabled then
        SpeedBtn.Text = "Speed (Com \"Fake lag\") [ON]"
        SpeedBtn.TextColor3 = Color3.fromRGB(0, 255, 0)
        local char = LocalPlayer.Character
        if char then
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hum then hum.WalkSpeed = CurrentSpeed end
        end
    else
        SpeedBtn.Text = "Speed (Com \"Fake lag\") [OFF]"
        SpeedBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
        local char = LocalPlayer.Character
        if char then
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hum then hum.WalkSpeed = 16 end
        end
    end
end)

-- 4. Infinity Jump (Vai para a coluna da direita)
CriarBotao("Infinity Jump", RightColumn, 5, function(state)
    InfJumpEnabled = state
end)

-- 5. Movimentação Giratória (Vai para a coluna da direita)
CriarBotao("Mov. Giratória (Spin)", RightColumn, 50, function(state)
    SpinningEnabled = state
    if not state then
        local char = LocalPlayer.Character
        if char then
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hum then hum.AutoRotate = true end
        end
    end
end)

-- Botão de Fechar Painel (Embaixo, ocupando toda a largura)
local ClosePanelBtn = Instance.new("TextButton")
ClosePanelBtn.Size = UDim2.new(1, -20, 0, 30)
ClosePanelBtn.Position = UDim2.new(0, 10, 1, -35)
ClosePanelBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
ClosePanelBtn.Text = "FECHAR PAINEL"
ClosePanelBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ClosePanelBtn.Font = Enum.Font.GothamBold
ClosePanelBtn.TextSize = 12
ClosePanelBtn.Parent = Main

local ClosePanelCorner = Instance.new("UICorner")
ClosePanelCorner.CornerRadius = UDim.new(0, 6)
ClosePanelCorner.Parent = ClosePanelBtn

CloseBtn.MouseButton1Click:Connect(function()
    Main.Visible = false
    OpenBtn.Visible = true
end)

ClosePanelBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

OpenBtn.MouseButton1Click:Connect(function()
    OpenBtn.Visible = false
    Main.Visible = true
end)

-- ==========================================
-- 4. LÓGICA DO JOGO (LEVE)
-- ==========================================

UserInputService.JumpRequest:Connect(function()
    if InfJumpEnabled then
        local char = LocalPlayer.Character
        if char then
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if hrp then
                hrp.AssemblyLinearVelocity = Vector3.new(hrp.AssemblyLinearVelocity.X, 60, hrp.AssemblyLinearVelocity.Z)
            end
        end
    end
end)

task.spawn(function()
    while task.wait(0.5) do
        if SpeedEnabled then
            local char = LocalPlayer.Character
            if char then
                local hum = char:FindFirstChildOfClass("Humanoid")
                if hum and hum.WalkSpeed ~= CurrentSpeed then
                    hum.WalkSpeed = CurrentSpeed
                end
            end
        end
    end
end)

-- ESP (Atualiza a cada 0.1s para não pesar)
local Tracked = {}

local function SetupESP(p)
    if p == LocalPlayer or Tracked[p] then return end
    local char = p.Character
    if not char then return end
    local head = char:FindFirstChild("Head")
    if not head then return end
    
    local hl = Instance.new("Highlight")
    hl.Adornee = char
    hl.FillTransparency = 0.3
    hl.OutlineTransparency = 1
    hl.FillColor = Color3.fromRGB(255, 255, 255)
    hl.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    hl.Enabled = false
    hl.Parent = char
    
    local bb = Instance.new("BillboardGui")
    bb.Adornee = head
    bb.Size = UDim2.fromOffset(190, 55)
    bb.StudsOffset = Vector3.new(0, 3.5, 0)
    bb.AlwaysOnTop = true
    bb.Enabled = false
    bb.Parent = ScreenGui
    
    local txt = Instance.new("TextLabel")
    txt.Name = "NameLabel"
    txt.Size = UDim2.new(1, 0, 0, 20)
    txt.Position = UDim2.new(0, 0, 0, 0)
    txt.BackgroundTransparency = 1
    txt.TextColor3 = Color3.fromRGB(255, 255, 255)
    txt.TextStrokeTransparency = 0.3
    txt.Font = Enum.Font.GothamBold
    txt.TextSize = 12
    txt.Parent = bb

    local hpBarBg = Instance.new("Frame")
    hpBarBg.Name = "HPBarBg"
    hpBarBg.Size = UDim2.new(0, 100, 0, 6)
    hpBarBg.Position = UDim2.new(0.5, -50, 0, 22)
    hpBarBg.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    hpBarBg.BorderSizePixel = 0
    hpBarBg.Parent = bb

    local hpBarFill = Instance.new("Frame")
    hpBarFill.Name = "HPBarFill"
    hpBarFill.Size = UDim2.new(1, 0, 1, 0)
    hpBarFill.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
    hpBarFill.BorderSizePixel = 0
    hpBarFill.Parent = hpBarBg

    local hpText = Instance.new("TextLabel")
    hpText.Name = "HPText"
    hpText.Size = UDim2.new(1, 0, 0, 14)
    hpText.Position = UDim2.new(0, 0, 0, 30)
    hpText.BackgroundTransparency = 1
    hpText.TextColor3 = Color3.fromRGB(255, 255, 255)
    hpText.TextStrokeTransparency = 0.3
    hpText.Font = Enum.Font.GothamBold
    hpText.TextSize = 11
    hpText.Parent = bb
    
    Tracked[p] = {Highlight = hl, Billboard = bb, Label = txt, HPBar = hpBarFill, HPText = hpText}
end

local function RemoveESP(p)
    if Tracked[p] then
        Tracked[p].Highlight:Destroy()
        Tracked[p].Billboard:Destroy()
        Tracked[p] = nil
    end
end

task.spawn(function()
    while task.wait(1) do
        for _, p in ipairs(Players:GetPlayers()) do
            if p ~= LocalPlayer then
                local char = p.Character
                if char and HitboxEnabled then
                    AplicarEfeitos(p)
                end
                if char then
                    local hasHighlight = char:FindFirstChildOfClass("Highlight")
                    if not hasHighlight and not Tracked[p] then
                        SetupESP(p)
                    end
                else
                    if Tracked[p] then
                        RemoveESP(p)
                    end
                end
            end
        end
    end
end)

task.spawn(function()
    while task.wait(0.1) do
        for p, data in pairs(Tracked) do
            local char = p.Character
            local head = char and char:FindFirstChild("Head")
            local root = char and char:FindFirstChild("HumanoidRootPart")
            local hum = char and char:FindFirstChildOfClass("Humanoid")
            local myChar = LocalPlayer.Character
            local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
            
            local enabled = ESPEnabled and root and head and hum
            data.Highlight.Enabled = enabled
            data.Billboard.Enabled = enabled
            
            if enabled then
                if HitboxEnabled and root then
                    root.Transparency = 1
                end
                
                local hue = tick() % 1
                local color = Color3.fromHSV(hue, 1, 1)
                data.Highlight.FillColor = color
                data.Label.TextColor3 = color
                
                local dist = myRoot and (root.Position - myRoot.Position).Magnitude or 0
                data.Label.Text = p.DisplayName .. " | " .. math.floor(dist) .. " De Distância"
                
                local health = hum.Health
                local maxHealth = hum.MaxHealth
                local percent = math.clamp(health / maxHealth, 0, 1)
                
                data.HPBar.Size = UDim2.new(percent, 0, 1, 0)
                data.HPText.Text = math.floor(health) .. " / " .. math.floor(maxHealth)
                
                if percent > 0.75 then
                    data.HPBar.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
                elseif percent > 0.50 then
                    data.HPBar.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
                elseif percent > 0.29 then
                    data.HPBar.BackgroundColor3 = Color3.fromRGB(255, 165, 0)
                elseif percent > 0 then
                    data.HPBar.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
                else
                    data.HPBar.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
                end
            end
        end
    end
end)

RunService.RenderStepped:Connect(function(dt)
    if SpinningEnabled then
        local char = LocalPlayer.Character
        if char then
            local hrp = char:FindFirstChild("HumanoidRootPart")
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hrp and hum then
                if hum.MoveDirection.Magnitude > 0 then
                    hum.AutoRotate = false
                    SpinAngle = SpinAngle + (SPIN_SPEED * dt)
                    local moveDir = hum.MoveDirection
                    local baseCFrame = CFrame.lookAt(hrp.Position, hrp.Position + moveDir)
                    hrp.CFrame = baseCFrame * CFrame.Angles(0, math.rad(SpinAngle), 0)
                else
                    hum.AutoRotate = true
                    SpinAngle = 0
                end
            end
        end
    end
end)

print("Painel Ultra-Leve carregado com sucesso no Delta! - Painel horizontal + Hitbox encurtada")
