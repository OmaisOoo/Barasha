local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer
local VehicleRemote = ReplicatedStorage:WaitForChild("RemoteFunction")
local Events = ReplicatedStorage:WaitForChild("Events")

local function autoFarm()
    while true do
        wait(0.5)
        local vehicle = workspace:FindFirstChild(LocalPlayer.Name.."'s Car")
        if vehicle and vehicle:FindFirstChild("DriveSeat") then
            vehicle:TranslateBy(Vector3.new(5, 0, 0))
        end
    end
end

local function noSpeedLimit()
    local vehicle = workspace:FindFirstChild(LocalPlayer.Name.."'s Car")
    if vehicle then
        local seat = vehicle:FindFirstChild("DriveSeat")
        if seat then
            seat.MaxSpeed = math.huge
        end
    end
end

local function buyLimitedCar(carName)
    Events:FindFirstChild("BuyCar"):FireServer(carName)
end

local gui = Instance.new("ScreenGui", game:GetService("CoreGui"))
gui.Name = "CDT_Farm_GUI"

local function createButton(text, posY, callback)
    local btn = Instance.new("TextButton", gui)
    btn.Size = UDim2.new(0, 200, 0, 40)
    btn.Position = UDim2.new(0, 10, 0, posY)
    btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Text = text
    btn.TextScaled = true
    btn.MouseButton1Click:Connect(callback)
end

createButton("Farm XP & Dinheiro", 0.1, function()
    spawn(autoFarm)
end)

createButton("Velocidade Infinita", 0.2, function()
    noSpeedLimit()
end)

createButton("Comprar Limited Car", 0.3, function()
    buyLimitedCar("JeskoAbsolute")
end)
