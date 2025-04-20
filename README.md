 -- Khởi tạo GUI local player = game.Players.LocalPlayer local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui")) gui.Name = "VNAccessGUI" gui.ResetOnSpawn = false

local currentTab = nil

-- Tạo khung chứa các nút tab local tabFrame = Instance.new("Frame", gui) tabFrame.Name = "TabButtons" tabFrame.Size = UDim2.new(0, 350, 0, 40) tabFrame.Position = UDim2.new(0.5, -175, 0.5, -210) tabFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30) tabFrame.BorderSizePixel = 0

-- Tạo các tab local function createTab(name) local frame = Instance.new("Frame", gui) frame.Name = name frame.Size = UDim2.new(0, 350, 0, 350) frame.Position = UDim2.new(0.5, -175, 0.5, -150) frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40) frame.Visible = false return frame end

local mainTab = createTab("MainTab") local trollTab = createTab("TrollTab") local creatorTab = createTab("CreatorTab")

-- Hiển thị tab local function showTab(tab) if currentTab then currentTab.Visible = false end mainTab.Visible = false trollTab.Visible = false creatorTab.Visible = false tab.Visible = true currentTab = tab end

-- Tạo nút chuyển tab local function createTabButton(text, pos, tab) local btn = Instance.new("TextButton", tabFrame) btn.Size = UDim2.new(0, 100, 0, 30) btn.Position = pos btn.Text = text btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60) btn.TextColor3 = Color3.new(1,1,1) btn.MouseButton1Click:Connect(function() showTab(tab) end) end

createTabButton("Menu Chính", UDim2.new(0, 10, 0, 5), mainTab) createTabButton("Troll", UDim2.new(0, 120, 0, 5), trollTab) createTabButton("Người tạo", UDim2.new(0, 230, 0, 5), creatorTab)

-- Nút ẩn/hiện GUI local toggle = Instance.new("TextButton", gui) toggle.Size = UDim2.new(0, 80, 0, 30) toggle.Position = UDim2.new(0, 10, 1, -40) toggle.Text = "Ẩn/Hiện" toggle.BackgroundColor3 = Color3.fromRGB(100, 100, 100) toggle.TextColor3 = Color3.new(1, 1, 1)

toggle.MouseButton1Click:Connect(function() local visibleNow = not mainTab.Visible and not trollTab.Visible and not creatorTab.Visible mainTab.Visible = visibleNow and currentTab == mainTab trollTab.Visible = visibleNow and currentTab == trollTab creatorTab.Visible = visibleNow and currentTab == creatorTab tabFrame.Visible = visibleNow end)

-- Multi-Jump game:GetService("UserInputService").JumpRequest:Connect(function() if player.Character then local humanoid = player.Character:FindFirstChildOfClass("Humanoid") if humanoid and humanoid:GetState() ~= Enum.HumanoidStateType.Seated then humanoid:ChangeState(Enum.HumanoidStateType.Jumping) end end end)

-- Tab 1 - Menu Chính local flyBtn = Instance.new("TextButton", mainTab) flyBtn.Position = UDim2.new(0, 10, 0, 50) flyBtn.Size = UDim2.new(0, 100, 0, 30) flyBtn.Text = "Fly" flyBtn.MouseButton1Click:Connect(function() loadstring(game:HttpGet("https://raw.githubusercontent.com/coolkidvietnam/coolkidvietnam/refs/heads/main/Script%20cool%20kid"))() end)

for i, speed in ipairs({16, 25, 50, 75}) do local btn = Instance.new("TextButton", mainTab) btn.Size = UDim2.new(0, 100, 0, 30) btn.Position = UDim2.new(0, 10 + ((i - 1) * 110) % 330, 0, 90 + math.floor((i - 1) / 3) * 40) btn.Text = "Tốc " .. tostring(speed) btn.MouseButton1Click:Connect(function() if player.Character and player.Character:FindFirstChild("Humanoid") then player.Character.Humanoid.WalkSpeed = speed end end) end

local noclip = false local conn local noclipBtn = Instance.new("TextButton", mainTab) noclipBtn.Position = UDim2.new(0, 10, 0, 170) noclipBtn.Size = UDim2.new(0, 100, 0, 30) noclipBtn.Text = "Noclip" noclipBtn.MouseButton1Click:Connect(function() noclip = not noclip if noclip then conn = game:GetService("RunService").Stepped:Connect(function() if player.Character then for _, v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide = false end end end end) else if conn then conn:Disconnect() end if player.Character then for _, v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide = true end end end end end)

local vflyBtn = Instance.new("TextButton", mainTab) vflyBtn.Position = UDim2.new(0, 120, 0, 170) vflyBtn.Size = UDim2.new(0, 100, 0, 30) vflyBtn.Text = "VFly" vflyBtn14
