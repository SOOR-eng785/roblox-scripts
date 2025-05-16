local gui = Instance.new("ScreenGui", game.CoreGui)

-- زر الفتح الرئيسي
local open = Instance.new("TextButton", gui)
open.Size = UDim2.new(0, 80, 0, 80)
open.Position = UDim2.new(1, -100, 0.4, -40)
open.Text = "👾👾 XSOORX 👾👾"
open.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
open.TextColor3 = Color3.fromRGB(255, 255, 255)
open.Font = Enum.Font.GothamBold
open.TextSize = 18
Instance.new("UICorner", open).CornerRadius = UDim.new(1, 0)

local openStroke = Instance.new("UIStroke", open)
openStroke.Thickness = 2
openStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

-- القائمة الرئيسية
local menu = Instance.new("Frame", gui)
menu.Size = UDim2.new(0, 300, 0, 300)
menu.Position = UDim2.new(1, -320, 0.5, -150)
menu.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
menu.Visible = false
Instance.new("UICorner", menu).CornerRadius = UDim.new(0, 12)

local stroke = Instance.new("UIStroke", menu)
stroke.Thickness = 4
stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
stroke.Color = Color3.fromRGB(255, 255, 255)

-- العنوان
local title = Instance.new("TextLabel", menu)
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.Text = "👾👾 XSOORX 👾👾"
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 18

-- زر الإغلاق
local close = Instance.new("TextButton", menu)
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1, -35, 0, 5)
close.Text = "X"
close.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
close.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", close)

-- القوائم
local rainbowButtons = {open, close}
local rainbowStrokes = {openStroke, stroke}
local pages = {}
local currentPage = 1

local scripts = {
    {
        {"Map Al Biout", "https://raw.githubusercontent.com/n0kc/AtomicHub/main/Map-Al-Biout.lua"},
        {"GhostHub", "https://raw.githubusercontent.com/GhostPlayer352/Test4/main/GhostHub"},
        {"TXM Script", "https://pastebin.com/raw/TXMNj1yy"},
        {"Pendulum Hub", "https://raw.githubusercontent.com/Tescalus/Pendulum-Hubs-Source/main/Pendulum%20Hub%20V5.lua"},
    },
    {
        {"Pastefy Script", "https://pastefy.app/ItfO0tdg/raw"},
        {"Fly V2", "https://gist.githubusercontent.com/meozoneYT/bf037dff9f0a70017304ddd67fdcd370/raw/e14e74f425b060df523343cf30b787074eb3c5d2/arceus%2520x%2520fly%2520v2%2520obflucator"},
        {"Get Tools", "https://pastebin.com/raw/g9vVSAA5"},
        {"No Cooldown", "https://pastebin.com/raw/DR0Mm7FS"},
    },
    {
        {"Use Tools", "https://pastebin.com/raw/5U0wMM26"},
        {"Extra Script", "https://pastebin.com/raw/gxgusJ0a"},
        {"Hook Wait", "https://pastebin.com/raw/YOUR_HOOK_WAIT_URL"},
        {"Empty", ""},
    },
    {
        {"Float Tools + Sword + KillAura", "custom_combined"},
        {"SPAM ON / OFF", "custom_spam"},
    }
}

