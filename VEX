local plrs = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = plrs.LocalPlayer
local lplr = LocalPlayer
local Camera = workspace.CurrentCamera
local cam = Camera
local Target = nil
local TargetChanged = Instance.new("BindableEvent")
local Selection = Instance.new("SelectionBox", game:GetService("Workspace"))
local RunService = game:GetService("RunService")
local mouse = LocalPlayer:GetMouse()
local Connections = {}
local velocity = Vector3.zero
local oldpos = Vector3.zero
local oldtick = tick()

local function getEquippedTool()
	return LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Tool")
end

local template = "1v1bot.lol - best ai bot to fight za opps\nclick Z to assist with glockfling\nclick Q with your mouse near a target\nclick F to toggle monkey movement (%s)\nclick R to toggle triggerbot (%s)\nExecute `_G.Uninject()` in another tab of the exec to uninject\n1v1bot.lol - made by Vex"
local title = Drawing.new("Text")
title.Position = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2 - 300)
title.Transparency = 1
title.Size = 18
title.Color = Color3.fromRGB(255, 0, 0)
title.Text = "1v1bot.lol - best ai bot to fight za opps\nclick Z to assist with glockfling\nclick Q with your mouse near a target\nclick F to toggle monkey movement (OFF)\nclick R to toggle triggerbot (OFF)\nExecute `_G.Uninject()` in another tab of the exec to uninject\n1v1bot.lol - made by Vex"
title.Center = true
title.Outline = true
title.OutlineColor = Color3.fromRGB(0, 0, 0)
title.Font = 2

if _G.Uninject then
	_G.Uninject()
end

_G.Uninject = function()
    title:Destroy()
	Selection:Destroy()
	for _, connection in next, Connections do
		connection:Disconnect()
	end
	if LocalPlayer.Backpack:FindFirstChild("Camlock") then
		LocalPlayer.Backpack.Camlock:Destroy()
	elseif LocalPlayer.Character:FindFirstChild("Camlock") then
		LocalPlayer.Character.Camlock:Destroy()
	end
end

function GetNearestPlayer()
	local closestDist = math.huge
	local closestPlr = nil
	for _, v in ipairs(plrs:GetPlayers()) do
		if v ~= lplr and v.Character and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health >= 0 then
			local screenPos, cameraVisible = cam:WorldToViewportPoint(v.Character.PrimaryPart.Position)
			if cameraVisible then
				local distToMouse = (Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2.new(screenPos.X, screenPos.Y)).Magnitude
				if distToMouse < closestDist then
					closestPlr = v
					closestDist = distToMouse
				end
			end
		end
	end
	return closestPlr
end

local function toggleFirstPerson()
    if lplr.CameraMode == Enum.CameraMode.Classic then
        lplr.CameraMode = Enum.CameraMode.LockFirstPerson
    else
        lplr.CameraMode = Enum.CameraMode.Classic
    end
end

local ai = false
local holdingShift = false
local tbot = false
table.insert(Connections, UserInputService.InputBegan:Connect(function(ip,gpe)
	if ip.KeyCode == Enum.KeyCode.Q and not gpe then
		if Target then
			Target = nil
			return TargetChanged:Fire(nil)
		end

		local plr = GetNearestPlayer()
		if plr then
			Target = plr.Character
			TargetChanged:Fire()
		else
			Target = nil
			TargetChanged:Fire(nil)
		end
    elseif ip.KeyCode == Enum.KeyCode.F and not gpe then
        ai = not ai
        title.Text = string.format(template, ai == true and "ON" or "OFF", tbot == true and "ON" or "OFF")
        title.Position = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2 - 300)
    elseif ip.KeyCode == Enum.KeyCode.LeftShift and not gpe then
        holdingShift = true
    elseif ip.KeyCode == Enum.KeyCode.R and not gpe then
        tbot = not tbot
        title.Text = string.format(template, ai == true and "ON" or "OFF", tbot == true and "ON" or "OFF")
        title.Position = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2 - 300)
    elseif ip.KeyCode == Enum.KeyCode.Z and not gpe then
        local skibidid = false
        local root = lplr.Character.HumanoidRootPart
        local isWallInfront = false
        local ray = Ray.new(root.Position, root.CFrame.LookVector * 2.4)
        local part = workspace:FindPartOnRay(ray, root.Parent, true, true)
        local head = lplr.Character.Head
        if not part then return nil end
        if (Camera.CFrame.Position - lplr.Character.Head.Position).Magnitude > 1.01 then
            toggleFirstPerson()
            skibidid = true
        end
        local item = getEquippedTool()
        if tostring(item) == "Glock" then
            item.Parent = lplr.Backpack
        end
        keypress(0xA2)
        task.wait(1/4)
        if tostring(item) ~= "Glock" then
            if item then
                item.Parent = lplr.Backpack
            end
        end
        if lplr.Backpack:FindFirstChild("Glock") then
            lplr.Backpack.Glock.Parent = lplr.Character
        end
        task.wait(1/8)
        local cf = head.CFrame
        Camera.CFrame = CFrame.new(
            Camera.CFrame.Position,
            cf.Position + (cf.LookVector * 5) + (cf.RightVector * -5)
        )
        task.wait(1/46)
        keyrelease(0xA2)
        task.delay(0.2, function()
            lplr.Character.Glock.Parent = lplr.Backpack 
        end)
        lplr.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        task.delay(0.1, function()
            if part then
                root.Velocity = root.Velocity + Vector3.new(0, math.random(70, 120), 0)
            end
        end)
        if skibidid then
            toggleFirstPerson()
        end
	end
end))
UserInputService.InputEnded:Connect(function(ip,gpe)
    if ip.KeyCode == Enum.KeyCode.LeftShift and not gpe then
        holdingShift = false
    end
end)

