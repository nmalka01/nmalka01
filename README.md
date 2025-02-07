local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:FindFirstChildOfClass("Humanoid")

-- Create ScreenGui
local adminGui = Instance.new("ScreenGui")
adminGui.Name = "AdminPanel"
adminGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
adminGui.ResetOnSpawn = false

-- Create Main Frame
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0.3, 0, 0.4, 0)
mainFrame.Position = UDim2.new(0.35, 0, 0.3, 0)
mainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50) -- Light gray
mainFrame.BackgroundTransparency = 0.5 -- Transparent look
mainFrame.BorderSizePixel = 0
mainFrame.Draggable = true
mainFrame.Active = true
mainFrame.Visible = false
mainFrame.Parent = adminGui

-- Add UICorner for rounded edges
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0.1, 0) -- Smooth rounded edges
corner.Parent = mainFrame

-- Add UIStroke for a classy outline
local stroke = Instance.new("UIStroke")
stroke.Thickness = 1
stroke.Color = Color3.fromRGB(180, 180, 180) -- Light gray stroke
stroke.Parent = mainFrame

-- Create Toggle Button
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0.1, 0, 0.05, 0)
toggleButton.Position = UDim2.new(0.9, 0, 0.05, 0)
toggleButton.Text = "Admin"
toggleButton.TextScaled = true
toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggleButton.Parent = adminGui

toggleButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)

-- Create Title Label
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(0.8, 0, 0.1, 0)
titleLabel.Position = UDim2.new(0.1, 0, 0, 0)
titleLabel.Text = "Admin panel by nmalka01"
titleLabel.TextScaled = true
titleLabel.BackgroundTransparency = 1
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Font = Enum.Font.GothamBold
titleLabel.Parent = mainFrame

-- Create Buttons
local function createButton(text, position, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0.8, 0, 0.1, 0)
    button.Position = UDim2.new(0.1, 0, position, 0)
    button.Text = text
    button.TextScaled = true
    button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Parent = mainFrame
    button.MouseButton1Click:Connect(callback)
    
    -- Add UICorner & UIStroke for buttons
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0.1, 0)
    buttonCorner.Parent = button

    local buttonStroke = Instance.new("UIStroke")
    buttonStroke.Thickness = 1
    buttonStroke.Color = Color3.fromRGB(180, 180, 180)
    buttonStroke.Parent = button

    return button
end

-- Fly Function
local flying = false
function fly()
    local character = player.Character
    if not character then return end
    flying = not flying

    if flying then
        local bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.Velocity = Vector3.new(0, 50, 0)
        bodyVelocity.MaxForce = Vector3.new(4000, 4000, 4000)
        bodyVelocity.Name = "FlyVelocity"
        bodyVelocity.Parent = character:FindFirstChild("HumanoidRootPart")
    else
        if character:FindFirstChild("HumanoidRootPart") then
            local bv = character.HumanoidRootPart:FindFirstChild("FlyVelocity")
            if bv then bv:Destroy() end
        end
    end
end

createButton("Fly", 0.15, fly)

-- Speed Changer
createButton("Speed Boost", 0.3, function()
    humanoid.WalkSpeed = 100
end)

createButton("Reset Speed", 0.4, function()
    humanoid.WalkSpeed = 16
end)

-- Jump Power Changer
createButton("Jump Power Boost", 0.5, function()
    humanoid.JumpPower = 150
end)

createButton("Reset Jump Power", 0.6, function()
    humanoid.JumpPower = 50
end)

-- Kill Button
createButton("Kill", 0.7, function()
    humanoid.Health = 0
end)

-- Lag Server
createButton("Lag Server", 0.8, function()
    while true do end -- Infinite loop (⚠️ Crashes server!)
end)
