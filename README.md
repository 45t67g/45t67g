-- Gui to Lua
-- Version: 3.2
 
-- Instances:
 
local DesX = Instance.new("ScreenGui")
local GUI = Instance.new("Frame")
local Menu = Instance.new("Frame")
local Fly = Instance.new("TextButton")
local Destroy = Instance.new("TextButton")
local Options = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
 
--Properties:
 
DesX.Name = "DesX"
DesX.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
DesX.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
 
GUI.Name = "GUI"
GUI.Parent = DesX
GUI.BackgroundColor3 = Color3.fromRGB(62, 62, 62)
GUI.BorderColor3 = Color3.fromRGB(255, 255, 255)
GUI.Position = UDim2.new(0.00606060587, 0, 0.425992757, 0)
GUI.Size = UDim2.new(0, 357, 0, 465)
 
Menu.Name = "Menu"
Menu.Parent = GUI
Menu.BackgroundColor3 = Color3.fromRGB(109, 109, 109)
Menu.BorderColor3 = Color3.fromRGB(255, 255, 255)
Menu.Position = UDim2.new(0.0200819336, 0, 0.18720381, 0)
Menu.Size = UDim2.new(0.957193434, 0, 0.792558312, 0)
 
Fly.Name = "Fly"
Fly.Parent = Menu
Fly.BackgroundColor3 = Color3.fromRGB(71, 71, 71)
Fly.BorderColor3 = Color3.fromRGB(255, 255, 255)
Fly.Position = UDim2.new(0.0174418613, 0, 0.0160995834, 0)
Fly.Size = UDim2.new(0, 71, 0, 42)
Fly.Font = Enum.Font.SciFi
Fly.Text = "FLY"
Fly.TextColor3 = Color3.fromRGB(255, 255, 255)
Fly.TextSize = 32.000
 
Destroy.Name = "Destroy"
Destroy.Parent = Menu
Destroy.BackgroundColor3 = Color3.fromRGB(167, 117, 107)
Destroy.BorderColor3 = Color3.fromRGB(255, 255, 255)
Destroy.Position = UDim2.new(0.459326655, 0, 0.868111253, 0)
Destroy.Size = UDim2.new(0, 178, 0, 42)
Destroy.Font = Enum.Font.SciFi
Destroy.Text = "Destroy GUI"
Destroy.TextColor3 = Color3.fromRGB(255, 255, 255)
Destroy.TextSize = 32.000
 
Options.Name = "Options"
Options.Parent = GUI
Options.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Options.BackgroundTransparency = 1.000
Options.Position = UDim2.new(0.0171918683, 0, -0.13032043, 0)
Options.Size = UDim2.new(0.751265407, 0, 0.149442971, 0)
 
TextLabel.Parent = Options
TextLabel.BackgroundColor3 = Color3.fromRGB(167, 167, 167)
TextLabel.BorderColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.Position = UDim2.new(0.00384693057, 0, 0.987247944, 0)
TextLabel.Size = UDim2.new(1.27410817, 0, 1.00568652, 0)
TextLabel.Font = Enum.Font.SciFi
TextLabel.LineHeight = 1.060
TextLabel.Text = "Deskari"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextScaled = true
TextLabel.TextSize = 96.000
TextLabel.TextWrapped = true
 
-- Scripts:
 
local function GMAPA_fake_script() -- Fly.LocalScript 
    local script = Instance.new('LocalScript', Fly)
 
    local Button = script.Parent
    
    Button.MouseButton1Click:Connect(function()
        repeat wait() 
        until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Head") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid") 
        local mouse = game.Players.LocalPlayer:GetMouse() 
        repeat wait() until mouse
        local plr = game.Players.LocalPlayer 
        local torso = plr.Character.Head 
        local flying = false
        local deb = true 
        local ctrl = {f = 0, b = 0, l = 0, r = 0} 
        local lastctrl = {f = 0, b = 0, l = 0, r = 0} 
        local maxspeed = 400 
        local speed = 5000 
    
        local function Fly() 
            local bg = Instance.new("BodyGyro", torso) 
            bg.P = 9e4 
            bg.maxTorque = Vector3.new(9e9, 9e9, 9e9) 
            bg.cframe = torso.CFrame 
            local bv = Instance.new("BodyVelocity", torso) 
            bv.velocity = Vector3.new(0,0.1,0) 
            bv.maxForce = Vector3.new(9e9, 9e9, 9e9) 
            repeat wait() 
                plr.Character.Humanoid.PlatformStand = true 
                if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then 
                    speed = speed+.5+(speed/maxspeed) 
                    if speed > maxspeed then 
                        speed = maxspeed 
                    end 
                elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then 
                    speed = speed-1 
                    if speed < 0 then 
                        speed = 0 
                    end 
                end 
                if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then 
                    bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
                    lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r} 
                elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then 
                    bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed 
                else 
                    bv.velocity = Vector3.new(0,0.1,0) 
                end 
                bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0) 
            until not flying 
            ctrl = {f = 0, b = 0, l = 0, r = 0} 
            lastctrl = {f = 0, b = 0, l = 0, r = 0} 
            speed = 0 
            bg:Destroy() 
            bv:Destroy() 
            plr.Character.Humanoid.PlatformStand = false 
        end 
        mouse.KeyDown:connect(function(key) 
            if key:lower() == "e" then 
                if flying then flying = false 
                else 
                    flying = true 
                    Fly() 
                end 
            elseif key:lower() == "w" then 
                ctrl.f = 1 
            elseif key:lower() == "s" then 
                ctrl.b = -1 
            elseif key:lower() == "a" then 
                ctrl.l = -1 
            elseif key:lower() == "d" then 
                ctrl.r = 1 
            end 
        end) 
        mouse.KeyUp:connect(function(key) 
            if key:lower() == "w" then 
                ctrl.f = 0 
            elseif key:lower() == "s" then 
                ctrl.b = 0 
            elseif key:lower() == "a" then 
                ctrl.l = 0 
            elseif key:lower() == "d" then 
                ctrl.r = 0 
            end 
        end)
        Fly()
    end)
end
coroutine.wrap(GMAPA_fake_script)()
local function AARBK_fake_script() -- Destroy.DestroyScript 
    local script = Instance.new('LocalScript', Destroy)
 
    local Button = script.Parent
    
    Button.MouseButton1Click:Connect(function()
        script.Parent.Parent.Parent.Parent:Destroy()
    end)
end
coroutine.wrap(AARBK_fake_script)()
local function TXYX_fake_script() -- GUI.Dragify 
    local script = Instance.new('LocalScript', GUI)
 
    local UserInputService = game:GetService("UserInputService")
    
    local gui = script.Parent
    
    local dragging
    local dragInput
    local dragStart
    local startPos
    
    local function update(input)
        local delta = input.Position - dragStart
        gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
    
    gui.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = gui.Position
    
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)
    
    gui.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)
    
    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            update(input)
        end
    end)
end
coroutine.wrap(TXYX_fake_script)()