local aicd = false

-- triggerbot
table.insert(Connections, RunService.RenderStepped:Connect(function()
    if Target and tbot then
        local tool = getEquippedTool()
        if tostring(tool) == "Glock" or tostring(tool) == "Shotty" then
            tool:Activate()
            task.wait(1/30)
            tool:Deactivate()
        end
    end
end))

-- monkey movement
table.insert(Connections, RunService.Heartbeat:Connect(function()
    if ai == true and tbot == true and LocalPlayer.Character and Target then
        local root = LocalPlayer.Character.HumanoidRootPart
        local targ = Target.HumanoidRootPart
        local ppos = root.CFrame
        local epos = Vector3.new(targ.Position.X, ppos.Y, targ.Position.Z)
        root.CFrame = CFrame.new(ppos.Position, epos)
    end
end))
table.insert(Connections, RunService.RenderStepped:Connect(function()
    if aicd == true then return nil end
    if ai and LocalPlayer.Character and not isDead then
        aicd = true
        local human = LocalPlayer.Character.Humanoid
        local root = LocalPlayer.Character.HumanoidRootPart
        local pos = root.Position
        human:MoveTo(
            pos + (root.CFrame.RightVector * math.random(-15, 15))
        )
        local ran = math.random(1,3)
        if (ran == 2) and not holdingShift then
            task.spawn(function()
                keypress(0x10)
                task.wait(
                    ran == 1 and 0.1 or
                    ran == 2 and 0.2 or
                    ran == 3 and 1 / 9 or
                    0.01
                )
                keyrelease(0x10)
            end)
        end
        if (ran == 1) then
            task.wait(0.1)
        elseif (ran == 2) then
            task.wait(0.2)
        elseif (ran == 3) then
            task.wait(1 / 9)
        end
        aicd = false
    end
end))

local aimAtPos
local oldY = 0
TargetChanged.Event:Connect(function(basePart: BasePart)
	if Target then
		oldpos = Target.HumanoidRootPart.Position
		aimAtPos = oldpos
		oldY = aimAtPos.Y
		oldtick = tick()
		Selection.Adornee = Target.PrimaryPart
	else
		Selection.Adornee = nil
	end
end)

local velo = Instance.new("Vector3Value")
-- always calculate velocity (resolver from huge velocity)
table.insert(Connections, RunService.RenderStepped:Connect(function()
	if Target then
		local newPosition = Target.HumanoidRootPart.Position
		local newTick = tick()
		local deltaPos = newPosition - oldpos
		local deltaTick = newTick - oldtick
		velocity = deltaPos / deltaTick
		velo.Value = velo.Value:Lerp(velocity, 0.1)
		oldpos = newPosition
		oldtick = newTick
	else
		velocity = Vector3.zero
	end
end))
-- camera
_G.Camera = {
	Shotty = {
		Far = 7.7,
		Middle = 8.2,
		Close = 8.4
	},
	Glock = {
		Far = 8,
		Middle = 9,
		Close = 5
	}
}

-- reset assist
local isDead = false
lplr.CharacterAdded:Connect(function(v)
    isDead = false
    v.Humanoid.Died:Connect(function()
        isDead = true
    end)
end)

lplr.Character.Humanoid.Died:Connect(function()
    isDead = true
end)

local function reset()
    if not isDead then
        lplr.Character.Humanoid.WalkSpeed = 0
        if lplr.Character.Humanoid.FloorMaterial ~= Enum.Material.Air then
            lplr.Character.PrimaryPart.Anchored = true
            task.spawn(function()
                task.wait(0.2)
                lplr.Character.PrimaryPart.Anchored = false
            end)
        end
        task.wait(0.25)
        lplr.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Dead)
        lplr.Character:BreakJoints()
    end
end

local cd = false
table.insert(Connections, RunService.RenderStepped:Connect(function()
    if cd then return nil end
    if not isDead and lplr.Character then
        if lplr.Character.Humanoid.Health < 32 then
            cd = true
            reset()
            task.wait(5.6)
            cd = false
        end
    end
end))

-- aim at
table.insert(Connections, RunService.RenderStepped:Connect(function()
	local current = Camera.CFrame
	local targetPos
    task.spawn(function()
        if tbot then
            local currentCFrame = lplr.Character.HumanoidRootPart.CFrame
            local targetCFrame = Vector3.new(Target.Head.X, currentCFrame.Y, Target.Head.Z)
            lplr.Character.HumanoidRootPart.CFrame = CFrame.new(currentCFrame.Position, targetCFrame)
        end
    end)
	if Target then
		local eq = getEquippedTool()
		if not eq then return nil end
		local rg = (Camera.CFrame.Position - aimAtPos).Magnitude
		local td = _G.Camera[tostring(eq)]
		local pd = td.Middle

		if tostring(eq) == "Glock" then
			if rg > 80 then
				pd = td.Far
			elseif rg > 40 then
				pd = td.Middle
			elseif rg > 10 or rg < 9 then
				pd = td.Close
			end
		elseif tostring(eq) == "Shotty" then
			if rg > 60 then
				pd = td.Far
			elseif rg > 30 then
				pd = td.Middle
			elseif rg > 20 or rg < 9 then
				pd = td.Close
			end
		end

		if not pd then
			pd = 8
		end

		targetPos = aimAtPos + (
			Vector3.new(velo.Value.X, 0, velo.Value.Z) / pd
		)

		-- print(velo.Value)
		local xyz = Target.HumanoidRootPart.Position
		aimAtPos = Vector3.new(xyz.X, oldY, xyz.Z)
		-- warn(xyz)
		Camera.CFrame = CFrame.new(current.Position, targetPos)
	end
end))
