# LUA_AI_GMod
Welcome for my tutorial on how to use my twitch chat lua ai gmod thing

Start your messages with ! to signify "hey this should be converted to code"
It then gets sent to an AI to convert to lua code

For example:

User: !spawn a ring of 50 combine soldiers that orbit the player

Lua:
 ```lua
if SERVER then
	local ply = Entity(1)
	local soldiers = {}
	local count = 50
	local radius = 200
	local speed = 2
	
	-- Spawn soldiers
	for i = 1, count do
		local angle = (i / count) * math.pi * 2
		
		local ent = ents.Create("npc_combine_s")
		ent:SetPos(ply:GetPos() + Vector(math.cos(angle) * radius, math.sin(angle) * radius, 0))
		ent:Spawn()
		
		table.insert(soldiers, ent)
	end
	
	-- Orbit using physics
	hook.Add("Think", "OrbitCombineSoldiers", function()
		if not IsValid(ply) then return end
		
		for i, ent in ipairs(soldiers) do
			if not IsValid(ent) then continue end
			
			local angle = CurTime() * speed + (i / #soldiers) * math.pi * 2
			local target = ply:GetPos() + Vector(math.cos(angle) * radius, math.sin(angle) * radius, 0)
			
			ent:SetPos(target)
		end
	end)
end
 ```

Some things it can do (in no particular order):
- Spawn props
- Give special properties to props and stuff
- Give weapons
- Create new weapons
- Create new npcs (nextbots technically)
- Put circles and squares on screen
- Create popups
- Interact with chat
- Run console commands (though limited for protection)
- Nearly any lua code
- Use VOX (it's an addon for GMod)
- Blow up players
- Launch players into the sky
- Teleport players
- Get images from the internet
- Change level
