local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Redux exploit",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Loading yeahh",
   LoadingSubtitle = "by Femboy Hub",
   ShowText = "Femboy Hub", -- for mobile users to unhide rayfield, change if you'd like
   Theme = "Default", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   ToggleUIKeybind = "K", -- The keybind to toggle the UI visibility (string like "K" or Enum.KeyCode)

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub right"
   },

   Discord = {
      Enabled = false, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

   KeySystem = false, -- Set this to true to use our key system
   KeySettings = {
      Title = "Untitled",
      Subtitle = "Key System",
      Note = "No method of obtaining the key is provided", -- Use this to tell the user how to get a key
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"Hello"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})


local MainTab = Window:CreateTab("Main", 4483362458) -- Title, Image

local Section = MainTab:CreateSection("Welcome! This is a Redux game exploit. It's very OP!")

local PlayerTab = Window:CreateTab("Player", 4483362458) -- Title, Image

local Button = PlayerTab:CreateButton({
    Name = "More faster",
    Callback = function()
        local Players = game:GetService("Players")
        local RunService = game:GetService("RunService")

        local Player = Players.LocalPlayer
        local Character = Player.Character
        if not Character then return end

        local Humanoid = Character:FindFirstChildOfClass("Humanoid")
        local Root = Character:FindFirstChild("HumanoidRootPart")
        if not Humanoid or not Root then return end

        if Character:GetAttribute("FastBoost") then
            Character:SetAttribute("FastBoost", false)
            return
        end

        Character:SetAttribute("FastBoost", true)

        local connection
        connection = RunService.Heartbeat:Connect(function(dt)
            if not Character:GetAttribute("FastBoost") then
                connection:Disconnect()
                return
            end

            if Humanoid.FloorMaterial == Enum.Material.Air then
                return
            end

            local dir = Humanoid.MoveDirection
            if dir.Magnitude > 0 then
                Root.CFrame = Root.CFrame + (dir * 30 * dt)
            end
        end)
    end,
})
