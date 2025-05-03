-- CONFIGURAÇÕES
local PALAVRA_MORTAL = "ola" -- Reset ao digitar "ola"
local COMANDO_PREFIXO = "/"   -- Prefixo para comandos
local Players = game:GetService("Players")
local TextChatService = game:GetService("TextChatService")
local RunService = game:GetService("RunService")

-- FUNÇÕES PRINCIPAIS
local function MATAR_PLAYER()
    local player = Players.LocalPlayer
    if player.Character then
        player.Character:BreakJoints()
        print("[MORTE] Personagem resetado!")
    end
end

local function ENVIAR_COCO()
    print("[COMANDO] Mandando coco...") -- Substitua por ação real
    -- Exemplo: Criar uma partícula de "coco" no jogo
end

-- ANALISADOR DE COMANDOS
local function ANALISAR_CHAT(message)
    local msg = string.lower(message)
    
    -- Reset por "ola"
    if msg == PALAVRA_MORTAL then
        MATAR_PLAYER()
    
    -- Sistema de comandos
    elseif string.sub(msg, 1, 1) == COMANDO_PREFIXO then
        local comando = string.sub(msg, 2) -- Remove o "/"
        
        if comando == "manda coco" then
            ENVIAR_COCO()
        -- Adicione outros comandos aqui
        end
    end
end

-- AUTO-REEXECUÇÃO EM TELETRANSPORTE
local function CONFIGURAR_AUTO_REEXECUTE()
    if syn and syn.queue_on_teleport then
        syn.queue_on_teleport([[
            wait(2)
            loadstring(game:HttpGet("URL_DO_SCRIPT"))()
        ]])
    end
end

-- INICIALIZAÇÃO
CONFIGURAR_AUTO_REEXECUTE()

-- MONITORAMENTO DO CHAT
if TextChatService then
    TextChatService.OnIncomingMessage = function(message)
        ANALISAR_CHAT(message.Text)
        return message
    end
else
    game:GetService("Chat").Chatted:Connect(ANALISAR_CHAT)
end

print("[SISTEMA] Ativo! Comandos:")
print("- Digite '"..PALAVRA_MORTAL.."' para resetar")
print("- Use '/manda coco' para ação especial")
