bewrewq=Instance.new("HopperBin",game.Players.LocalPlayer.Backpack)
bewrewq.BinType = "Script"
Tool = bewrewq
VELOCITY = 85 -- constant

local Pellet = Instance.new("Part")
Pellet.Locked = true
Pellet.BackSurface = 0
Pellet.BottomSurface = 0
Pellet.FrontSurface = 0
Pellet.LeftSurface = 0
Pellet.RightSurface = 0
Pellet.TopSurface = 0
Pellet.Shape = 0
Pellet.Size = Vector3.new(1,1,1)
Pellet.BrickColor = BrickColor.new(2)
script.Parent.PelletScript:clone().Parent = Pellet

function fire(mouse_pos)


	Tool.Handle.SlingshotSound:play()

-- find player's head pos

	local vCharacter = Tool.Parent
	local vPlayer = game.Players:playerFromCharacter(vCharacter)

	local head = vCharacter:findFirstChild("Head")
	if head == nil then return end

	local dir = mouse_pos - head.Position
	dir = computeDirection(dir)

	local launch = head.Position + 5 * dir

	local delta = mouse_pos - launch
	
	local dy = delta.y
	
	local new_delta = Vector3.new(delta.x, 0, delta.z)
	delta = new_delta

	local dx = delta.magnitude
	local unit_delta = delta.unit
	
	-- acceleration due to gravity in RBX units
	local g = (-9.81 * 20)

	local theta = computeLaunchAngle( dx, dy, g)

	local vy = math.sin(theta)
	local xz = math.cos(theta)
	local vx = unit_delta.x * xz
	local vz = unit_delta.z * xz
	

	local missile = Pellet:clone()
        

		

	missile.Position = launch
	missile.Velocity = Vector3.new(vx,vy,vz) * VELOCITY

	missile.PelletScript.Disabled = false

	local creator_tag = Instance.new("ObjectValue")
	creator_tag.Value = vPlayer
	creator_tag.Name = "creator"
	creator_tag.Parent = missile
	
	missile.Parent = game.Workspace

end


function computeLaunchAngle(dx,dy,grav)
	-- arcane
	-- http://en.wikipedia.org/wiki/Trajectory_of_a_projectile
	
	local g = math.abs(grav)
	local inRoot = (VELOCITY*VELOCITY*VELOCITY*VELOCITY) - (g * ((g*dx*dx) + (2*dy*VELOCITY*VELOCITY)))
	if inRoot <= 0 then
		return .25 * math.pi
	end
	local root = math.sqrt(inRoot)
	local inATan1 = ((VELOCITY*VELOCITY) + root) / (g*dx)

	local inATan2 = ((VELOCITY*VELOCITY) - root) / (g*dx)
	local answer1 = math.atan(inATan1)
	local answer2 = math.atan(inATan2)
	if answer1 < answer2 then return answer1 end
	return answer2
end

function computeDirection(vec)
	local lenSquared = vec.magnitude * vec.magnitude
	local invSqrt = 1 / math.sqrt(lenSquared)
	return Vector3.new(vec.x * invSqrt, vec.y * invSqrt, vec.z * invSqrt)
end




Tool.Enabled = true
function onActivated()

	if not Tool.Enabled then
		return
	end

	Tool.Enabled = false

	local character = Tool.Parent;
	local humanoid = character.Humanoid
	if humanoid == nil then
		print("Humanoid not found")
		return 
	end

	local targetPos = humanoid.TargetPoint

	fire(targetPos)

	wait(.2)

	Tool.Enabled = true
end

script.Parent.Activated:connect(onActivated)



--rbxsig%ilw2odzZI2P3k/y9QiKZ3aRTsqyw93zGU8wTXg0/rXW3eXl6y0c8+A52nyYnuu8Ut91L6KXvKHg27ylK6b8+djUE6EfxBttSkr8L1f6sXij6S5KwLQDMK7gMsDT+ec53tSNkqwT5rhFTM9BIXtSs3i+QixnAVdFOzhjy4sM51Sw=%
--rbxassetid%1014650%
local Tool = script.Parent;

enabled = true
function onButton1Down(mouse)
	if not enabled then
		return
	end

	enabled = false
	mouse.Icon = "rbxasset://textures\\GunWaitCursor.png"

	wait(.2)
	mouse.Icon = "rbxasset://textures\\GunCursor.png"
	enabled = true

end

function onEquippedLocal(mouse)

	if mouse == nil then
		print("Mouse not found")
		return 
	end

	mouse.Icon = "rbxasset://textures\\GunCursor.png"
	mouse.Button1Down:connect(function() onButton1Down(mouse) end)
end



Tool.Equipped:connect(onEquippedLocal)


--rbxsig%TtFgSww3tb7yQWlKIIy4M4/MD5STLZbfqPBwW4DbPx0BCKsj2+ToL2oGyOtsWQOVsHx1cfXkfOoQpO4JFeQPhij7R1Vai4rh9hiIXYw35M0sKeq/0WYEhg/3rqRE/ItBoW+2YFGu+AyxWt8nvIMoPfoyZ/JBItmU3uN4WOfYWtM=%
--rbxassetid%1014652%
local debris = game:service("Debris")
pellet = script.Parent
damage = 8

function onTouched(hit)
	humanoid = hit.Parent:findFirstChild("Humanoid")
	if humanoid~=nil then
		tagHumanoid(humanoid)
		humanoid:TakeDamage(damage)
	else
		damage = damage / 2
		if damage < 1 then
			connection:disconnect()
			pellet.Parent = nil
		end
	end
end

function tagHumanoid(humanoid)
	-- todo: make tag expire
	local tag = pellet:findFirstChild("creator")
	if tag ~= nil then
		-- kill all other tags
		while(humanoid:findFirstChild("creator") ~= nil) do
			humanoid:findFirstChild("creator").Parent = nil
		end

		local new_tag = tag:clone()
		new_tag.Parent = humanoid
		debris:AddItem(new_tag, 1)
	end
end

connection = pellet.Touched:connect(onTouched)

r = game:service("RunService")
t, s = r.Stepped:wait()
d = t + 2.0 - s
while t < d do
	t = r.Stepped:wait()
end

pellet.Parent = nil
