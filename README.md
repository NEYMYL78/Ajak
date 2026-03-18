local UIS = game:GetService("UserInputService")
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- Ссылка на объект анимации, который вы создали ранее
local animObject = script.Parent:WaitForChild("AttackAnim")
local loadAnim = humanoid:LoadAnimation(animObject)

local debounce = false -- Переменная для "кулдауна" (перезарядки)
local cooldownTime = 1.0 -- Время в секундах между атаками

UIS.InputBegan:Connect(function(input, processed)
    if processed then return end -- Игнорируем, если игрок пишет в чат
    
    -- Проверяем нажатие клавиши F и отсутствие активной перезарядки
    if input.KeyCode == Enum.KeyCode.F and not debounce then
        debounce = true
        
        loadAnim:Play() -- Запуск анимации
        print("Атака!")
        
        -- Здесь можно добавить RemoteEvent для нанесения урона на сервере
        
        task.wait(cooldownTime) -- Ожидание перезарядки
        debounce = false
    end
end)
