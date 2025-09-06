--[[
	Roblox2Lua
	----------
	
	This code was generated using
	Deluct's Roblox2Lua plugin.
]]--

--// Instances

local lockexe = Instance.new("ScreenGui")
lockexe.IgnoreGuiInset = false
lockexe.ResetOnSpawn = true
lockexe.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
lockexe.Name = "lock.exe"
lockexe.Parent = workspace

local local_script = Instance.new("LocalScript")
local_script.Source = "local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Player = Players.LocalPlayer
local Mouse = Player:GetMouse()
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local lockKey = nil
local targetPartName = nil
local target = nil
local highlight = nil

-- Sounds
local keySound = Instance.new("Sound")
keySound.SoundId = "rbxassetid://111174530730534"
keySound.Volume = 0.2
keySound.Parent = Player:WaitForChild("PlayerGui")

local lockSound = Instance.new("Sound")
lockSound.SoundId = "rbxassetid://86220592770005"
lockSound.Volume = 0.1
lockSound.Parent = Player:WaitForChild("PlayerGui")

-- Notification function
local function notify(title, text)
	pcall(function()
		game.StarterGui:SetCore("SendNotification", {
			Title = title;
			Text = text;
			Duration = 5
		})
	end)
end

-- Step 1: Choose Lock Key with double press
notify("Lock System", "Press the key you want to use twice to confirm")
local keyChosen = false
local firstPressKey = nil
local confirmPressed = false

Mouse.KeyDown:Connect(function(key)
	if not keyChosen then
		if not firstPressKey then
			firstPressKey = key
			notify("Lock System", "Press "..key.." again to confirm")
		elseif key == firstPressKey then
			confirmPressed = true
			lockKey = key
			keyChosen = true
			keySound:Play()
			notify("Lock System", "Lock Key Set: "..lockKey.." Starting in 1 second")
		else
			firstPressKey = key
			notify("Lock System", "Press "..key.." again to confirm")
		end
	end
end)

-- Wait 1 second after key confirmed
local startTime = tick()
RunService.RenderStepped:Connect(function()
	if keyChosen and confirmPressed and tick() - startTime >= 1 then
		confirmPressed = false
		notify("Lock System", "Now choose target part: H for Head, T for Torso")
	end
end)

-- Step 2: Choose Head or Torso
local partChosen = false
Mouse.KeyDown:Connect(function(key)
	if keyChosen and not partChosen and not confirmPressed then
		if key:lower() == "h" then
			targetPartName = "Head"
			partChosen = true
			notify("Lock System", "Target part set to Head")
		elseif key:lower() == "t" then
			targetPartName = "Torso"
			partChosen = true
			notify("Lock System", "Target part set to Torso")
		end
	end
end)

-- Rainbow highlight
local rainbowColors = {
	Color3.fromRGB(255, 0, 0), Color3.fromRGB(255, 127, 0),
	Color3.fromRGB(255, 255, 0), Color3.fromRGB(0, 255, 0),
	Color3.fromRGB(0, 0, 255), Color3.fromRGB(75, 0, 130),
	Color3.fromRGB(148, 0, 211)
}
local colorIndex = 1
local colorStep = 0

local function startHighlight(char)
	if highlight then highlight:Destroy() end
	highlight = Instance.new("Highlight")
	highlight.Adornee = char
	highlight.FillTransparency = 0.5
	highlight.OutlineTransparency = 0.5
	highlight.FillColor = rainbowColors[1]
	highlight.OutlineColor = Color3.new(0,0,0)
	highlight.Parent = char
end

local function updateRainbow()
	if highlight then
		colorStep = colorStep + 0.01
		if colorStep >= 1 then
			colorStep = 0
			colorIndex = colorIndex + 1
			if colorIndex > #rainbowColors then colorIndex = 1 end
		end
		local nextIndex = colorIndex + 1
		if nextIndex > #rainbowColors then nextIndex = 1 end
		highlight.FillColor = rainbowColors[colorIndex]:Lerp(rainbowColors[nextIndex], colorStep)
	end
end

-- Get torso for R6/R15
local function getTorso(char)
	if char:FindFirstChild("UpperTorso") then
		return char.UpperTorso -- R15
	elseif char:FindFirstChild("Torso") then
		return char.Torso -- R6
	end
	return nil
end

-- Step 3: Lock onto player with single press
Mouse.KeyDown:Connect(function(key)
	if key == lockKey and partChosen and not confirmPressed then
		local closestDistance = math.huge
		target = nil

		for _, plr in pairs(Players:GetPlayers()) do
			if plr ~= Player and plr.Character then
				local part
				if targetPartName == "Head" then
					part = plr.Character:FindFirstChild("Head")
				else
					part = getTorso(plr.Character)
				end

				if part then
					local distance = (part.Position - Player.Character.HumanoidRootPart.Position).Magnitude
					if distance < closestDistance then
						closestDistance = distance
						target = plr
					end
				end
			end
		end

		if target then
			notify("Lock System", "Target Set: "..target.Name)
			lockSound:Play()
			startHighlight(target.Character)
		end
	end
end)

RunService.RenderStepped:Connect(function()
	updateRainbow()
end)
"
local_script.Parent = lockexe

--//Modules

local modules = {}

--// Scripts

