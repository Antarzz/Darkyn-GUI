Darkyn GUI made by Nickiuzoth!

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootPart = character:WaitForChild("HumanoidRootPart")

local UserInputService = game:GetService("UserInputService")

local flying = false
local invisible = false
local flySpeed = 50
local bodyVelocity
local bodyGyro
local guiVisible = true

-- Create GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "DarkynGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = player.PlayerGui

-- Main Frame
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 280, 0, 250)
mainFrame.Position = UDim2.new(0.5, -140, 0.1, 0)
mainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 20)
mainFrame.BorderSizePixel = 2
mainFrame.BorderColor3 = Color3.fromRGB(30, 60, 120)
mainFrame.Parent = screenGui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = mainFrame

-- Title Bar
local titleBar = Instance.new("Frame")
titleBar.Name = "TitleBar"
titleBar.Size = UDim2.new(1, 0, 0, 45)
titleBar.BackgroundColor3 = Color3.fromRGB(15, 30, 60)
titleBar.BorderSizePixel = 0
titleBar.Parent = mainFrame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 12)
titleCorner.Parent = titleBar

-- Title Text
local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(0.8, 0, 1, 0)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "Darkyn GUI"
title.TextColor3 = Color3.fromRGB(100, 150, 255)
title.TextSize = 20
title.Font = Enum.Font.GothamBold
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = titleBar

-- Close Button (X)
local closeButton = Instance.new("TextButton")
closeButton.Name = "CloseButton"
closeButton.Size = UDim2.new(0, 35, 0, 35)
closeButton.Position = UDim2.new(1, -40, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(20, 40, 80)
closeButton.BorderSizePixel = 0
closeButton.Text = "X"
closeButton.TextColor3 = Color3.fromRGB(255, 100, 100)
closeButton.TextSize = 18
closeButton.Font = Enum.Font.GothamBold
closeButton.Parent = titleBar

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 8)
closeCorner.Parent = closeButton

-- Flying Toggle Button
local flyButton = Instance.new("TextButton")
flyButton.Name = "FlyButton"
flyButton.Size = UDim2.new(0.85, 0, 0, 40)
flyButton.Position = UDim2.new(0.075, 0, 0, 60)
flyButton.BackgroundColor3 = Color3.fromRGB(30, 60, 120)
flyButton.BorderSizePixel = 0
flyButton.Text = "✈️ Enable Flying"
flyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
flyButton.TextSize = 16
flyButton.Font = Enum.Font.GothamBold
flyButton.Parent = mainFrame

local flyCorner = Instance.new("UICorner")
flyCorner.CornerRadius = UDim.new(0, 8)
flyCorner.Parent = flyButton

-- Invisibility Toggle Button
local invisButton = Instance.new("TextButton")
invisButton.Name = "InvisButton"
invisButton.Size = UDim2.new(0.85, 0, 0, 40)
invisButton.Position = UDim2.new(0.075, 0, 0, 110)
invisButton.BackgroundColor3 = Color3.fromRGB(30, 60, 120)
invisButton.BorderSizePixel = 0
invisButton.Text = "👻 Enable Invisibility"
invisButton.TextColor3 = Color3.fromRGB(255, 255, 255)
invisButton.TextSize = 16
invisButton.Font = Enum.Font.GothamBold
invisButton.Parent = mainFrame

local invisCorner = Instance.new("UICorner")
invisCorner.CornerRadius = UDim.new(0, 8)
invisCorner.Parent = invisButton

-- Speed Label
local speedLabel = Instance.new("TextLabel")
speedLabel.Name = "SpeedLabel"
speedLabel.Size = UDim2.new(1, 0, 0, 25)
speedLabel.Position = UDim2.new(0, 0, 0, 160)
speedLabel.BackgroundTransparency = 1
speedLabel.Text = "Speed: 50"
speedLabel.TextColor3 = Color3.fromRGB(100, 150, 255)
speedLabel.TextSize = 14
speedLabel.Font = Enum.Font.GothamBold
speedLabel.Parent = mainFrame

-- Speed Slider Background
local sliderBg = Instance.new("Frame")
sliderBg.Name = "SliderBg"
sliderBg.Size = UDim2.new(0.85, 0, 0, 10)
sliderBg.Position = UDim2.new(0.075, 0, 0, 190)
sliderBg.BackgroundColor3 = Color3.fromRGB(20, 40, 80)
sliderBg.BorderSizePixel = 0
sliderBg.Parent = mainFrame

local sliderCorner = Instance.new("UICorner")
sliderCorner.CornerRadius = UDim.new(1, 0)
sliderCorner.Parent = sliderBg

-- Speed Slider Fill
local sliderFill = Instance.new("Frame")
sliderFill.Name = "SliderFill"
sliderFill.Size = UDim2.new(0.5, 0, 1, 0)
sliderFill.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
sliderFill.BorderSizePixel = 0
sliderFill.Parent = sliderBg

local fillCorner = Instance.new("UICorner")
fillCorner.CornerRadius = UDim.new(1, 0)
fillCorner.Parent = sliderFill

-- Speed Slider Button
local sliderButton = Instance.new("TextButton")
sliderButton.Name = "SliderButton"
sliderButton.Size = UDim2.new(0, 20, 0, 20)
sliderButton.Position = UDim2.new(0.5, -10, 0.5, -10)
sliderButton.BackgroundColor3 = Color3.fromRGB(150, 200, 255)
sliderButton.BorderSizePixel = 0
sliderButton.Text = ""
sliderButton.Parent = sliderBg

