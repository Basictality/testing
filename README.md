x=Instance.new("HopperBin",game.Players.LocalPlayer.Backpack)
x.BinType = "Script"
local dragging;
local center;
local scale;

local camera = game.Workspace.CurrentCamera

local part = Instance.new("Part")
part.FormFactor = Enum.FormFactor.Symmetric
part.Size = Vector3.new(1,1,1)
part.Anchored = true
part.Transparency = .6
part.BrickColor = BrickColor.Green()

local mesh = Instance.new("SpecialMesh", part)
mesh.MeshType = Enum.MeshType.FileMesh
mesh.MeshId = "http://www.roblox.com/asset/?id=1185246"

x.Selected:connect(function(mouse)
	mouse.Button1Down:connect(function()
		dragging = true
		center = mouse.Hit.p
		part.CFrame = CFrame.new(center)
		part.Parent = camera
		scale = 1
		mesh.Scale = Vector3.new(1,1,1)
	end)
	mouse.Move:connect(function()
		if not dragging then return end
		scale = (center - mouse.Hit.p).magnitude * 3
		scale = scale <= 60 and scale or 60
		mesh.Scale = Vector3.new(scale, scale, scale)
	end)
	mouse.Button1Up:connect(function()
		dragging = false
		part.Parent = nil
		local boom = Instance.new("Explosion", game.Workspace)
		boom.BlastRadius = scale/3
		boom.Position = center
	end)
end)