-- LocalScript
task.spawn(function()
	local script = local_script

	local oldreq = require
	local function require(target)
		if modules[target] then
			return modules[target]()
		end
		return oldreq(target)
	end

	local Players = game:GetService("Players")
	local RunService = game:GetService("RunService")
	local Player = Players.LocalPlayer
	local Mouse = Player:GetMouse()
	local ReplicatedStorage = game:GetService("ReplicatedStorage")
	
	local lockKey = nil
	local targetPartName = nil
	local target = nil
	local highlight = nil
	
	-- Sounds
	local keySound = Instance.new("Sound")
	keySound.SoundId = "rbxassetid://111174530730534"
	keySound.Volume = 0.2
	keySound.Parent = Player:WaitForChild("PlayerGui")
	
	local lockSound = Instance.new("Sound")
	lockSound.SoundId = "rbxassetid://86220592770005"
	lockSound.Volume = 0.1
	lockSound.Parent = Player:WaitForChild("PlayerGui")
	
	-- Notification function
	local function notify(title, text)
		pcall(function()
			game.StarterGui:SetCore("SendNotification", {
				Title = title;
				Text = text;
				Duration = 5
			})
		end)
	end
	
	-- Step 1: Choose Lock Key with double press
	notify("Lock System", "Press the key you want to use twice to confirm")
	local keyChosen = false
	local firstPressKey = nil
	local confirmPressed = false
	
	Mouse.KeyDown:Connect(function(key)
		if not keyChosen then
			if not firstPressKey then
				firstPressKey = key
				notify("Lock System", "Press "..key.." again to confirm")
			elseif key == firstPressKey then
				confirmPressed = true
				lockKey = key
				keyChosen = true
				keySound:Play()
				notify("Lock System", "Lock Key Set: "..lockKey.." Starting in 1 second")
			else
				firstPressKey = key
				notify("Lock System", "Press "..key.." again to confirm")
			end
		end
	end)
	
	-- Wait 1 second after key confirmed
	local startTime = tick()
	RunService.RenderStepped:Connect(function()
		if keyChosen and confirmPressed and tick() - startTime >= 1 then
			confirmPressed = false
			notify("Lock System", "Now choose target part: H for Head, T for Torso")
		end
	end)
	
	-- Step 2: Choose Head or Torso
	local partChosen = false
	Mouse.KeyDown:Connect(function(key)
		if keyChosen and not partChosen and not confirmPressed then
			if key:lower() == "h" then
				targetPartName = "Head"
				partChosen = true
				notify("Lock System", "Target part set to Head")
			elseif key:lower() == "t" then
				targetPartName = "Torso"
				partChosen = true
				notify("Lock System", "Target part set to Torso")
			end
		end
	end)
	
	-- Rainbow highlight
	local rainbowColors = {
		Color3.fromRGB(255, 0, 0), Color3.fromRGB(255, 127, 0),
		Color3.fromRGB(255, 255, 0), Color3.fromRGB(0, 255, 0),
		Color3.fromRGB(0, 0, 255), Color3.fromRGB(75, 0, 130),
		Color3.fromRGB(148, 0, 211)
	}
	local colorIndex = 1
	local colorStep = 0
	
	local function startHighlight(char)
		if highlight then highlight:Destroy() end
		highlight = Instance.new("Highlight")
		highlight.Adornee = char
		highlight.FillTransparency = 0.5
		highlight.OutlineTransparency = 0.5
		highlight.FillColor = rainbowColors[1]
		highlight.OutlineColor = Color3.new(0,0,0)
		highlight.Parent = char
	end
	
	local function updateRainbow()
		if highlight then
			colorStep = colorStep + 0.01
			if colorStep >= 1 then
				colorStep = 0
				colorIndex = colorIndex + 1
				if colorIndex > #rainbowColors then colorIndex = 1 end
			end
			local nextIndex = colorIndex + 1
			if nextIndex > #rainbowColors then nextIndex = 1 end
			highlight.FillColor = rainbowColors[colorIndex]:Lerp(rainbowColors[nextIndex], colorStep)
		end
	end
	
	-- Get torso for R6/R15
	local function getTorso(char)
		if char:FindFirstChild("UpperTorso") then
			return char.UpperTorso -- R15
		elseif char:FindFirstChild("Torso") then
			return char.Torso -- R6
		end
		return nil
	end
	
	-- Step 3: Lock onto player with single press
	Mouse.KeyDown:Connect(function(key)
		if key == lockKey and partChosen and not confirmPressed then
			local closestDistance = math.huge
			target = nil
	
			for _, plr in pairs(Players:GetPlayers()) do
				if plr ~= Player and plr.Character then
					local part
					if targetPartName == "Head" then
						part = plr.Character:FindFirstChild("Head")
					else
						part = getTorso(plr.Character)
					end
	
					if part then
						local distance = (part.Position - Player.Character.HumanoidRootPart.Position).Magnitude
						if distance < closestDistance then
							closestDistance = distance
							target = plr
						end
					end
				end
			end
	
			if target then
				notify("Lock System", "Target Set: "..target.Name)
				lockSound:Play()
				startHighlight(target.Character)
			end
		end
	end)
	
	RunService.RenderStepped:Connect(function()
		updateRainbow()
	end)
	
end)
