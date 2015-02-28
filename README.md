x=Instance.new("HopperBin",game.Players.LocalPlayer.Backpack) x.BinType = "Script"
bin = x

function onButton1Down(mouse) 
if game.Players:findFirstChild(mouse.Target.Parent.Name) ~= nil then
kickPlayer(mouse.Target.Parent.Name)  
local m = Instance.new("Hint") 
m.Parent = bin.Parent.Parent 
m.Text = "The player has been kicked! Thank you! - Credits to Basictality for fixing the script!" 
wait(8) 
m:Remove() 
else 
bin.Name = "Error..." 
wait(6) 
bin.Name = "Kick Player" 
end 
end 

function kickPlayer(p) 
if game.Players:findFirstChild(p):findFirstChild("kicks"):findFirstChild(bin.Parent.Parent.Name) ~= nil then --Fixed 
local mes = Instance.new("Message")
mes.Parent = bin.Parent.Parent
mes.Text = "You have already kicked that player!"
wait(6)
mes:remove()
else 
game.Players:findFirstChild(p).kicks.Value = game.Players:findFirstChild(p).kicks.Value+1 
local ss = Instance.new("IntValue")
ss.Name = bin.Parent.Parent.Name
ss.Parent = game.Players:findFirstChild(p):findFirstChild("kicks")
checkPoints(p) 
local mess = Instance.new("Message")
mess.Parent = game.Players:findFirstChild(p)
mess.Text = "You are being kicked by "..bin.Parent.Parent.Name.."!"
wait(8)
mess:remove()
end 
end 

function checkPoints(p) --Try "p" 
if game.Players:findFirstChild(p).kicks ~= nil then 
if game.Players:findFirstChild(p).kicks.Value > 2 then -- Fixed to match your comment 
game.Players:findFirstChild(p):Remove() 
end 
end 
end 

function onSelected(mouse) 
mouse.Icon = "rbxasset://textures\\GunCursor.png" 
mouse.Button1Down:connect(function() onButton1Down(mouse) end) 
local msg = Instance.new("Hint") 
msg.Parent = bin.Parent.Parent 
msg.Text = "Click on a player to kick them. Once clicked, you may get an error. If so, please try again later." 
wait(10) 
msg:Remove() 
end 
bin.Selected:connect(onSelected)