-- إنشاء صفحات
local function createPage(scriptsList)
    local frame = Instance.new("Frame", menu)
    frame.Size = UDim2.new(1, 0, 1, -50)
    frame.Position = UDim2.new(0, 0, 0, 40)
    frame.BackgroundTransparency = 1
    frame.Visible = false

    for i, data in ipairs(scriptsList) do
        local btn = Instance.new("TextButton", frame)
        btn.Size = UDim2.new(0.9, 0, 0, 40)
        btn.Position = UDim2.new(0.05, 0, 0, (i - 1) * 50)
        btn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        btn.Text = data[1]
        btn.Font = Enum.Font.GothamBold
        btn.TextSize = 16
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)

        table.insert(rainbowButtons, btn)

        btn.MouseButton1Click:Connect(function()
            if data[2] == "custom_combined" then
                -- سيف + أدوات طافية + كيل اورا
                pcall(function()
                    loadstring(game:HttpGet("https://raw.githubusercontent.com/Markklol/Script/refs/heads/main/Sword%20Script"))()
                end)
                local offsets = {
                    ["Axe"] = Vector3.new(13, -10, -4),
                    ["Staff"] = Vector3.new(2, 10, -16),
                    ["Energy Sword"] = Vector3.new(-13, -10, -4),
                }
                local function FloatTools()
                    local char = game.Players.LocalPlayer.Character
                    if char then
                        for _, tool in pairs(char:GetChildren()) do
                            if tool:IsA("Tool") and offsets[tool.Name] then
                                tool.Grip = CFrame.new(offsets[tool.Name])
                            end
                        end
                    end
                end
                FloatTools()
                game.Players.LocalPlayer.CharacterAdded:Connect(function()
                    wait(1)
                    FloatTools()
                end)
                spawn(function()
                    while true do
                        task.wait(0.2)
                        local player = game.Players.LocalPlayer
                        local char = player.Character
                        if not char then continue end
                        local hrp = char:FindFirstChild("HumanoidRootPart")
                        if not hrp then continue end
                        local closest, dist = nil, 1000
                        for _, p in pairs(game.Players:GetPlayers()) do
                            if p ~= player and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                                local d = (hrp.Position - p.Character.HumanoidRootPart.Position).Magnitude
                                if d < dist then
                                    closest = p
                                    dist = d
                                end
                            end
                        end
                        if closest and dist <= 6 then
                            local tool = char:FindFirstChildOfClass("Tool")
                            if tool then tool:Activate() end
                        end
                    end
                end)
            elseif data[2] == "custom_spam" then
                -- زر SPAM
                local spamGui = Instance.new("ScreenGui", game.CoreGui)
                local btn = Instance.new("TextButton", spamGui)
                btn.Position = UDim2.new(0.68, 0, 0.50, 0)
                btn.Size = UDim2.new(0, 70, 0, 30)
                btn.Text = "SPAM OFF"
                btn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
                btn.Font = Enum.Font.GothamBold
                btn.TextSize = 14
                btn.TextColor3 = Color3.fromRGB(255, 255, 255)
                local corner = Instance.new("UICorner", btn)
                local stroke = Instance.new("UIStroke", btn)
                stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
                stroke.Thickness = 2

                local attackEnabled = false      
                local attackingTools = {}      

                btn.MouseButton1Click:Connect(function()      
                    attackEnabled = not attackEnabled      
                    btn.Text = attackEnabled and "SPAM ON" or "SPAM OFF"      
                    if not attackEnabled then      
                        local player = game.Players.LocalPlayer      
                        if player and player.Character then      
                            for _, tool in ipairs(player.Character:GetChildren()) do      
                                if tool:IsA("Tool") then      
                                    tool.Parent = player.Backpack      
                                end      
                            end      
                        end      
                        attackingTools = {}      
                    end      
                end)      

                local function activateTool(tool)      
                    if not attackingTools[tool] then      
                        attackingTools[tool] = true      
                        task.spawn(function()      
                            while attackEnabled and tool.Parent == game.Players.LocalPlayer.Character do      
                                pcall(function()      
                                    tool:Activate()      
                                end)      
                                task.wait()      
                            end      
                            attackingTools[tool] = nil      
                        end)      
                    end      
                end      

                game:GetService("RunService").Heartbeat:Connect(function()      
                    if attackEnabled then      
                        local player = game.Players.LocalPlayer      
                        if player and player.Character then      
                            for _, tool in ipairs(player.Backpack:GetChildren()) do      
                                if tool:IsA("Tool") then      
                                    if tool.Parent ~= player.Character then      
                                        tool.Parent = player.Character      
                                    end      
                                    activateTool(tool)      
                                end      
                            end      
                        end      
                    end      
                end)      

                task.spawn(function()      
                    while true do      
                        local hue = tick() % 5 / 5      
                        local color = Color3.fromHSV(hue, 1, 1)      
                        stroke.Color = color      
                        btn.TextColor3 = color      
                        task.wait(0.05)      
                    end      
                end)      
            else      
                pcall(function()      
                    loadstring(game:HttpGet(data[2]))()      
                end)      
            end
        end)
    end

    return frame
end

for _, scriptList in ipairs(scripts) do
    table.insert(pages, createPage(scriptList))
end

local nextPageBtn = Instance.new("TextButton", menu)
nextPageBtn.Size = UDim2.new(0.9, 0, 0, 30)
nextPageBtn.Position = UDim2.new(0.05, 0, 1, -35)
nextPageBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
nextPageBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
nextPageBtn.Text = "Next Page"
nextPageBtn.Font = Enum.Font.GothamBold
nextPageBtn.TextSize = 14
Instance.new("UICorner", nextPageBtn).CornerRadius = UDim.new(0, 6)
table.insert(rainbowButtons, nextPageBtn)

local function showPage(index)
    for i, page in ipairs(pages) do
        page.Visible = (i == index)
    end
end

showPage(currentPage)

nextPageBtn.MouseButton1Click:Connect(function()
    currentPage += 1
    if currentPage > #pages then
        currentPage = 1
    end
    showPage(currentPage)
end)

local function updateRainbow()
    local hue = tick() % 5 / 5
    local color = Color3.fromHSV(hue, 1, 1)
    title.TextColor3 = color
    for _, btn in ipairs(rainbowButtons) do
        btn.TextColor3 = color
    end
    for _, s in ipairs(rainbowStrokes) do
        s.Color = color
    end
end

game:GetService("RunService").Heartbeat:Connect(updateRainbow)

open.MouseButton1Click:Connect(function()
    menu.Visible = true
end)

close.MouseButton1Click:Connect(function()
    menu.Visible = false
end)

-- إضافة سكربت القتل القريب
local range = 29  -- مدى القتل (ضخم جداً ليشمل كل الخريطة)

local player = game:GetService("Players").LocalPlayer  -- اللاعب الحالي

game:GetService("RunService").RenderStepped:Connect(function()
    local p = game.Players:GetPlayers()
    for i = 2, #p do  -- يبدأ من 2 لتجاهل اللاعب الحالي
        local v = p[i].Character
        if v and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and v:FindFirstChild("HumanoidRootPart") and player:DistanceFromCharacter(v.HumanoidRootPart.Position) <= range then
            local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")
            if tool and tool:FindFirstChild("Handle") then
                tool:Activate()
                for i,v in next, v:GetChildren() do
                    if v:IsA("BasePart") then
                        firetouchinterest(tool.Handle,v,0)
                        firetouchinterest(tool.Handle,v,1)
                    end
                end
            end
        end
    end
end)
