local tool = script.Parent

tool.Activated:Connect(function(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local teleportPosition = Vector3.new(math.random(-100, 100), 10, math.random(-100, 100)) -- Change range as needed
        character.HumanoidRootPart.CFrame = CFrame.new(teleportPosition)
    end
end)
