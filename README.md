-- Criação do GUI
local ScreenGui = Instance.new("ScreenGui")
local OpenButton = Instance.new("TextButton")
local Frame = Instance.new("Frame")
local TeleportButton = Instance.new("TextButton")

-- Propriedades do ScreenGui
ScreenGui.Name = "TeleportMenu"
ScreenGui.Parent = game.CoreGui

-- Propriedades do OpenButton
OpenButton.Name = "OpenButton"
OpenButton.Parent = ScreenGui
OpenButton.Text = "Abrir Menu"
OpenButton.Size = UDim2.new(0, 100, 0, 50)
OpenButton.Position = UDim2.new(0, 10, 0, 10)

-- Propriedades do Frame
Frame.Name = "MenuFrame"
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 200, 0, 200)
Frame.Position = UDim2.new(0.5, -100, 0.5, -100)
Frame.Visible = false

-- Propriedades do TeleportButton
TeleportButton.Name = "TeleportButton"
TeleportButton.Parent = Frame
TeleportButton.Text = "Ativar Teleporte"
TeleportButton.Size = UDim2.new(0, 180, 0, 50)
TeleportButton.Position = UDim2.new(0.5, -90, 0.5, -25)

-- Variáveis de controle
local teleportEnabled = false
local itemName = "TeleportItem"

-- Função para abrir/fechar o menu
OpenButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

-- Função para ativar/desativar o teleporte
TeleportButton.MouseButton1Click:Connect(function()
    teleportEnabled = not teleportEnabled
    if teleportEnabled then
        TeleportButton.Text = "Desativar Teleporte"
        -- Adiciona o item ao inventário
        local player = game.Players.LocalPlayer
        local backpack = player:FindFirstChild("Backpack")
        if backpack and not backpack:FindFirstChild(itemName) then
            local item = Instance.new("Tool")
            item.Name = itemName
            item.Parent = backpack
        end
    else
        TeleportButton.Text = "Ativar Teleporte"
    end
end)

-- Função para teleporte
game.Players.LocalPlayer:GetMouse().Button1Down:Connect(function()
    if teleportEnabled then
        local player = game.Players.LocalPlayer
        local character = player.Character
        local mouse = player:GetMouse()
        if character and character:FindFirstChild(itemName) then
            character:SetPrimaryPartCFrame(CFrame.new(mouse.Hit.p))
        end
    end
end)
