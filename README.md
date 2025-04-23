local GinIngerto = {
    Menus = {},
    States = {}
}

-- Khởi tạo menu và trạng thái
local menuNames = {"Player", "Vehicle", "World", "Troll"}

local functions = {
    Player = {
        "God Mode", "Infinite Ammo", "Super Jump", "Fast Run", "Invisible",
        "No Wanted", "Teleport to WP", "Infinite Stamina", "Health Regen", "Seatbelt"
    },
    Vehicle = {
        "Vehicle God Mode", "Spawn Supercar", "Boost", "Drift Mode", "Repair",
        "Rainbow Paint", "Fly Mode", "Gravity Toggle", "Eject", "Vehicle Jump"
    },
    World = {
        "Change Weather", "Freeze Time", "Blackout", "Earthquake", "Spawn Peds",
        "Explode Cars", "Teleport All", "Zombie Mode", "Clear Area", "Slow Motion"
    },
    Troll = {
        "Explode Player", "Cage", "Launch Air", "Fake Ban", "Force Dance",
        "Lag Spike", "Attach Object", "Steal Car", "Random Skin", "Animal Morph"
    }
}

-- Khởi tạo từng menu với trạng thái OFF
for _, menu in ipairs(menuNames) do
    GinIngerto.Menus[menu] = functions[menu]
    GinIngerto.States[menu] = {}
    for i, func in ipairs(functions[menu]) do
        GinIngerto.States[menu][func] = false -- OFF ban đầu
    end
end

-- Hiển thị Menu
function GinIngerto:ShowMenu()
    print("\n==== GIN INGERTÔ MENU ====\n")
    for _, menu in ipairs(menuNames) do
        print("---- " .. menu .. " Options ----")
        for i, func in ipairs(self.Menus[menu]) do
            local state = self.States[menu][func] and "[ON]" or "[OFF]"
            print(i .. ". " .. func .. " " .. state)
        end
        print("")
    end
end

-- Bật / Tắt chức năng
function GinIngerto:ToggleFunction(menu, funcIndex)
    local funcName = self.Menus[menu][funcIndex]
    local current = self.States[menu][funcName]
    self.States[menu][funcName] = not current
    local newState = self.States[menu][funcName] and "BẬT" or "TẮT"
    print(">> " .. funcName .. " đã " .. newState)
end

-- Ví dụ sử dụng
GinIngerto:ShowMenu()
GinIngerto:ToggleFunction("Player", 1) -- Bật God Mode
GinIngerto:ToggleFunction("Vehicle", 3) -- Bật Boost
GinIngerto:ShowMenu()

return GinIngerto
