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
    floor.Parent = workspace

    return floor
end

local function updateLocalFloorPosition()
    if isActivated and humanoid and humanoidRootPart then
        if not localFloor then
            localFloor = createLocalFloor()
        end
        localFloor.Position = humanoidRootPart.Position - Vector3.new(0, humanoid.HipHeight + 3.5, 0) -- Чуть ниже ног
    elseif localFloor then
        localFloor:Destroy()
        localFloor = nil
    end
end

local function toggleLocalFloor()
    isActivated = not isActivated
    toggleButton.Text = isActivated and "Выкл" or "Вкл"
end

local gui = Instance.new("ScreenGui")
gui.Parent = player.PlayerGui

local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 100, 0, 30)
toggleButton.Position = UDim2.new(0.5, -50, 0, 10)
toggleButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
toggleButton.TextColor3 = Color3.new(1, 1, 1)
toggleButton.FontSize = Enum.FontSize.Size14
toggleButton.Text = "Вкл"
toggleButton.Parent = gui

toggleButton.MouseButton1Click:Connect(toggleLocalFloor)

-- Обновляем позицию пола под игроком только если кнопка включена
game:GetService("RunService").Stepped:Connect(updateLocalFloorPosition)
