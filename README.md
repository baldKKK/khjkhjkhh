# local User = "The77KK" -- Substitua pelo seu nome de usuário exato

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

-- Função para verificar o comando no chat
local function onPlayerChatted(player, message)
        local args = string.split(message, " ")  -- Divide a mensagem em palavras
        if args[1]:lower() == "!arma" then  -- Se o comando for "!arma"
            local armaNome = args[2]  -- Pega o nome da arma digitada

            -- Verifica se a arma existe no ReplicatedStorage
            local arma = ReplicatedStorage:FindFirstChild(armaNome)
            if arma then
                local backpack = player:FindFirstChild("Backpack")
                if backpack then
                    local armaClone = arma:Clone()
                    armaClone.Parent = backpack
                    player.Character.Humanoid:EquipTool(armaClone) -- Equipa automaticamente
                    player:LoadCharacter() -- Garante que a arma não bugue
                end
            else
                player:Kick("Arma não encontrada!")  -- Kicka se o nome estiver errado
            end
        end
    end
end

-- Conectar evento ao chat
Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(message)
        onPlayerChatted(player, message)
    end)
end)
