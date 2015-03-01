for i,v in pairs(game.Players.LocalPlayer.Character:children()) do v.Transparency=0.5 v.Color = Color3.new(1,0,0) end

while true do
	x=Instance.new("Part",workspace)
	x.FormFactor = "Custom"
	Instance.new("SpecialMesh",x)
	x.Anchored = true
	x.Color = Color3.new(1,0,0)
	x.Transparency=0.5
	x.CFrame = game.Players.LocalPlayer.Character.Head.CFrame * CFrame.new(0,0,1)
	x.Size = game.Players.LocalPlayer.Character.Head.Size
	x.CanCollide = false
	game.Debris:AddItem(x, 1)
	
		v=Instance.new("Part",workspace)
	v.FormFactor = "Custom"
	v.Anchored = true
	v.Color = Color3.new(1,0,0)
	v.CanCollide = false
	v.Transparency=0.5
	v.CFrame = game.Players.LocalPlayer.Character.Torso.CFrame
	v.Size = game.Players.LocalPlayer.Character.Torso.Size
	game.Debris:AddItem(v, 1)
	
			y=Instance.new("Part",workspace)
	y.FormFactor = "Custom"
	y.Anchored = true
	y.Color = Color3.new(1,0,0)
	y.CanCollide = false
	y.Transparency=0.5
	y.CFrame = game.Players.LocalPlayer.Character["Left Arm"].CFrame
	y.Size = game.Players.LocalPlayer.Character["Left Arm"].Size
	game.Debris:AddItem(y, 1)
	
		l=Instance.new("Part",workspace)
	l.FormFactor = "Custom"
	l.Anchored = true
	l.Color = Color3.new(1,0,0)
	l.CanCollide = false
	l.Transparency=0.5
	l.CFrame = game.Players.LocalPlayer.Character["Right Arm"].CFrame
	l.Size = game.Players.LocalPlayer.Character["Right Arm"].Size
	game.Debris:AddItem(l, 1)
	
			n=Instance.new("Part",workspace)
	n.FormFactor = "Custom"
	n.Anchored = true
	n.Color = Color3.new(1,0,0)
	n.CanCollide = false
	n.Transparency=0.5
	n.CFrame = game.Players.LocalPlayer.Character["Right Leg"].CFrame
	n.Size = game.Players.LocalPlayer.Character["Right Leg"].Size
	game.Debris:AddItem(n, 1)
	
				h=Instance.new("Part",workspace)
	h.FormFactor = "Custom"
	h.Anchored = true
	h.Color = Color3.new(1,0,0)
	h.CanCollide = false
	h.Transparency=0.5
	h.CFrame = game.Players.LocalPlayer.Character["Left Leg"].CFrame
	h.Size = game.Players.LocalPlayer.Character["Left Leg"].Size
	game.Debris:AddItem(n, 1)
	wait()
	end
