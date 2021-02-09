# Shootout _Remastered_: Framework
The framework. When it comes to FPS games the _framework_ is the brain of the game and its one of the two parts to make FPS game work.
The framework is written by me in Luau, a language that roblox studio uses. Its really easy and lightweight.
### How it works
My framework is made to work for different guns and be really customizable. That was the first and **really** worth it sacrifice of my gun system. Instead of putting the modules
inside module folders I put the modules right into the guns. That gave me much more customizability. Why did I do that? Read _Animations_.

So lets get started:
- In my framework it all starts with the function:
```lua
equip(weapon) --a basic calling of a lua function
```
- Where the magic happens:
```lua
function equip()
    --not gonna show you my code (this is not a tutorial)
end
```
This would work but it would only for a second. Thats where _Run Service_ comes in handy.
```lua
game:GetService("RunService").RenderStepped:Connect(function()
    --here we can set the the viewmodel position to the cameras position
end)
```
But you didn't come here to see how every single system works didn't you? So why is mine special? Because of this:
```lua
game:GetService("RunService").RenderStepped:Connect(function()
    LeftArm:SetPrimaryPartCFrame(
    LeftArm.PrimaryPart.CFrame
    * weaponmodule.LArmCF
    )
end)
```
This is why I sacrificed the aesthetics for function.

**Not Finished**
### Animations
Animations in my framework aren't made with blender or moon animator or that fancy stuff. They are made with CFrames
If you know a bit of coding and you have played phantom forces you might now that in phantom forces there are no animations, they are CFrames. But isn't animations a line of
CFrames? Well yes, but actually no. Animations also tween the CFrames,
while in my framework I have to do it manually.

My actualy reload from the game:
```lua
Settings.Reload = function()
	Settings.MainCF = CFrame.new(.8, -1, -1.5) * CFrame.Angles(math.rad(10),math.rad(5),math.rad(-10))
	wait(0.1)
	Settings.LArmCF = CFrame.new(-0.3,-0.7,-0.2) * CFrame.Angles(math.rad(-70),math.rad(-10),math.rad(-25))
	wait(1)
	script.Parent.Mag.Parent = workspace.CurrentCamera:WaitForChild("LeftArm")
	Settings.MainCF = CFrame.new(.8, -1.1, -1.5) * CFrame.Angles(0,0,0)
	Settings.LArmCF = CFrame.new(-0.3,-1.5,-0.2) * CFrame.Angles(math.rad(-70),math.rad(-10),math.rad(-25))
	script.Parent.Handle.MagOut:Play()
	wait(0.5)
	Settings.MainCF = CFrame.new(.8, -1, -1.5) * CFrame.Angles(0,0,0)
	wait(1)
	Settings.MainCF = CFrame.new(.8, -0.9, -1.5) * CFrame.Angles(0,0,0)
	Settings.LArmCF = CFrame.new(-0.3,-0.7,-0.2) * CFrame.Angles(math.rad(-70),math.rad(-10),math.rad(-25))
	Settings.MainCF = CFrame.new(.8, -1, -1.5) * CFrame.Angles(math.rad(10),math.rad(5),math.rad(-10))
	script.Parent.Handle.MagIn:Play()
	wait(0.5)
	Settings.MainCF = CFrame.new(.8, -1, -1.5) * CFrame.Angles(0,0,0)
	wait(0.5)
	workspace.CurrentCamera:WaitForChild("LeftArm").Mag.Parent = script.Parent
	Settings.LArmCF = CFrame.new(-0.3,-0.3,-1) * CFrame.Angles(math.rad(-70),math.rad(-25),math.rad(-25))
	Settings.StoredMags = Settings.StoredMags - 1
	Settings.CurrentMag = Settings.MagSize
	print(Settings.StoredMags)
end
```
