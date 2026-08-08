local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer
local event = ReplicatedStorage:WaitForChild("MobileLevelAdmin")

local gui = Instance.new("ScreenGui")
gui.Name = "MobileLevelAdmin"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.fromOffset(220, 230)
frame.Position = UDim2.new(1, -235, 0.5, -115)
frame.BackgroundColor3 = Color3.fromRGB(25,25,30)
frame.Parent = gui

Instance.new("UICorner", frame).CornerRadius = UDim.new(0,12)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,0,0,40)
title.Text = "LEVEL ADMIN"
title.TextColor3 = Color3.new(1,1,1)
title.TextSize = 20
title.BackgroundTransparency = 1
title.Parent = frame

local box = Instance.new("TextBox")
box.Size = UDim2.new(1,-20,0,40)
box.Position = UDim2.fromOffset(10,45)
box.Text = "10"
box.PlaceholderText = "จำนวน Level"
box.TextSize = 18
box.Parent = frame

local function button(text, y, color, action)
	local b = Instance.new("TextButton")
	b.Size = UDim2.new(1,-20,0,40)
	b.Position = UDim2.fromOffset(10,y)
	b.Text = text
	b.TextSize = 17
	b.TextColor3 = Color3.new(1,1,1)
	b.BackgroundColor3 = color
	b.Parent = frame

	Instance.new("UICorner", b).CornerRadius = UDim.new(0,8)

	b.Activated:Connect(function()
		event:FireServer(action, tonumber(box.Text) or 1)
	end)
end

button("+ เพิ่ม Level", 90, Color3.fromRGB(40,170,90), "add")
button("ตั้ง Level", 135, Color3.fromRGB(60,110,210), "set")
button("Reset", 180, Color3.fromRGB(190,55,55), "reset")