local sliderBtnCorner = Instance.new("UICorner")
sliderBtnCorner.CornerRadius = UDim.new(1, 0)
sliderBtnCorner.Parent = sliderButton

-- Instructions
local instructions = Instance.new("TextLabel")
instructions.Name = "Instructions"
instructions.Size = UDim2.new(1, 0, 0, 30)
instructions.Position = UDim2.new(0, 0, 1, -30)
instructions.BackgroundTransparency = 1
instructions.Text = "Press K to toggle GUI | WASD + Space/Shift"
instructions.TextColor3 = Color3.fromRGB(80, 120, 200)
instructions.TextSize = 11
instructions.Font = Enum.Font.Gotham
instructions.Parent = mainFrame

-- Toggle flying function
local function toggleFly()
	flying = not flying
	
	if flying then
		bodyVelocity = Instance.new("BodyVelocity")
		bodyVelocity.Velocity = Vector3.new(0, 0, 0)
		bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
		bodyVelocity.Parent = rootPart
		
		bodyGyro = Instance.new("BodyGyro")
		bodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
		bodyGyro.P = 9e4
		bodyGyro.Parent = rootPart
		
		humanoid.PlatformStand = true
		
		flyButton.Text = "✈️ Disable Flying"
		flyButton.BackgroundColor3 = Color3.fromRGB(50, 100, 200)
	else
		if bodyVelocity then bodyVelocity:Destroy() end
		if bodyGyro then bodyGyro:Destroy() end
		
		humanoid.PlatformStand = false
		
		flyButton.Text = "✈️ Enable Flying"
		flyButton.BackgroundColor3 = Color3.fromRGB(30, 60, 120)
	end
end

-- Toggle invisibility function
local function toggleInvisibility()
	invisible = not invisible
	
	if invisible then
		for _, part in pairs(character:GetDescendants()) do
			if part:IsA("BasePart") or part:IsA("Decal") then
				part.Transparency = 1
			end
			if part:IsA("Accessory") then
				part.Handle.Transparency = 1
			end
		end
		if character:FindFirstChild("Head") and character.Head:FindFirstChild("face") then
			character.Head.face.Transparency = 1
		end
		
		invisButton.Text = "👻 Disable Invisibility"
		invisButton.BackgroundColor3 = Color3.fromRGB(50, 100, 200)
	else
		for _, part in pairs(character:GetDescendants()) do
			if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
				part.Transparency = 0
			elseif part:IsA("Decal") then
				part.Transparency = 0
			end
			if part:IsA("Accessory") then
				part.Handle.Transparency = 0
			end
		end
		if character:FindFirstChild("Head") and character.Head:FindFirstChild("face") then
			character.Head.face.Transparency = 0
		end
		
		invisButton.Text = "👻 Enable Invisibility"
		invisButton.BackgroundColor3 = Color3.fromRGB(30, 60, 120)
	end
end

-- Toggle GUI visibility
local function toggleGUI()
	guiVisible = not guiVisible
	mainFrame.Visible = guiVisible
	
	if guiVisible then
		print("Darkyn GUI opened")
	else
		print("Press K to open Darkyn GUI")
	end
end

-- Button events
flyButton.MouseButton1Click:Connect(toggleFly)
invisButton.MouseButton1Click:Connect(toggleInvisibility)
closeButton.MouseButton1Click:Connect(toggleGUI)

-- Keyboard shortcut for GUI toggle
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	
	if input.KeyCode == Enum.KeyCode.K then
		toggleGUI()
	end
end)

-- Slider functionality
local dragging = false

sliderButton.MouseButton1Down:Connect(function()
	dragging = true
end)

UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = false
	end
end)

-- Main loop
game:GetService("RunService").Heartbeat:Connect(function()
	if dragging then
		local mousePos = UserInputService:GetMouseLocation().X
		local sliderPos = sliderBg.AbsolutePosition.X
		local sliderSize = sliderBg.AbsoluteSize.X
		
		local relative = math.clamp((mousePos - sliderPos) / sliderSize, 0, 1)
		
		sliderButton.Position = UDim2.new(relative, -10, 0.5, -10)
		sliderFill.Size = UDim2.new(relative, 0, 1, 0)
		
		flySpeed = math.floor(relative * 100)
		speedLabel.Text = "Speed: " .. flySpeed
	end
	
	-- Flight movement
	if flying and bodyVelocity and bodyGyro then
		local camera = workspace.CurrentCamera
		local direction = Vector3.new(0, 0, 0)
		
		if UserInputService:IsKeyDown(Enum.KeyCode.W) then
			direction = direction + (camera.CFrame.LookVector * flySpeed)
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.S) then
			direction = direction - (camera.CFrame.LookVector * flySpeed)
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.A) then
			direction = direction - (camera.CFrame.RightVector * flySpeed)
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.D) then
			direction = direction + (camera.CFrame.RightVector * flySpeed)
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
			direction = direction + Vector3.new(0, flySpeed, 0)
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then
			direction = direction - Vector3.new(0, flySpeed, 0)
		end
		
		bodyVelocity.Velocity = direction
		bodyGyro.CFrame = camera.CFrame
	end
end)

-- Initial message
print("Darkyn GUI loaded! Press K to toggle GUI")
