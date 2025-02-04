local player = game.Players.LocalPlayer

local rewards = ""
local completionStats = ""

local endScreen = player.PlayerGui.Interface.Rewards.Main.Info.Main
local stats = endScreen.Stats
local items = endScreen.Items

local function SendNotification()
	local data = {
		["content"] = "",
		["embeds"] = {
			{
				["title"] = "**Rewards Logger**",
				["description"] = "Game ended for: "..player.Name..". Here are the rewards and stats:",
            	["color"] = tonumber(0xffffff),
            	["fields"] = {
					{
						["name"] = "Rewards",
						["value"] = rewards
					},
					{
						["name"] = "Stats",
						["value"] = completionStats
					}
				}
			}
		}
	}

	local newdata = game:GetService("HttpService"):JSONEncode(data)

	local headers = {
		["content-type"] = "application/json"
	}
	
	local request = http_request or request or HttpPost or syn.request
	local abcdef = {Url = WebHook, Body = newdata, Method = "POST", Headers = headers}
	
	request(abcdef)
end

local function SetTables()
	for _, item in pairs(items:GetChildren()) do
		if not item:IsA("Frame") then
			continue
		end

		local name = item.Name
		local value = item.Main.Inner.Quantity.Text
	
		rewards = rewards .. name .. ": " .. tostring(value) .. "\n"
	end

	for _, stat in pairs(stats:GetChildren()) do
		if not stat:IsA("Frame") then
			continue
		end

		local name = stat.Stat.Text
		local value = stat.Amount.Text
	
		completionStats = completionStats .. name .. ": " .. tostring(value) .. "\n"
	end

	SendNotification()
end

while not player.PlayerGui.Interface.Rewards.Visible == true do
	wait(1)
end

SetTables()


