local RS, RSS = game:GetService("RunService"), game:GetService("ReplicatedStorage")
local LP = game.Players.LocalPlayer
local GR, SR = RSS.GlockFire, RSS.ShottyFire

local mouse = LP:GetMouse()
local fly = false
local flying = false
local fly_speed: number = 2

local players = game.Players:GetPlayers()


local Enabled = true


local plr = LP

local AirWalkPart = Instance.new("Part", workspace)
AirWalkPart.Size = Vector3.new(7, 2, 3)
AirWalkPart.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(0, -4, 0)
AirWalkPart.Transparency = 1
AirWalkPart.Anchored = true

local function toggle_fly()
	fly = true
	if fly then
		if plr.Character ~= nil then
			if plr.Character:FindFirstChild("HumanoidRootPart") and plr.Character:FindFirstChildWhichIsA("Humanoid") then

				local float_part: Part = Instance.new('Part', plr.Character)
				float_part.Name = "float_part"
				float_part.Transparency = 1
				float_part.Size = Vector3.new(6,1,6)
				float_part.Anchored = true

				plr.CharacterAdded:Connect(function()
					flying = false
					fly = false

				end)

				plr.Character.HumanoidRootPart.Anchored = true

				local root_part: BasePart = plr.Character.HumanoidRootPart

				local CONTROL = {F = 0, B = 0, L = 0, R = 0}
				local lCONTROL = {F = 0, B = 0, L = 0, R = 0}
				local SPEED = 0

				local function start_fly()
					flying = true

					local BG = Instance.new('BodyGyro', root_part)
					local BV = Instance.new('BodyVelocity', root_part)

					BG.P = 9e4
					BG.maxTorque = Vector3.new(9e9, 9e9, 9e9)
					BG.cframe = root_part.CFrame

					BV.velocity = Vector3.new(0, 0.1, 0)
					BV.maxForce = Vector3.new(9e9, 9e9, 9e9)

					spawn(function()
						repeat wait()
							if CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 then
								SPEED = 50
							elseif not (CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0) and SPEED ~= 0 then
								SPEED = 0
							end
							if (CONTROL.L + CONTROL.R) ~= 0 or (CONTROL.F + CONTROL.B) ~= 0 then
								BV.velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (CONTROL.F + CONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(CONTROL.L + CONTROL.R, (CONTROL.F + CONTROL.B) * 0.2, 0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
								lCONTROL = {F = CONTROL.F, B = CONTROL.B, L = CONTROL.L, R = CONTROL.R}
							elseif (CONTROL.L + CONTROL.R) == 0 and (CONTROL.F + CONTROL.B) == 0 and SPEED ~= 0 then
								BV.velocity = ((workspace.CurrentCamera.CoordinateFrame.LookVector * (lCONTROL.F + lCONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(lCONTROL.L + lCONTROL.R, (lCONTROL.F + lCONTROL.B) * 0.2, 0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
							else
								BV.velocity = Vector3.new(0, 0.1, 0)
							end
							BG.cframe = workspace.CurrentCamera.CoordinateFrame
						until not flying
						CONTROL = {F = 0, B = 0, L = 0, R = 0}
						lCONTROL = {F = 0, B = 0, L = 0, R = 0}
						SPEED = 0

						BG:destroy()
						BV:destroy()
					end)
				end

				mouse.KeyDown:connect(function(KEY)
					if KEY:lower() == 'w' then
						CONTROL.F = fly_speed

					elseif KEY:lower() == 's' then
						CONTROL.B = -fly_speed

					elseif KEY:lower() == 'a' then
						CONTROL.L = -fly_speed

					elseif KEY:lower() == 'd' then
						CONTROL.R = fly_speed

					end
				end)

				mouse.KeyUp:connect(function(KEY)
					if KEY:lower() == 'w' then
						CONTROL.F = 0
					elseif KEY:lower() == 's' then
						CONTROL.B = 0
					elseif KEY:lower() == 'a' then
						CONTROL.L = 0
					elseif KEY:lower() == 'd' then
						CONTROL.R = 0
					end
				end)

				start_fly()

				plr.Character.HumanoidRootPart.Anchored = false
			elseif plr.Character:FindFirstChild("Torso") and plr.Character:FindFirstChild("Humanoid") then

				local float_part: Part = Instance.new('Part', plr.Character)
				float_part.Name = "float_part"
				float_part.Transparency = 1
				float_part.Size = Vector3.new(6,1,6)
				float_part.Anchored = true

				plr.CharacterAdded:Connect(function()
					flying = false
					fly = false
				end)

				plr.Character.Torso.Anchored = true

				local root_part: BasePart = plr.Character.Torso

				local CONTROL = {F = 0, B = 0, L = 0, R = 0}
				local lCONTROL = {F = 0, B = 0, L = 0, R = 0}
				local SPEED = 0

				local function start_fly()
					flying = true

					local BG = Instance.new('BodyGyro', root_part)
					local BV = Instance.new('BodyVelocity', root_part)

					BG.P = 9e4
					BG.maxTorque = Vector3.new(9e9, 9e9, 9e9)
					BG.cframe = T.CFrame

					BV.velocity = Vector3.new(0, 0.1, 0)
					BV.maxForce = Vector3.new(9e9, 9e9, 9e9)

					spawn(function()
						repeat wait()
							if CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 then
								SPEED = 50
							elseif not (CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0) and SPEED ~= 0 then
								SPEED = 0
							end
							if (CONTROL.L + CONTROL.R) ~= 0 or (CONTROL.F + CONTROL.B) ~= 0 then
								BV.velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (CONTROL.F + CONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(CONTROL.L + CONTROL.R, (CONTROL.F + CONTROL.B) * 0.2, 0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
								lCONTROL = {F = CONTROL.F, B = CONTROL.B, L = CONTROL.L, R = CONTROL.R}
							elseif (CONTROL.L + CONTROL.R) == 0 and (CONTROL.F + CONTROL.B) == 0 and SPEED ~= 0 then
								BV.velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (lCONTROL.F + lCONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(lCONTROL.L + lCONTROL.R, (lCONTROL.F + lCONTROL.B) * 0.2, 0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
							else
								BV.velocity = Vector3.new(0, 0.1, 0)
							end
							BG.cframe = workspace.CurrentCamera.CoordinateFrame
						until not flying

						CONTROL = {F = 0, B = 0, L = 0, R = 0}
						lCONTROL = {F = 0, B = 0, L = 0, R = 0}
						SPEED = 0

						BG:destroy()
						BV:destroy()
					end)
				end

				mouse.KeyDown:connect(function(KEY)
					if KEY:lower() == 'w' then
						CONTROL.F = fly_speed

					elseif KEY:lower() == 's' then
						CONTROL.B = -fly_speed

					elseif KEY:lower() == 'a' then
						CONTROL.L = -fly_speed

					elseif KEY:lower() == 'd' then
						CONTROL.R = fly_speed

					end
				end)

				mouse.KeyUp:connect(function(KEY)
					if KEY:lower() == 'w' then
						CONTROL.F = 0
					elseif KEY:lower() == 's' then
						CONTROL.B = 0
					elseif KEY:lower() == 'a' then
						CONTROL.L = 0
					elseif KEY:lower() == 'd' then
						CONTROL.R = 0
					end
				end)

				start_fly()

				plr.Character.Torso.Anchored = false

				repeat wait() plr.Character.Humanoid.PlatformStand = false until not plr.Character.Humanoid
			end
		end
	else
		if plr.Character.Character then
			if plr.Character.Character:FindFirstChild("float_part") then
				plr.Character.Character:FindFirstChild("float_part"):Destroy()
			end
		end

		flying = false
	end
end


local function GetRandomTarget()
	for _ = 1, 10 do
		local randomPlayer = players[math.random(1, #players)]
		if randomPlayer ~= LP and randomPlayer.Character and randomPlayer.Character:FindFirstChild("HumanoidRootPart") then
			return randomPlayer.Character.HumanoidRootPart
		end
	end
	return nil
end

local function Noclip(char)
	local NoclipConnection;
	NoclipConnection = RS.Heartbeat:Connect(function()
		if not char then NoclipConnection:Disconnect() return end
		for _, v in ipairs(char:GetDescendants()) do
			if v:IsA("Part") or v:IsA("BasePart") then
				v.CanCollide = false
			end
		end
	end)
end

local function Desync(char)
	local DesyncConnection;
	DesyncConnection = RS.Heartbeat:Connect(function()
		if not char then DesyncConnection:Disconnect() return end

		local Old = char.HumanoidRootPart.AssemblyLinearVelocity

		char.HumanoidRootPart.AssemblyLinearVelocity = Vector3.new(1, 1, 1) * 16384

		RS.RenderStepped:Wait()

		char.HumanoidRootPart.AssemblyLinearVelocity = Old
	end)
end

local function X(Y: Model)
	local Stam = Y:WaitForChild("Stam")
	if not Stam then return end

	Stam.Changed:Connect(function(val)
		val = 100
		Stam.Value = 100
	end)

	local Pipe = LP.Backpack:FindFirstChild("Pipe")
	local Glock = LP.Backpack:FindFirstChild("Glock")

	if not Pipe or not Glock then return end
	Glock.Parent = Y

	local currentTarget = GetRandomTarget()

	Desync(Y); Noclip(Y); toggle_fly();

	Y.Humanoid.StateChanged:Connect(function(_, state)
		if state == Enum.HumanoidStateType.PlatformStanding then
			Y.Humanoid:ChangeState(Enum.HumanoidStateType.GettingUp) 
		end
	end)

	repeat	RS.Heartbeat:Wait()
		
		
		LP.Backpack.ServerTraits.Touch:FireServer(Pipe, Pipe.Handle, true, true); 
		
		pcall(function()
			GR:FireServer(currentTarget.CFrame + currentTarget.Velocity / 8)
		end)

		local PrimaryPart = Y:FindFirstChild("HumanoidRootPart")

		if not PrimaryPart then return end

		if Glock.Ammo.Value <= 0 and Glock.Clips.Value <= 0 then
			Y.Humanoid.Health = 0
		end

		if not currentTarget 
			or not currentTarget.Parent 
			or not currentTarget.Parent:FindFirstChildOfClass("Humanoid") 
			or currentTarget.Parent:FindFirstChildOfClass("Humanoid").Health <= 0 
			or currentTarget.Velocity.Magnitude > 200
			or currentTarget.Parent:FindFirstChild("KO")  then

			currentTarget = GetRandomTarget()
		end

		AirWalkPart.CFrame = PrimaryPart.CFrame + Vector3.new(0, -4, 0)

		if currentTarget then
			PrimaryPart.CFrame = PrimaryPart.CFrame:Lerp((currentTarget.CFrame + currentTarget.Velocity / 4.3), 1.2)
		end

	until not Y or Y:FindFirstChildOfClass("Humanoid").Health == 0
end

X(LP.Character)



LP.CharacterAdded:Connect(function(char)
	task.wait(0.2)
	X(char)
end)
