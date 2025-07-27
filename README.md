--[[
    ✨ سكربت العم طوفي ❤️‍🔥
    مطور بواسطة العم طوفي 😉❤️‍🔥
]]

local player = game.Players.LocalPlayer
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local startTime = tick()

-- إنشاء واجهة GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "InfoGUI"
screenGui.Parent = player:WaitForChild("PlayerGui")

-- الإطار الرئيسي
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 0, 0, 0) -- يبدأ صغير للأنيميشن
frame.Position = UDim2.new(0.5, -150, 0.1, 0)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0
frame.Visible = true
frame.Parent = screenGui
frame.Active = true
frame.Draggable = true

-- حركة تكبير عند الظهور
TweenService:Create(frame, TweenInfo.new(1, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
    Size = UDim2.new(0, 300, 0, 200)
}):Play()

-- العنوان
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.Text = "📌 العم طوفي ❤️‍🔥"
title.TextColor3 = Color3.fromRGB(255, 215, 0)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.TextSize = 26
title.Parent = frame

-- الوقت
local timeLabel = Instance.new("TextLabel")
timeLabel.Size = UDim2.new(1, 0, 0, 30)
timeLabel.Position = UDim2.new(0, 0, 0.25, 0)
timeLabel.Text = "وقت في السيرفر: 00:00:00"
timeLabel.TextColor3 = Color3.new(1, 1, 1)
timeLabel.BackgroundTransparency = 1
timeLabel.Font = Enum.Font.Gotham
timeLabel.TextSize = 20
timeLabel.Parent = frame

-- اسم اللاعب
local playerNameLabel = Instance.new("TextLabel")
playerNameLabel.Size = UDim2.new(1, 0, 0, 30)
playerNameLabel.Position = UDim2.new(0, 0, 0.45, 0)
playerNameLabel.Text = "اسمك: " .. player.Name
playerNameLabel.TextColor3 = Color3.new(1, 1, 1)
playerNameLabel.BackgroundTransparency = 1
playerNameLabel.Font = Enum.Font.Gotham
playerNameLabel.TextSize = 18
playerNameLabel.Parent = frame

-- عدد اللاعبين
local playersCountLabel = Instance.new("TextLabel")
playersCountLabel.Size = UDim2.new(1, 0, 0, 30)
playersCountLabel.Position = UDim2.new(0, 0, 0.65, 0)
playersCountLabel.Text = "عدد اللاعبين: " .. #Players:GetPlayers()
playersCountLabel.TextColor3 = Color3.new(1, 1, 1)
playersCountLabel.BackgroundTransparency = 1
playersCountLabel.Font = Enum.Font.Gotham
playersCountLabel.TextSize = 18
playersCountLabel.Parent = frame

Players.PlayerAdded:Connect(function()
    playersCountLabel.Text = "عدد اللاعبين: " .. #Players:GetPlayers()
end)
Players.PlayerRemoving:Connect(function()
    playersCountLabel.Text = "عدد اللاعبين: " .. #Players:GetPlayers()
end)

-- توقيع المطور
local creditLabel = Instance.new("TextLabel")
creditLabel.Size = UDim2.new(1, 0, 0, 20)
creditLabel.Position = UDim2.new(0, 0, 0.85, 0)
creditLabel.Text = "مطور بواسطة العم طوفي 😉❤️‍🔥"
creditLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
creditLabel.BackgroundTransparency = 1
creditLabel.Font = Enum.Font.GothamBold
creditLabel.TextSize = 14
creditLabel.Parent = frame

-- زر الإغلاق
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0.25, 0, 0.2, 0)
closeButton.Position = UDim2.new(0.7, 0, 0.05, 0)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 20
closeButton.Parent = frame

closeButton.MouseButton1Click:Connect(function()
    TweenService:Create(frame, TweenInfo.new(0.8, Enum.EasingStyle.Back, Enum.EasingDirection.In), {
        Size = UDim2.new(0, 0, 0, 0)
    }):Play()
    wait(0.8)
    screenGui:Destroy()
end)

-- تحديث الوقت كل ثانية
while true do
    wait(1)
    local timeSpent = tick() - startTime
    local hours = math.floor(timeSpent / 3600)
    local minutes = math.floor((timeSpent % 3600) / 60)
    local seconds = math.floor(timeSpent % 60)
    timeLabel.Text = string.format("وقت في السيرفر: %02d:%02d:%02d", hours, minutes, seconds)
end
