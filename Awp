local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local humanoid = character:WaitForChild("Humanoid")

local isActivated = false
local localFloor = nil

local function createLocalFloor()
    local floor = Instance.new("Part")
    floor.Size = Vector3.new(10, 1, 10)
    floor.Anchored = true
    floor.CanCollide = true
    floor.Transparency = 0.5
    floor.Color = Color3.new(0.8, 0.8, 0.8)
    floor.Parent = workspace
    return floor
end

local function updateLocalFloorPosition()
    if isActivated and humanoid and humanoidRootPart then
        if not localFloor then
            localFloor = createLocalFloor()
        end
        localFloor.Position = humanoidRootPart.Position - Vector3.new(0, humanoid.HipHeight + 1.5, 0)
    elseif localFloor then
        localFloor:Destroy()
        localFloor = nil
    end
end

local function toggleLocalFloor()
    isActivated = not isActivated
    toggleButton.Text = isActivated and "OFF" or "ON"
    toggleButton.BackgroundColor3 = isActivated and Color3.new(0.8, 0.2, 0.2) or Color3.new(0.2, 0.8, 0.2)
end

local gui = Instance.new("ScreenGui")
gui.Parent = player.PlayerGui

local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 80, 0, 30)
toggleButton.Position = UDim2.new(0.5, -40, 0.9, 0)
toggleButton.BackgroundColor3 = Color3.new(0.2, 0.8, 0.2)
toggleButton.TextColor3 = Color3.new(1, 1, 1)
toggleButton.Font = Enum.Font.SourceSansBold
toggleButton.TextSize = 14
toggleButton.Text = "ON"
toggleButton.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 8)
corner.Parent = toggleButton

toggleButton.MouseButton1Click:Connect(toggleLocalFloor)

game:GetService("RunService").Stepped:Connect(updateLocalFloorPosition)
