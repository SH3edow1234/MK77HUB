-- Blox Fruits Script Avançado (Compatível com Executor CODEX 2.660 Mobile)

-- Configurações Avançadas
local autoFarmEnabled = false
local autoFruitSniperEnabled = false
local autoFarmChestEnabled = false
local fruitRainEnabled = false
local autoQuestEnabled = false
local autoRaidEnabled = false
local autoTrialsEnabled = false

-- Detecção de Mundo (Blox Fruits)
local currentSea = 1

local function detectSea()
    -- Lógica simplificada para detecção de Sea no CODEX Mobile
    -- Exemplo: Verificar a posição do jogador em relação a áreas conhecidas
    return 1
end

currentSea = detectSea()

-- Funções Auxiliares Simplificadas (Adaptadas para CODEX Mobile)
local function findNearest(objects, position, maxDistance)
    local nearest = nil
    local nearestDistance = maxDistance or math.huge
    for _, obj in ipairs(objects) do
        if obj and obj.PrimaryPart and obj.PrimaryPart.Position then
            local distance = (obj.PrimaryPart.Position - position).Magnitude
            if distance < nearestDistance then
                nearest = obj
                nearestDistance = distance
            end
        end
    end
    return nearest
end

local function moveTo(position)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character:FindFirstChild("HumanoidRootPart").CFrame = CFrame.new(position)
    end
end

local function attack(target)
    -- Lógica de ataque simplificada para CODEX Mobile
    if player and player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid:EquipTool(player.Character:FindFirstChildOfClass("Tool"))
        player.Character.Humanoid:UseTool()
    end
end

local function collectFruit(fruit)
    -- Lógica de coleta de fruta simplificada para CODEX Mobile
    fruit:Destroy()
end

local function openChest(chest)
    -- Lógica de abertura de baú simplificada para CODEX Mobile
    chest:Destroy()
end

local function getQuestFromNPC(npcName)
    -- Lógica de quest simplificada para CODEX Mobile
    local npc = workspace:FindFirstChild(npcName)
    if npc then
        moveTo(npc.PrimaryPart.Position)
        -- Simulação de diálogo (substituir por lógica real)
        print("Quest iniciada com " .. npcName)
    end
end

local function returnToFarming(monsterName)
    -- Lógica de retorno ao farm simplificada para CODEX Mobile
    local monster = workspace:FindFirstChild(monsterName)
    if monster then
        moveTo(monster.PrimaryPart.Position)
    end
end

local function startRaid()
    -- Lógica de Raid simplificada para CODEX Mobile
    print("Iniciando Raid (simulação)")
end

local function completeTrials()
    -- Lógica de Trials simplificada para CODEX Mobile
    print("Completando Trials (simulação)")
end

-- Lógica de Quest (Blox Fruits)
local Mon, LevelQuest, NameQuest, NameMon, CFrameQuest, CFrameMon

if currentSea == 1 then
    if myLevel >= 1 and myLevel <= 9 then
        Mon = "Bandit"
        LevelQuest = 1
        NameQuest = "BanditQuest1"
        NameMon = "Bandit"
        CFrameQuest = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
        CFrameMon = CFrame.new(1045.962646484375, 27.00250816345215, 1560.8203125)
    elseif myLevel >= 175 and myLevel <= 189 then
        Mon = "Dark Master"
        LevelQuest = 2
        NameQuest = "SkyQuest"
        NameMon = "Dark Master"
        CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
        CFrameMon = CFrame.new(-4582.47412109375, 786.3787841796875, -2413.513427734375)
    end
elseif currentSea == 2 then
    -- Adicione a lógica de quest para Sea 2 aqui
elseif currentSea == 3 then
    -- Adicione a lógica de quest para Sea 3 aqui
end

-- Auto Farm (Blox Fruits)
if autoFarmEnabled and Mon then
    local monster = findNearest(workspace:GetDescendants(), player.Character.HumanoidRootPart.Position, 50)
    if monster and monster.Name == NameMon then
        moveTo(monster.PrimaryPart.Position)
        attack(monster)
    end
end

-- Auto Fruit Sniper (Blox Fruits)
if autoFruitSniperEnabled then
    local fruit = findNearest(workspace:GetDescendants(), player.Character.HumanoidRootPart.Position, 100)
    if fruit and fruit:IsA("BasePart") and fruit.Name:lower():find("fruit") then
        moveTo(fruit.Position)
        collectFruit(fruit)
    end
end

-- Auto Farm Chest (Blox Fruits)
if autoFarmChestEnabled then
    local chest = findNearest(workspace:GetDescendants(), player.Character.HumanoidRootPart.Position, 100)
    if chest and chest:IsA("Model") and chest.Name:lower():find("chest") then
        moveTo(chest.PrimaryPart.Position)
        openChest(chest)
    end
end

-- ESP de Chuva de Frutas (Blox Fruits)
if fruitRainEnabled then
    local endTime = tick() + fruitRainDuration
    while tick() < endTime do
        local fruitName = "Apple" -- Fruta padrão para CODEX Mobile
        local fruit = Instance.new("Part")
        fruit.Name = fruitName
        fruit.Anchored = true
        fruit.Position = Vector3.new(math.random(-100, 100), 100, math.random(-100, 100))
        fruit.Parent = workspace
        wait(0.5)
    end
end

-- Auto Quest (Blox Fruits)
if autoQuestEnabled then
    getQuestFromNPC(NameMon .. " Quest Giver")
    wait(5)
    returnToFarming(NameMon)
end

-- Auto Raid (Blox Fruits)
if autoRaidEnabled then
    startRaid()
end

-- Auto Trials (Blox Fruits)
if autoTrialsEnabled then
    completeTrials()
end

-- IU Simplificada para CODEX Mobile
if player and player.PlayerGui then
    local screenGui = Instance.new("ScreenGui")
    screenGui.Parent = player.PlayerGui

    local function createButton(text, variable, yPosition)
        local button = Instance.new("TextButton")
        button.Parent = screenGui
        button.Size = UDim2.new(0, 150, 0, 30)
        button.Position = UDim2.new(0.05, 0, 0.05 + yPosition * 0.05, 0)
        button.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
        button.Text = text .. ": " .. (variable and "Ligado" or "Desligado")
        button.MouseButton1Click:Connect(function()
            variable = not variable
            button.Text = text .. ": " .. (variable and "Ligado" or "Desligado")
        end)
        return button
    end

    createButton("Auto Farm", autoFarmEnabled, 0).MouseButton1Click:Connect(function() autoFarmEnabled = not autoFarmEnabled end)
    createButton("Fruit Sniper", autoFruitSniperEnabled, 1).MouseButton1Click:Connect(
