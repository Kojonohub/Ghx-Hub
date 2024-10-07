-- Blox Fruits Auto-Farm Script
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Função para coletar frutas
function collectFruits()
    for _, item in pairs(workspace:GetChildren()) do
        if item:IsA("Fruit") and item:FindFirstChild("TouchInterest") then
            item:Destroy()  -- Coleta a fruta
        end
    end
end

-- Função para atacar inimigos próximos
function attackEnemies()
    for _, enemy in pairs(workspace:GetChildren()) do
        if enemy:IsA("NPC") and enemy:FindFirstChild("Humanoid") then
            local humanoid = enemy.Humanoid
            if humanoid.Health > 0 then
                character:MoveTo(enemy.Position)
                wait(1)  -- Aguarda um segundo antes de atacar
                fireclickdetector(enemy:FindFirstChild("ClickDetector")) -- Simula o ataque
            end
        end
    end
end

-- Função principal para auto-farm
function autoFarm()
    while wait(5) do
        collectFruits()   -- Coleta frutas
        attackEnemies()   -- Ataca inimigos
    end
end

-- Inicia o auto-farm
autoFarm()
