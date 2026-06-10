game:GetService("StarterGui"):SetCore("SendNotification", { 

	Title = "Jacks Script Hub";

	Text = "Say Hello to V1 of the Script Hub";})

game:GetService("StarterGui"):SetCore("SendNotification", { 

	Title = "WARNING!";

	Text = "This is a HEAVY Work in Progress!, and Currently Player Select Fling is broken and does not work it only flings you";})



local player = game.Players.LocalPlayer
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local COLORS = {
	BACKGROUND = Color3.new(0.06, 0.06, 0.1),
	SECONDARY = Color3.new(0.1, 0.1, 0.16),
	ACCENT = Color3.new(0.55, 0.25, 0.85),
	SUCCESS = Color3.new(0.15, 0.85, 0.5),
	DANGER = Color3.new(0.95, 0.25, 0.35),
	TEXT = Color3.new(0.95, 0.95, 0.98),
	TEXT_DARK = Color3.new(0.08, 0.08, 0.12),
	BLUE = Color3.new(0.25, 0.55, 1),
	MUTED = Color3.new(0.5, 0.5, 0.6),
	CARD = Color3.new(0.12, 0.12, 0.18),
	BORDER = Color3.new(0.2, 0.2, 0.3),
}

-- ===================== SCREEN GUI =====================
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ScriptHubGui"
screenGui.Parent = player.PlayerGui
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- ===================== MAIN FRAME =====================
local frame = Instance.new("Frame")
frame.Name = "MainFrame"
frame.Size = UDim2.new(0, 440, 0, 350)
frame.Position = UDim2.new(0.5, -220, 0.5, -175)
frame.BackgroundColor3 = COLORS.BACKGROUND
frame.BorderSizePixel = 0
frame.Parent = screenGui

local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 16)
frameCorner.Parent = frame

local frameGradient = Instance.new("UIGradient")
frameGradient.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.new(0.1, 0.1, 0.16)),
	ColorSequenceKeypoint.new(1, Color3.new(0.06, 0.06, 0.1))
}
frameGradient.Rotation = 45
frameGradient.Parent = frame

local frameStroke = Instance.new("UIStroke")
frameStroke.Color = Color3.new(0.25, 0.2, 0.4)
frameStroke.Thickness = 1.5
frameStroke.Parent = frame

-- ===================== TITLE BAR =====================
local titleLabel = Instance.new("TextLabel")
titleLabel.Name = "TitleLabel"
titleLabel.Size = UDim2.new(1, -60, 0, 45)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.Text = "SCRIPT HUB"
titleLabel.TextColor3 = COLORS.TEXT
titleLabel.BackgroundColor3 = COLORS.SECONDARY
titleLabel.BorderSizePixel = 0
titleLabel.TextScaled = true
titleLabel.Font = Enum.Font.GothamBold
titleLabel.Parent = frame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 16)
titleCorner.Parent = titleLabel

local titleGradient = Instance.new("UIGradient")
titleGradient.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, COLORS.ACCENT),
	ColorSequenceKeypoint.new(1, COLORS.BLUE)
}
titleGradient.Rotation = 90
titleGradient.Parent = titleLabel

-- ===================== CLOSE BUTTON =====================
local closeButton = Instance.new("TextButton")
closeButton.Name = "CloseButton"
closeButton.Size = UDim2.new(0, 40, 0, 40)
closeButton.Position = UDim2.new(1, -45, 0, 2.5)
closeButton.Text = "✕"
closeButton.TextColor3 = COLORS.TEXT
closeButton.BackgroundColor3 = COLORS.DANGER
closeButton.BorderSizePixel = 0
closeButton.TextScaled = true
closeButton.Font = Enum.Font.GothamBold
closeButton.Parent = frame

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 10)
closeCorner.Parent = closeButton

-- ===================== HIDE/TOGGLE BUTTON =====================
local hideButton = Instance.new("TextButton")
hideButton.Name = "HideButton"
hideButton.Size = UDim2.new(0, 50, 0, 50)
hideButton.Position = UDim2.new(0, 10, 0, 10)
hideButton.Text = "HUB"
hideButton.TextColor3 = COLORS.TEXT
hideButton.BackgroundColor3 = COLORS.SECONDARY
hideButton.BorderSizePixel = 0
hideButton.TextScaled = true
hideButton.Font = Enum.Font.Gotham
hideButton.Parent = screenGui

local hideCorner = Instance.new("UICorner")
hideCorner.CornerRadius = UDim.new(0, 25)
hideCorner.Parent = hideButton

local hideStroke = Instance.new("UIStroke")
hideStroke.Color = COLORS.ACCENT
hideStroke.Thickness = 2
hideStroke.Parent = hideButton

-- ===================== TAB BUTTONS =====================
-- Tab sidebar background
local tabSidebar = Instance.new("Frame")
tabSidebar.Name = "TabSidebar"
tabSidebar.Size = UDim2.new(0, 90, 1, -50)
tabSidebar.Position = UDim2.new(0, 0, 0, 45)
tabSidebar.BackgroundColor3 = COLORS.SECONDARY
tabSidebar.BackgroundTransparency = 0.7
tabSidebar.BorderSizePixel = 0
tabSidebar.ZIndex = 1
tabSidebar.Parent = frame

local tabContainer = Instance.new("Frame")
tabContainer.Name = "TabContainer"
tabContainer.Size = UDim2.new(0, 90, 1, -50)
tabContainer.Position = UDim2.new(0, 0, 0, 45)
tabContainer.BackgroundTransparency = 1
tabContainer.ClipsDescendants = true
tabContainer.ZIndex = 2
tabContainer.Parent = frame

local tabContainerPadding = Instance.new("UIPadding")
tabContainerPadding.PaddingTop = UDim.new(0, 6)
tabContainerPadding.PaddingLeft = UDim.new(0, 4)
tabContainerPadding.PaddingRight = UDim.new(0, 4)
tabContainerPadding.Parent = tabContainer

local tabLayout = Instance.new("UIListLayout")
tabLayout.FillDirection = Enum.FillDirection.Vertical
tabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
tabLayout.Padding = UDim.new(0, 4)
tabLayout.Parent = tabContainer

-- Tab separator line
local tabSeparator = Instance.new("Frame")
tabSeparator.Name = "TabSeparator"
tabSeparator.Size = UDim2.new(0, 1, 1, -50)
tabSeparator.Position = UDim2.new(0, 90, 0, 45)
tabSeparator.BackgroundColor3 = COLORS.BORDER
tabSeparator.BorderSizePixel = 0
tabSeparator.ZIndex = 3
tabSeparator.Parent = frame

local teleportTab = Instance.new("TextButton")
teleportTab.Name = "TeleportTab"
teleportTab.Size = UDim2.new(1, 0, 0, 36)
teleportTab.Text = "⚡ Teleport"
teleportTab.TextColor3 = COLORS.TEXT
teleportTab.BackgroundColor3 = COLORS.ACCENT
teleportTab.BorderSizePixel = 0
teleportTab.TextScaled = true
teleportTab.Font = Enum.Font.GothamSemibold
teleportTab.Parent = tabContainer

local teleportTabCorner = Instance.new("UICorner")
teleportTabCorner.CornerRadius = UDim.new(0, 8)
teleportTabCorner.Parent = teleportTab

local flyTab = Instance.new("TextButton")
flyTab.Name = "FlyTab"
flyTab.Size = UDim2.new(1, 0, 0, 36)
flyTab.Text = "✈ Fly"
flyTab.TextColor3 = COLORS.TEXT
flyTab.BackgroundColor3 = COLORS.SECONDARY
flyTab.BorderSizePixel = 0
flyTab.TextScaled = true
flyTab.Font = Enum.Font.GothamSemibold
flyTab.Parent = tabContainer

local flyTabCorner = Instance.new("UICorner")
flyTabCorner.CornerRadius = UDim.new(0, 8)
flyTabCorner.Parent = flyTab

local espTab = Instance.new("TextButton")
espTab.Name = "EspTab"
espTab.Size = UDim2.new(1, 0, 0, 36)
espTab.Text = "👁 ESP"
espTab.TextColor3 = COLORS.TEXT
espTab.BackgroundColor3 = COLORS.SECONDARY
espTab.BorderSizePixel = 0
espTab.TextScaled = true
espTab.Font = Enum.Font.GothamSemibold
espTab.Parent = tabContainer

local espTabCorner = Instance.new("UICorner")
espTabCorner.CornerRadius = UDim.new(0, 8)
espTabCorner.Parent = espTab

local touchFlingTab = Instance.new("TextButton")
touchFlingTab.Name = "TouchFlingTab"
touchFlingTab.Size = UDim2.new(1, 0, 0, 36)
touchFlingTab.Text = "💫 TouchFling"
touchFlingTab.TextColor3 = COLORS.TEXT
touchFlingTab.BackgroundColor3 = COLORS.SECONDARY
touchFlingTab.BorderSizePixel = 0
touchFlingTab.TextScaled = true
touchFlingTab.Font = Enum.Font.GothamSemibold
touchFlingTab.Parent = tabContainer

local touchFlingTabCorner = Instance.new("UICorner")
touchFlingTabCorner.CornerRadius = UDim.new(0, 8)
touchFlingTabCorner.Parent = touchFlingTab

local noclipTab = Instance.new("TextButton")
noclipTab.Name = "NoclipTab"
noclipTab.Size = UDim2.new(1, 0, 0, 36)
noclipTab.Text = "🚶 Noclip"
noclipTab.TextColor3 = COLORS.TEXT
noclipTab.BackgroundColor3 = COLORS.SECONDARY
noclipTab.BorderSizePixel = 0
noclipTab.TextScaled = true
noclipTab.Font = Enum.Font.GothamSemibold
noclipTab.Parent = tabContainer

local noclipTabCorner = Instance.new("UICorner")
noclipTabCorner.CornerRadius = UDim.new(0, 8)
noclipTabCorner.Parent = noclipTab

-- ===================== TELEPORT PAGE =====================
local teleportPage = Instance.new("Frame")
teleportPage.Name = "TeleportPage"
teleportPage.Size = UDim2.new(1, -100, 1, -60)
teleportPage.Position = UDim2.new(0, 95, 0, 50)
teleportPage.BackgroundTransparency = 1
teleportPage.Visible = true
teleportPage.Parent = frame

local dropdownButton = Instance.new("TextButton")
dropdownButton.Name = "DropdownButton"
dropdownButton.Size = UDim2.new(1, 0, 0, 35)
dropdownButton.Text = "📋 Player LeaderBoard"
dropdownButton.TextColor3 = COLORS.TEXT
dropdownButton.BackgroundColor3 = COLORS.CARD
dropdownButton.BorderSizePixel = 0
dropdownButton.TextScaled = true
dropdownButton.Font = Enum.Font.Gotham
dropdownButton.Parent = teleportPage

local dropdownCorner = Instance.new("UICorner")
dropdownCorner.CornerRadius = UDim.new(0, 8)
dropdownCorner.Parent = dropdownButton

local tpButtonContainer = Instance.new("Frame")
tpButtonContainer.Name = "ButtonContainer"
tpButtonContainer.Size = UDim2.new(1, 0, 0, 40)
tpButtonContainer.Position = UDim2.new(0, 0, 1, -40)
tpButtonContainer.BackgroundTransparency = 1
tpButtonContainer.Parent = teleportPage

local tpButtonLayout = Instance.new("UIListLayout")
tpButtonLayout.FillDirection = Enum.FillDirection.Horizontal
tpButtonLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
tpButtonLayout.Padding = UDim.new(0, 10)
tpButtonLayout.Parent = tpButtonContainer

local followButton = Instance.new("TextButton")
followButton.Name = "FollowButton"
followButton.Size = UDim2.new(0, 145, 0, 40)
followButton.Text = "🔗 Weld"
followButton.TextColor3 = COLORS.TEXT
followButton.BackgroundColor3 = COLORS.SUCCESS
followButton.BorderSizePixel = 0
followButton.TextScaled = true
followButton.Font = Enum.Font.GothamSemibold
followButton.Parent = tpButtonContainer

local followCorner = Instance.new("UICorner")
followCorner.CornerRadius = UDim.new(0, 8)
followCorner.Parent = followButton

local teleportButton = Instance.new("TextButton")
teleportButton.Name = "TeleportButton"
teleportButton.Size = UDim2.new(0, 145, 0, 40)
teleportButton.Text = "⚡ Teleport"
teleportButton.TextColor3 = COLORS.TEXT
teleportButton.BackgroundColor3 = COLORS.ACCENT
teleportButton.BorderSizePixel = 0
teleportButton.TextScaled = true
teleportButton.Font = Enum.Font.GothamSemibold
teleportButton.Parent = tpButtonContainer

local teleportCorner = Instance.new("UICorner")
teleportCorner.CornerRadius = UDim.new(0, 8)
teleportCorner.Parent = teleportButton

-- ===================== FLY PAGE =====================
local flyPage = Instance.new("Frame")
flyPage.Name = "FlyPage"
flyPage.Size = UDim2.new(1, -100, 1, -60)
flyPage.Position = UDim2.new(0, 95, 0, 50)
flyPage.BackgroundTransparency = 1
flyPage.Visible = false
flyPage.Parent = frame

local flyToggle = Instance.new("TextButton")
flyToggle.Name = "FlyToggle"
flyToggle.Size = UDim2.new(1, 0, 0, 40)
flyToggle.Text = "✈ Fly: OFF"
flyToggle.TextColor3 = COLORS.TEXT
flyToggle.BackgroundColor3 = COLORS.DANGER
flyToggle.BorderSizePixel = 0
flyToggle.TextScaled = true
flyToggle.Font = Enum.Font.GothamSemibold
flyToggle.Parent = flyPage

local flyToggleCorner = Instance.new("UICorner")
flyToggleCorner.CornerRadius = UDim.new(0, 10)
flyToggleCorner.Parent = flyToggle

local speedLabel = Instance.new("TextLabel")
speedLabel.Name = "SpeedLabel"
speedLabel.Size = UDim2.new(1, 0, 0, 25)
speedLabel.Position = UDim2.new(0, 0, 0, 50)
speedLabel.Text = "Speed: 50"
speedLabel.TextColor3 = COLORS.TEXT
speedLabel.BackgroundTransparency = 1
speedLabel.TextScaled = true
speedLabel.Font = Enum.Font.Gotham
speedLabel.Parent = flyPage

local speedSliderBg = Instance.new("Frame")
speedSliderBg.Name = "SpeedSliderBg"
speedSliderBg.Size = UDim2.new(1, 0, 0, 20)
speedSliderBg.Position = UDim2.new(0, 0, 0, 80)
speedSliderBg.BackgroundColor3 = COLORS.SECONDARY
speedSliderBg.BorderSizePixel = 0
speedSliderBg.Parent = flyPage

local speedSliderBgCorner = Instance.new("UICorner")
speedSliderBgCorner.CornerRadius = UDim.new(0, 12)
speedSliderBgCorner.Parent = speedSliderBg

local speedSliderFill = Instance.new("Frame")
speedSliderFill.Name = "SpeedSliderFill"
speedSliderFill.Size = UDim2.new(0.5, 0, 1, 0)
speedSliderFill.BackgroundColor3 = COLORS.BLUE
speedSliderFill.BorderSizePixel = 0
speedSliderFill.Parent = speedSliderBg

local speedSliderFillCorner = Instance.new("UICorner")
speedSliderFillCorner.CornerRadius = UDim.new(0, 12)
speedSliderFillCorner.Parent = speedSliderFill

local speedSliderKnob = Instance.new("TextButton")
speedSliderKnob.Name = "SpeedSliderKnob"
speedSliderKnob.Size = UDim2.new(0, 20, 0, 24)
speedSliderKnob.Position = UDim2.new(0.5, -10, 0, -2)
speedSliderKnob.Text = ""
speedSliderKnob.BackgroundColor3 = COLORS.TEXT
speedSliderKnob.BorderSizePixel = 0
speedSliderKnob.Parent = speedSliderBg

local speedSliderKnobCorner = Instance.new("UICorner")
speedSliderKnobCorner.CornerRadius = UDim.new(1, 0)
speedSliderKnobCorner.Parent = speedSliderKnob

local flyInfoLabel = Instance.new("TextLabel")
flyInfoLabel.Name = "FlyInfoLabel"
flyInfoLabel.Size = UDim2.new(1, 0, 0, 40)
flyInfoLabel.Position = UDim2.new(0, 0, 0, 110)
flyInfoLabel.Text = "WASD to move | Space up | Shift down"
flyInfoLabel.TextColor3 = COLORS.MUTED
flyInfoLabel.BackgroundTransparency = 1
flyInfoLabel.TextScaled = true
flyInfoLabel.Font = Enum.Font.Gotham
flyInfoLabel.TextWrapped = true
flyInfoLabel.Parent = flyPage

-- ===================== PLAYER LIST (DROPDOWN) =====================
local playerList = Instance.new("ScrollingFrame")
playerList.Name = "PlayerList"
playerList.Size = UDim2.new(0, 300, 0, 0)
playerList.Position = UDim2.new(0.5, 170, 0.5, -100)
playerList.BackgroundColor3 = COLORS.BACKGROUND
playerList.BorderSizePixel = 0
playerList.Visible = false
playerList.CanvasSize = UDim2.new(0, 0, 0, 0)
playerList.ScrollBarThickness = 8
playerList.ScrollBarImageColor3 = COLORS.ACCENT
playerList.Parent = screenGui

local listCorner = Instance.new("UICorner")
listCorner.CornerRadius = UDim.new(0, 12)
listCorner.Parent = playerList

local listStroke = Instance.new("UIStroke")
listStroke.Color = COLORS.BORDER
listStroke.Thickness = 1
listStroke.Parent = playerList

local playerListLayout = Instance.new("UIListLayout")
playerListLayout.SortOrder = Enum.SortOrder.Name
playerListLayout.Padding = UDim.new(0, 2)
playerListLayout.Parent = playerList

-- ===================== CONFIRM DIALOG =====================
local confirmDialog = Instance.new("Frame")
confirmDialog.Name = "ConfirmDialog"
confirmDialog.Size = UDim2.new(0, 300, 0, 150)
confirmDialog.Position = UDim2.new(0.5, -150, 0.5, -75)
confirmDialog.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
confirmDialog.BorderSizePixel = 0
confirmDialog.Visible = false
confirmDialog.Parent = screenGui

local confirmCorner = Instance.new("UICorner")
confirmCorner.CornerRadius = UDim.new(0, 16)
confirmCorner.Parent = confirmDialog

local confirmGradient = Instance.new("UIGradient")
confirmGradient.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.new(0.1, 0.1, 0.16)),
	ColorSequenceKeypoint.new(1, Color3.new(0.06, 0.06, 0.1))
}
confirmGradient.Rotation = 45
confirmGradient.Parent = confirmDialog

local confirmStroke = Instance.new("UIStroke")
confirmStroke.Color = Color3.new(0.5, 0.2, 0.6)
confirmStroke.Thickness = 2
confirmStroke.Parent = confirmDialog

local confirmTitle = Instance.new("TextLabel")
confirmTitle.Name = "ConfirmTitle"
confirmTitle.Size = UDim2.new(1, -20, 0, 40)
confirmTitle.Position = UDim2.new(0, 10, 0, 10)
confirmTitle.Text = "⚠️ Confirmation"
confirmTitle.TextColor3 = COLORS.ACCENT
confirmTitle.BackgroundTransparency = 1
confirmTitle.TextScaled = true
confirmTitle.Font = Enum.Font.GothamBold
confirmTitle.Parent = confirmDialog

local confirmQuestion = Instance.new("TextLabel")
confirmQuestion.Name = "ConfirmQuestion"
confirmQuestion.Size = UDim2.new(1, -20, 0, 40)
confirmQuestion.Position = UDim2.new(0, 10, 0, 50)
confirmQuestion.Text = "Close Script Hub?"
confirmQuestion.TextColor3 = COLORS.TEXT
confirmQuestion.BackgroundTransparency = 1
confirmQuestion.TextScaled = true
confirmQuestion.Font = Enum.Font.Gotham
confirmQuestion.Parent = confirmDialog

local confirmButtonContainer = Instance.new("Frame")
confirmButtonContainer.Name = "ConfirmButtonContainer"
confirmButtonContainer.Size = UDim2.new(1, -20, 0, 40)
confirmButtonContainer.Position = UDim2.new(0, 10, 1, -50)
confirmButtonContainer.BackgroundTransparency = 1
confirmButtonContainer.Parent = confirmDialog

local confirmButtonLayout = Instance.new("UIListLayout")
confirmButtonLayout.FillDirection = Enum.FillDirection.Horizontal
confirmButtonLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
confirmButtonLayout.Padding = UDim.new(0, 20)
confirmButtonLayout.Parent = confirmButtonContainer

local yesButton = Instance.new("TextButton")
yesButton.Name = "YesButton"
yesButton.Size = UDim2.new(0, 100, 0, 40)
yesButton.Text = "V Yes"
yesButton.TextColor3 = COLORS.TEXT
yesButton.BackgroundColor3 = COLORS.DANGER
yesButton.BorderSizePixel = 0
yesButton.TextScaled = true
yesButton.Font = Enum.Font.GothamSemibold
yesButton.Parent = confirmButtonContainer

local yesCorner = Instance.new("UICorner")
yesCorner.CornerRadius = UDim.new(0, 8)
yesCorner.Parent = yesButton

local noButton = Instance.new("TextButton")
noButton.Name = "NoButton"
noButton.Size = UDim2.new(0, 100, 0, 40)
noButton.Text = "✕ No"
noButton.TextColor3 = COLORS.TEXT
noButton.BackgroundColor3 = COLORS.SECONDARY
noButton.BorderSizePixel = 0
noButton.TextScaled = true
noButton.Font = Enum.Font.GothamSemibold
noButton.Parent = confirmButtonContainer

local noCorner = Instance.new("UICorner")
noCorner.CornerRadius = UDim.new(0, 8)
noCorner.Parent = noButton

-- ===================== STATE VARIABLES =====================
local following = false
local targetPlayer = nil
local followConnection = nil
local deathConnection = nil

local flying = false
local flySpeed = 50
local flyBodyVelocity = nil
local flyBodyGyro = nil
local flyConnection = nil

local espEnabled = false
local espConnection = nil
local Murder = nil
local Sheriff = nil
local Hero = nil

local touchFlingEnabled = false
local touchFlingPower = 500
local touchFlingConnections = {}
local touchFlingDebounce = {}

local noclipEnabled = false
local noclipConnection = nil

local flingTarget = nil
local flingPower = 500
local multiflingOpen = false

-- ===================== HELPER FUNCTIONS =====================
local function animateButton(button, hoverColor, originalColor)
	local hoverTween = TweenService:Create(button,
		TweenInfo.new(0.2, Enum.EasingStyle.Quad),
		{BackgroundColor3 = hoverColor}
	)
	local leaveTween = TweenService:Create(button,
		TweenInfo.new(0.2, Enum.EasingStyle.Quad),
		{BackgroundColor3 = originalColor}
	)
	button.MouseEnter:Connect(function() hoverTween:Play() end)
	button.MouseLeave:Connect(function() leaveTween:Play() end)
end

animateButton(closeButton, Color3.new(1, 0.3, 0.4), COLORS.DANGER)
animateButton(followButton, Color3.new(0.25, 0.95, 0.6), COLORS.SUCCESS)
animateButton(teleportButton, Color3.new(0.65, 0.35, 0.95), COLORS.ACCENT)
animateButton(dropdownButton, Color3.new(0.18, 0.18, 0.24), COLORS.CARD)
animateButton(yesButton, Color3.new(1, 0.3, 0.4), COLORS.DANGER)
animateButton(noButton, Color3.new(0.16, 0.16, 0.22), COLORS.SECONDARY)
animateButton(flyToggle, Color3.new(0.25, 0.95, 0.6), COLORS.SUCCESS)
animateButton(teleportTab, Color3.new(0.65, 0.35, 0.95), COLORS.ACCENT)
animateButton(flyTab, Color3.new(0.35, 0.65, 1), COLORS.BLUE)
animateButton(espTab, Color3.new(0.65, 0.35, 0.95), COLORS.ACCENT)
animateButton(touchFlingTab, Color3.new(0.65, 0.35, 0.95), COLORS.ACCENT)
animateButton(noclipTab, Color3.new(0.35, 0.65, 1), COLORS.BLUE)

-- ===================== ESP PAGE =====================
local espPage = Instance.new("Frame")
espPage.Name = "EspPage"
espPage.Size = UDim2.new(1, -100, 1, -60)
espPage.Position = UDim2.new(0, 95, 0, 50)
espPage.BackgroundTransparency = 1
espPage.Visible = false
espPage.Parent = frame

local espToggle = Instance.new("TextButton")
espToggle.Name = "EspToggle"
espToggle.Size = UDim2.new(1, 0, 0, 40)
espToggle.Text = "👁 MM2 ESP: OFF"
espToggle.TextColor3 = COLORS.TEXT
espToggle.BackgroundColor3 = COLORS.DANGER
espToggle.BorderSizePixel = 0
espToggle.TextScaled = true
espToggle.Font = Enum.Font.GothamSemibold
espToggle.Parent = espPage

local espToggleCorner = Instance.new("UICorner")
espToggleCorner.CornerRadius = UDim.new(0, 10)
espToggleCorner.Parent = espToggle

local espLegend = Instance.new("Frame")
espLegend.Name = "EspLegend"
espLegend.Size = UDim2.new(1, 0, 0, 110)
espLegend.Position = UDim2.new(0, 0, 0, 50)
espLegend.BackgroundTransparency = 1
espLegend.Parent = espPage

local espLegendLayout = Instance.new("UIListLayout")
espLegendLayout.SortOrder = Enum.SortOrder.LayoutOrder
espLegendLayout.Padding = UDim.new(0, 6)
espLegendLayout.Parent = espLegend

local function createLegendItem(color, text, order)
	local container = Instance.new("Frame")
	container.Size = UDim2.new(1, 0, 0, 22)
	container.BackgroundTransparency = 1
	container.LayoutOrder = order
	container.Parent = espLegend

	local dot = Instance.new("Frame")
	dot.Size = UDim2.new(0, 16, 0, 16)
	dot.Position = UDim2.new(0, 5, 0.5, -8)
	dot.BackgroundColor3 = color
	dot.BorderSizePixel = 0
	dot.Parent = container

	local dotCorner = Instance.new("UICorner")
	dotCorner.CornerRadius = UDim.new(1, 0)
	dotCorner.Parent = dot

	local dotStroke = Instance.new("UIStroke")
	dotStroke.Color = COLORS.BORDER
	dotStroke.Thickness = 0.5
	dotStroke.Parent = dot

	local label = Instance.new("TextLabel")
	label.Size = UDim2.new(1, -30, 1, 0)
	label.Position = UDim2.new(0, 28, 0, 0)
	label.Text = text
	label.TextColor3 = COLORS.TEXT
	label.BackgroundTransparency = 1
	label.TextScaled = true
	label.Font = Enum.Font.Gotham
	label.TextXAlignment = Enum.TextXAlignment.Left
	label.Parent = container
end

createLegendItem(Color3.fromRGB(225, 0, 0), "Murderer", 1)
createLegendItem(Color3.fromRGB(0, 0, 225), "Sheriff", 2)
createLegendItem(Color3.fromRGB(255, 250, 0), "Hero (if Sheriff dead)", 3)
createLegendItem(Color3.fromRGB(0, 225, 0), "Innocent", 4)

-- ===================== FLING PAGE =====================
local flingPage = Instance.new("Frame")
flingPage.Name = "FlingPage"
flingPage.Size = UDim2.new(1, -100, 1, -60)
flingPage.Position = UDim2.new(0, 95, 0, 50)
flingPage.BackgroundTransparency = 1
flingPage.Visible = false
flingPage.Parent = frame

local flingPowerLabel = Instance.new("TextLabel")
flingPowerLabel.Name = "FlingPowerLabel"
flingPowerLabel.Size = UDim2.new(1, 0, 0, 25)
flingPowerLabel.Position = UDim2.new(0, 0, 0, 0)
flingPowerLabel.Text = "Power: 500"
flingPowerLabel.TextColor3 = COLORS.TEXT
flingPowerLabel.BackgroundTransparency = 1
flingPowerLabel.TextScaled = true
flingPowerLabel.Font = Enum.Font.Gotham
flingPowerLabel.Parent = flingPage

local flingPowerSliderBg = Instance.new("Frame")
flingPowerSliderBg.Name = "FlingPowerSliderBg"
flingPowerSliderBg.Size = UDim2.new(1, 0, 0, 20)
flingPowerSliderBg.Position = UDim2.new(0, 0, 0, 30)
flingPowerSliderBg.BackgroundColor3 = COLORS.SECONDARY
flingPowerSliderBg.BorderSizePixel = 0
flingPowerSliderBg.Parent = flingPage

local flingPowerSliderBgCorner = Instance.new("UICorner")
flingPowerSliderBgCorner.CornerRadius = UDim.new(0, 12)
flingPowerSliderBgCorner.Parent = flingPowerSliderBg

local flingPowerSliderFill = Instance.new("Frame")
flingPowerSliderFill.Name = "FlingPowerSliderFill"
flingPowerSliderFill.Size = UDim2.new(0.5, 0, 1, 0)
flingPowerSliderFill.BackgroundColor3 = COLORS.ACCENT
flingPowerSliderFill.BorderSizePixel = 0
flingPowerSliderFill.Parent = flingPowerSliderBg

local flingPowerSliderFillCorner = Instance.new("UICorner")
flingPowerSliderFillCorner.CornerRadius = UDim.new(0, 12)
flingPowerSliderFillCorner.Parent = flingPowerSliderFill

local flingPowerSliderKnob = Instance.new("TextButton")
flingPowerSliderKnob.Name = "FlingPowerSliderKnob"
flingPowerSliderKnob.Size = UDim2.new(0, 20, 0, 24)
flingPowerSliderKnob.Position = UDim2.new(0.5, -10, 0, -2)
flingPowerSliderKnob.Text = ""
flingPowerSliderKnob.BackgroundColor3 = COLORS.TEXT
flingPowerSliderKnob.BorderSizePixel = 0
flingPowerSliderKnob.Parent = flingPowerSliderBg

local flingPowerSliderKnobCorner = Instance.new("UICorner")
flingPowerSliderKnobCorner.CornerRadius = UDim.new(1, 0)
flingPowerSliderKnobCorner.Parent = flingPowerSliderKnob

local flingTargetDropdown = Instance.new("TextButton")
flingTargetDropdown.Name = "FlingTargetDropdown"
flingTargetDropdown.Size = UDim2.new(1, 0, 0, 35)
flingTargetDropdown.Position = UDim2.new(0, 0, 0, 60)
flingTargetDropdown.Text = "📋 Select Target"
flingTargetDropdown.TextColor3 = COLORS.TEXT
flingTargetDropdown.BackgroundColor3 = COLORS.CARD
flingTargetDropdown.BorderSizePixel = 0
flingTargetDropdown.TextScaled = true
flingTargetDropdown.Font = Enum.Font.Gotham
flingTargetDropdown.Parent = flingPage

local flingTargetDropdownCorner = Instance.new("UICorner")
flingTargetDropdownCorner.CornerRadius = UDim.new(0, 8)
flingTargetDropdownCorner.Parent = flingTargetDropdown

local flingActionButton = Instance.new("TextButton")
flingActionButton.Name = "FlingActionButton"
flingActionButton.Size = UDim2.new(1, 0, 0, 35)
flingActionButton.Position = UDim2.new(0, 0, 0, 105)
flingActionButton.Text = "💨 Fling Target"
flingActionButton.TextColor3 = COLORS.TEXT
flingActionButton.BackgroundColor3 = COLORS.ACCENT
flingActionButton.BorderSizePixel = 0
flingActionButton.TextScaled = true
flingActionButton.Font = Enum.Font.GothamSemibold
flingActionButton.Parent = flingPage

local flingActionButtonCorner = Instance.new("UICorner")
flingActionButtonCorner.CornerRadius = UDim.new(0, 8)
flingActionButtonCorner.Parent = flingActionButton

local multiflingButton = Instance.new("TextButton")
multiflingButton.Name = "MultiflingButton"
multiflingButton.Size = UDim2.new(1, 0, 0, 35)
multiflingButton.Position = UDim2.new(0, 0, 0, 135)
multiflingButton.Text = "🌀 Multifling Panel"
multiflingButton.TextColor3 = COLORS.TEXT
multiflingButton.BackgroundColor3 = COLORS.BLUE
multiflingButton.BorderSizePixel = 0
multiflingButton.TextScaled = true
multiflingButton.Font = Enum.Font.GothamSemibold
multiflingButton.Parent = flingPage

local multiflingButtonCorner = Instance.new("UICorner")
multiflingButtonCorner.CornerRadius = UDim.new(0, 8)
multiflingButtonCorner.Parent = multiflingButton

-- ===================== MULTIFLING SEPARATE FRAME =====================
local multiflingFrame = Instance.new("Frame")
multiflingFrame.Name = "MultiflingFrame"
multiflingFrame.Size = UDim2.new(0, 300, 0, 400)
multiflingFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
multiflingFrame.BackgroundColor3 = COLORS.BACKGROUND
multiflingFrame.BorderSizePixel = 0
multiflingFrame.Visible = false
multiflingFrame.Parent = screenGui

local multiflingFrameCorner = Instance.new("UICorner")
multiflingFrameCorner.CornerRadius = UDim.new(0, 16)
multiflingFrameCorner.Parent = multiflingFrame

local multiflingFrameGradient = Instance.new("UIGradient")
multiflingFrameGradient.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.new(0.1, 0.1, 0.16)),
	ColorSequenceKeypoint.new(1, Color3.new(0.06, 0.06, 0.1))
}
multiflingFrameGradient.Rotation = 45
multiflingFrameGradient.Parent = multiflingFrame

local multiflingFrameStroke = Instance.new("UIStroke")
multiflingFrameStroke.Color = Color3.new(0.25, 0.2, 0.4)
multiflingFrameStroke.Thickness = 1.5
multiflingFrameStroke.Parent = multiflingFrame

local multiflingTitle = Instance.new("TextLabel")
multiflingTitle.Name = "MultiflingTitle"
multiflingTitle.Size = UDim2.new(1, -50, 0, 40)
multiflingTitle.Position = UDim2.new(0, 0, 0, 0)
multiflingTitle.Text = "🌀 MULTIFLING"
multiflingTitle.TextColor3 = COLORS.TEXT
multiflingTitle.BackgroundColor3 = COLORS.SECONDARY
multiflingTitle.BorderSizePixel = 0
multiflingTitle.TextScaled = true
multiflingTitle.Font = Enum.Font.GothamBold
multiflingTitle.Parent = multiflingFrame

local multiflingTitleCorner = Instance.new("UICorner")
multiflingTitleCorner.CornerRadius = UDim.new(0, 16)
multiflingTitleCorner.Parent = multiflingTitle

local multiflingTitleGradient = Instance.new("UIGradient")
multiflingTitleGradient.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, COLORS.ACCENT),
	ColorSequenceKeypoint.new(1, COLORS.BLUE)
}
multiflingTitleGradient.Rotation = 90
multiflingTitleGradient.Parent = multiflingTitle

local multiflingCloseBtn = Instance.new("TextButton")
multiflingCloseBtn.Name = "CloseButton"
multiflingCloseBtn.Size = UDim2.new(0, 40, 0, 40)
multiflingCloseBtn.Position = UDim2.new(1, -45, 0, 0)
multiflingCloseBtn.Text = "✕"
multiflingCloseBtn.TextColor3 = COLORS.TEXT
multiflingCloseBtn.BackgroundColor3 = COLORS.DANGER
multiflingCloseBtn.BorderSizePixel = 0
multiflingCloseBtn.TextScaled = true
multiflingCloseBtn.Font = Enum.Font.GothamBold
multiflingCloseBtn.Parent = multiflingFrame

local multiflingCloseBtnCorner = Instance.new("UICorner")
multiflingCloseBtnCorner.CornerRadius = UDim.new(0, 10)
multiflingCloseBtnCorner.Parent = multiflingCloseBtn

local multiflingPowerLabel = Instance.new("TextLabel")
multiflingPowerLabel.Name = "PowerLabel"
multiflingPowerLabel.Size = UDim2.new(1, -20, 0, 20)
multiflingPowerLabel.Position = UDim2.new(0, 10, 0, 50)
multiflingPowerLabel.Text = "Fling Power: 500"
multiflingPowerLabel.TextColor3 = COLORS.TEXT
multiflingPowerLabel.BackgroundTransparency = 1
multiflingPowerLabel.TextScaled = true
multiflingPowerLabel.Font = Enum.Font.Gotham
multiflingPowerLabel.Parent = multiflingFrame

local multiflingPowerSliderBg = Instance.new("Frame")
multiflingPowerSliderBg.Name = "PowerSliderBg"
multiflingPowerSliderBg.Size = UDim2.new(1, -20, 0, 16)
multiflingPowerSliderBg.Position = UDim2.new(0, 10, 0, 75)
multiflingPowerSliderBg.BackgroundColor3 = COLORS.SECONDARY
multiflingPowerSliderBg.BorderSizePixel = 0
multiflingPowerSliderBg.Parent = multiflingFrame

local multiflingPowerSliderBgCorner = Instance.new("UICorner")
multiflingPowerSliderBgCorner.CornerRadius = UDim.new(0, 10)
multiflingPowerSliderBgCorner.Parent = multiflingPowerSliderBg

local multiflingPowerSliderFill = Instance.new("Frame")
multiflingPowerSliderFill.Name = "PowerSliderFill"
multiflingPowerSliderFill.Size = UDim2.new(0.5, 0, 1, 0)
multiflingPowerSliderFill.BackgroundColor3 = COLORS.ACCENT
multiflingPowerSliderFill.BorderSizePixel = 0
multiflingPowerSliderFill.Parent = multiflingPowerSliderBg

local multiflingPowerSliderFillCorner = Instance.new("UICorner")
multiflingPowerSliderFillCorner.CornerRadius = UDim.new(0, 10)
multiflingPowerSliderFillCorner.Parent = multiflingPowerSliderFill

local multiflingPowerSliderKnob = Instance.new("TextButton")
multiflingPowerSliderKnob.Name = "PowerSliderKnob"
multiflingPowerSliderKnob.Size = UDim2.new(0, 18, 0, 20)
multiflingPowerSliderKnob.Position = UDim2.new(0.5, -9, 0, -2)
multiflingPowerSliderKnob.Text = ""
multiflingPowerSliderKnob.BackgroundColor3 = COLORS.TEXT
multiflingPowerSliderKnob.BorderSizePixel = 0
multiflingPowerSliderKnob.Parent = multiflingPowerSliderBg

local multiflingPowerSliderKnobCorner = Instance.new("UICorner")
multiflingPowerSliderKnobCorner.CornerRadius = UDim.new(1, 0)
multiflingPowerSliderKnobCorner.Parent = multiflingPowerSliderKnob

local flingAllButton = Instance.new("TextButton")
flingAllButton.Name = "FlingAllButton"
flingAllButton.Size = UDim2.new(1, -20, 0, 30)
flingAllButton.Position = UDim2.new(0, 95, 0, 50)
flingAllButton.Text = "💥 Fling All Players"
flingAllButton.TextColor3 = COLORS.TEXT
flingAllButton.BackgroundColor3 = COLORS.DANGER
flingAllButton.BorderSizePixel = 0
flingAllButton.TextScaled = true
flingAllButton.Font = Enum.Font.GothamSemibold
flingAllButton.Parent = multiflingFrame

local flingAllButtonCorner = Instance.new("UICorner")
flingAllButtonCorner.CornerRadius = UDim.new(0, 8)
flingAllButtonCorner.Parent = flingAllButton

local multiflingPlayerList = Instance.new("ScrollingFrame")
multiflingPlayerList.Name = "PlayerList"
multiflingPlayerList.Size = UDim2.new(1, -20, 0, 250)
multiflingPlayerList.Position = UDim2.new(0, 10, 0, 140)
multiflingPlayerList.BackgroundColor3 = COLORS.CARD
multiflingPlayerList.BorderSizePixel = 0
multiflingPlayerList.CanvasSize = UDim2.new(0, 0, 0, 0)
multiflingPlayerList.ScrollBarThickness = 6
multiflingPlayerList.ScrollBarImageColor3 = COLORS.ACCENT
multiflingPlayerList.Parent = multiflingFrame

local multiflingPlayerListCorner = Instance.new("UICorner")
multiflingPlayerListCorner.CornerRadius = UDim.new(0, 8)
multiflingPlayerListCorner.Parent = multiflingPlayerList

local multiflingPlayerListLayout = Instance.new("UIListLayout")
multiflingPlayerListLayout.SortOrder = Enum.SortOrder.Name
multiflingPlayerListLayout.Padding = UDim.new(0, 4)
multiflingPlayerListLayout.Parent = multiflingPlayerList

local multiflingPlayerListPadding = Instance.new("UIPadding")
multiflingPlayerListPadding.PaddingTop = UDim.new(0, 4)
multiflingPlayerListPadding.PaddingBottom = UDim.new(0, 4)
multiflingPlayerListPadding.PaddingLeft = UDim.new(0, 4)
multiflingPlayerListPadding.PaddingRight = UDim.new(0, 4)
multiflingPlayerListPadding.Parent = multiflingPlayerList

-- ===================== TOUCHFLING PAGE =====================
local touchFlingPage = Instance.new("Frame")
touchFlingPage.Name = "TouchFlingPage"
touchFlingPage.Size = UDim2.new(1, -100, 1, -60)
touchFlingPage.Position = UDim2.new(0, 95, 0, 50)
touchFlingPage.BackgroundTransparency = 1
touchFlingPage.Visible = false
touchFlingPage.Parent = frame

local touchFlingToggle = Instance.new("TextButton")
touchFlingToggle.Name = "TouchFlingToggle"
touchFlingToggle.Size = UDim2.new(1, 0, 0, 40)
touchFlingToggle.Text = "💫 TouchFling: OFF"
touchFlingToggle.TextColor3 = COLORS.TEXT
touchFlingToggle.BackgroundColor3 = COLORS.DANGER
touchFlingToggle.BorderSizePixel = 0
touchFlingToggle.TextScaled = true
touchFlingToggle.Font = Enum.Font.GothamSemibold
touchFlingToggle.Parent = touchFlingPage

local touchFlingToggleCorner = Instance.new("UICorner")
touchFlingToggleCorner.CornerRadius = UDim.new(0, 10)
touchFlingToggleCorner.Parent = touchFlingToggle

local touchFlingPowerLabel = Instance.new("TextLabel")
touchFlingPowerLabel.Name = "TouchFlingPowerLabel"
touchFlingPowerLabel.Size = UDim2.new(1, 0, 0, 25)
touchFlingPowerLabel.Position = UDim2.new(0, 0, 0, 50)
touchFlingPowerLabel.Text = "Power: 500"
touchFlingPowerLabel.TextColor3 = COLORS.TEXT
touchFlingPowerLabel.BackgroundTransparency = 1
touchFlingPowerLabel.TextScaled = true
touchFlingPowerLabel.Font = Enum.Font.Gotham
touchFlingPowerLabel.Parent = touchFlingPage

local touchFlingPowerSliderBg = Instance.new("Frame")
touchFlingPowerSliderBg.Name = "TouchFlingPowerSliderBg"
touchFlingPowerSliderBg.Size = UDim2.new(1, 0, 0, 20)
touchFlingPowerSliderBg.Position = UDim2.new(0, 0, 0, 80)
touchFlingPowerSliderBg.BackgroundColor3 = COLORS.SECONDARY
touchFlingPowerSliderBg.BorderSizePixel = 0
touchFlingPowerSliderBg.Parent = touchFlingPage

local touchFlingPowerSliderBgCorner = Instance.new("UICorner")
touchFlingPowerSliderBgCorner.CornerRadius = UDim.new(0, 12)
touchFlingPowerSliderBgCorner.Parent = touchFlingPowerSliderBg

local touchFlingPowerSliderFill = Instance.new("Frame")
touchFlingPowerSliderFill.Name = "TouchFlingPowerSliderFill"
touchFlingPowerSliderFill.Size = UDim2.new(0.5, 0, 1, 0)
touchFlingPowerSliderFill.BackgroundColor3 = COLORS.ACCENT
touchFlingPowerSliderFill.BorderSizePixel = 0
touchFlingPowerSliderFill.Parent = touchFlingPowerSliderBg

local touchFlingPowerSliderFillCorner = Instance.new("UICorner")
touchFlingPowerSliderFillCorner.CornerRadius = UDim.new(0, 12)
touchFlingPowerSliderFillCorner.Parent = touchFlingPowerSliderFill

local touchFlingPowerSliderKnob = Instance.new("TextButton")
touchFlingPowerSliderKnob.Name = "TouchFlingPowerSliderKnob"
touchFlingPowerSliderKnob.Size = UDim2.new(0, 20, 0, 24)
touchFlingPowerSliderKnob.Position = UDim2.new(0.5, -10, 0, -2)
touchFlingPowerSliderKnob.Text = ""
touchFlingPowerSliderKnob.BackgroundColor3 = COLORS.TEXT
touchFlingPowerSliderKnob.BorderSizePixel = 0
touchFlingPowerSliderKnob.Parent = touchFlingPowerSliderBg

local touchFlingPowerSliderKnobCorner = Instance.new("UICorner")
touchFlingPowerSliderKnobCorner.CornerRadius = UDim.new(1, 0)
touchFlingPowerSliderKnobCorner.Parent = touchFlingPowerSliderKnob

local touchFlingInfoLabel = Instance.new("TextLabel")
touchFlingInfoLabel.Name = "TouchFlingInfoLabel"
touchFlingInfoLabel.Size = UDim2.new(1, 0, 0, 40)
touchFlingInfoLabel.Position = UDim2.new(0, 0, 0, 110)
touchFlingInfoLabel.Text = "Anyone who touches you gets flung away"
touchFlingInfoLabel.TextColor3 = COLORS.MUTED
touchFlingInfoLabel.BackgroundTransparency = 1
touchFlingInfoLabel.TextScaled = true
touchFlingInfoLabel.Font = Enum.Font.Gotham
touchFlingInfoLabel.TextWrapped = true
touchFlingInfoLabel.Parent = touchFlingPage

-- ===================== NOCLIP PAGE =====================
local noclipPage = Instance.new("Frame")
noclipPage.Name = "NoclipPage"
noclipPage.Size = UDim2.new(1, -100, 1, -60)
noclipPage.Position = UDim2.new(0, 95, 0, 50)
noclipPage.BackgroundTransparency = 1
noclipPage.Visible = false
noclipPage.Parent = frame

local noclipToggle = Instance.new("TextButton")
noclipToggle.Name = "NoclipToggle"
noclipToggle.Size = UDim2.new(1, 0, 0, 40)
noclipToggle.Text = "🚶 Noclip: OFF"
noclipToggle.TextColor3 = COLORS.TEXT
noclipToggle.BackgroundColor3 = COLORS.DANGER
noclipToggle.BorderSizePixel = 0
noclipToggle.TextScaled = true
noclipToggle.Font = Enum.Font.GothamSemibold
noclipToggle.Parent = noclipPage

local noclipToggleCorner = Instance.new("UICorner")
noclipToggleCorner.CornerRadius = UDim.new(0, 10)
noclipToggleCorner.Parent = noclipToggle

local noclipInfoLabel = Instance.new("TextLabel")
noclipInfoLabel.Name = "NoclipInfoLabel"
noclipInfoLabel.Size = UDim2.new(1, 0, 0, 30)
noclipInfoLabel.Position = UDim2.new(0, 0, 0, 50)
noclipInfoLabel.Text = "Walk through walls and parts"
noclipInfoLabel.TextColor3 = COLORS.MUTED
noclipInfoLabel.BackgroundTransparency = 1
noclipInfoLabel.TextScaled = true
noclipInfoLabel.Font = Enum.Font.Gotham
noclipInfoLabel.TextWrapped = true
noclipInfoLabel.Parent = noclipPage

local noclipKeybindLabel = Instance.new("TextLabel")
noclipKeybindLabel.Name = "NoclipKeybindLabel"
noclipKeybindLabel.Size = UDim2.new(1, 0, 0, 30)
noclipKeybindLabel.Position = UDim2.new(0, 0, 0, 85)
noclipKeybindLabel.Text = "Press N to toggle"
noclipKeybindLabel.TextColor3 = COLORS.ACCENT
noclipKeybindLabel.BackgroundTransparency = 1
noclipKeybindLabel.TextScaled = true
noclipKeybindLabel.Font = Enum.Font.GothamSemibold
noclipKeybindLabel.Parent = noclipPage

-- ===================== TAB SWITCHING =====================
local function switchTab(tabName)
	teleportPage.Visible = (tabName == "teleport")
	flyPage.Visible = (tabName == "fly")
	espPage.Visible = (tabName == "esp")
	flingPage.Visible = (tabName == "fling")
	touchFlingPage.Visible = (tabName == "touchfling")
	noclipPage.Visible = (tabName == "noclip")
	teleportTab.BackgroundColor3 = (tabName == "teleport") and COLORS.ACCENT or COLORS.SECONDARY
	flyTab.BackgroundColor3 = (tabName == "fly") and COLORS.ACCENT or COLORS.SECONDARY
	espTab.BackgroundColor3 = (tabName == "esp") and COLORS.ACCENT or COLORS.SECONDARY
	touchFlingTab.BackgroundColor3 = (tabName == "touchfling") and COLORS.ACCENT or COLORS.SECONDARY
	noclipTab.BackgroundColor3 = (tabName == "noclip") and COLORS.ACCENT or COLORS.SECONDARY
end

teleportTab.MouseButton1Click:Connect(function() switchTab("teleport") end)
flyTab.MouseButton1Click:Connect(function() switchTab("fly") end)
espTab.MouseButton1Click:Connect(function() switchTab("esp") end)
touchFlingTab.MouseButton1Click:Connect(function() switchTab("touchfling") end)
noclipTab.MouseButton1Click:Connect(function() switchTab("noclip") end)

-- ===================== TELEPORT LOGIC =====================
local function stopFollowing()
	following = false
	if followConnection then
		followConnection:Disconnect()
		followConnection = nil
	end
	if deathConnection then
		deathConnection:Disconnect()
		deathConnection = nil
	end
	followButton.Text = "🔗 Weld"
	followButton.BackgroundColor3 = COLORS.SUCCESS
end

local function onPlayerDeath()
	stopFollowing()
end

local function onCharacterAdded(character)
	local humanoid = character:WaitForChild("Humanoid")
	if deathConnection then
		deathConnection:Disconnect()
	end
	deathConnection = humanoid.Died:Connect(onPlayerDeath)
end

player.CharacterAdded:Connect(onCharacterAdded)
if player.Character then
	onCharacterAdded(player.Character)
end

local function createPlayerButton(playerName)
	local btn = Instance.new("TextButton")
	btn.Name = playerName .. "Button"
	btn.Size = UDim2.new(1, -10, 0, 35)
	btn.Text = "👤 " .. playerName
	btn.TextColor3 = COLORS.TEXT
	btn.BackgroundColor3 = COLORS.SECONDARY
	btn.BorderSizePixel = 0
	btn.TextScaled = true
	btn.Font = Enum.Font.Gotham
	btn.Parent = playerList

	local btnCorner = Instance.new("UICorner")
	btnCorner.CornerRadius = UDim.new(0, 6)
	btnCorner.Parent = btn

	animateButton(btn, Color3.new(0.16, 0.16, 0.22), COLORS.SECONDARY)

	btn.MouseButton1Click:Connect(function()
		local playerObj = game.Players:FindFirstChild(playerName)
		if playerObj and playerObj.Character and playerObj.Character:FindFirstChild("HumanoidRootPart") then
			if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
				player.Character.HumanoidRootPart.CFrame = playerObj.Character.HumanoidRootPart.CFrame
			end
		end
		targetPlayer = playerObj
		flingTarget = playerObj
		flingTargetDropdown.Text = "🎯 " .. playerName
		dropdownButton.Text = "🎯 " .. playerName
		playerList.Visible = false
		local hideTween = TweenService:Create(playerList,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Size = UDim2.new(0, 300, 0, 0)}
		)
		hideTween:Play()
	end)
end

local function updatePlayerList()
	for _, child in pairs(playerList:GetChildren()) do
		if child:IsA("TextButton") then
			child:Destroy()
		end
	end
	local playerCount = 0
	for _, otherPlayer in pairs(game.Players:GetPlayers()) do
		if otherPlayer ~= player then
			createPlayerButton(otherPlayer.Name)
			playerCount = playerCount + 1
		end
	end
	playerList.CanvasSize = UDim2.new(0, 0, 0, playerCount * 37)
end

updatePlayerList()
game.Players.PlayerAdded:Connect(updatePlayerList)
game.Players.PlayerRemoving:Connect(updatePlayerList)

followButton.MouseButton1Click:Connect(function()
	following = not following
	if following then
		followButton.Text = "🔓 Turn off"
		followButton.BackgroundColor3 = COLORS.DANGER
		followConnection = RunService.Heartbeat:Connect(function()
			if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
				if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
					player.Character.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
				end
			end
		end)
		if player.Character and player.Character:FindFirstChild("Humanoid") then
			if deathConnection then deathConnection:Disconnect() end
			deathConnection = player.Character.Humanoid.Died:Connect(onPlayerDeath)
		end
	else
		stopFollowing()
	end
end)

teleportButton.MouseButton1Click:Connect(function()
	if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
		if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
			player.Character.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
		end
	end
end)

dropdownButton.MouseButton1Click:Connect(function()
	flingTargetDropdown.Text = "📋 Select Target"
	flingTarget = nil
	if playerList.Visible then
		local hideTween = TweenService:Create(playerList,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Size = UDim2.new(0, 300, 0, 0)}
		)
		hideTween:Play()
		hideTween.Completed:Connect(function() playerList.Visible = false end)
	else
		playerList.Visible = true
		playerList.Size = UDim2.new(0, 300, 0, 0)
		local showTween = TweenService:Create(playerList,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Size = UDim2.new(0, 300, 0, -220)}
		)
		showTween:Play()
	end
end)

flingTargetDropdown.MouseButton1Click:Connect(function()
	dropdownButton.Text = "📋 Player LeaderBoard"
	targetPlayer = nil
	if playerList.Visible then
		local hideTween = TweenService:Create(playerList,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Size = UDim2.new(0, 300, 0, 0)}
		)
		hideTween:Play()
		hideTween.Completed:Connect(function() playerList.Visible = false end)
	else
		playerList.Visible = true
		playerList.Size = UDim2.new(0, 300, 0, 0)
		local showTween = TweenService:Create(playerList,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Size = UDim2.new(0, 300, 0, -220)}
		)
		showTween:Play()
	end
end)

-- ===================== FLY LOGIC =====================
local function startFly()
	local character = player.Character
	if not character then return end
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	local hrp = character:FindFirstChild("HumanoidRootPart")
	if not humanoid or not hrp then return end

	flying = true
	flyToggle.Text = "✈ Fly: ON"
	flyToggle.BackgroundColor3 = COLORS.SUCCESS

	humanoid.PlatformStand = true

	flyBodyVelocity = Instance.new("BodyVelocity")
	flyBodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
	flyBodyVelocity.Velocity = Vector3.new(0, 0, 0)
	flyBodyVelocity.Parent = hrp

	flyBodyGyro = Instance.new("BodyGyro")
	flyBodyGyro.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
	flyBodyGyro.P = 9e4
	flyBodyGyro.Parent = hrp

	flyConnection = RunService.Heartbeat:Connect(function()
		if not flying then return end
		if not character or not character.Parent then
			stopFly()
			return
		end

		local camera = workspace.CurrentCamera
		local moveDir = Vector3.new(0, 0, 0)

		if UserInputService:IsKeyDown(Enum.KeyCode.W) then
			moveDir = moveDir + camera.CFrame.LookVector
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.S) then
			moveDir = moveDir - camera.CFrame.LookVector
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.A) then
			moveDir = moveDir - camera.CFrame.RightVector
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.D) then
			moveDir = moveDir + camera.CFrame.RightVector
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
			moveDir = moveDir + Vector3.new(0, 1, 0)
		end
		if UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then
			moveDir = moveDir - Vector3.new(0, 1, 0)
		end

		if moveDir.Magnitude > 0 then
			moveDir = moveDir.Unit * flySpeed
		end

		flyBodyVelocity.Velocity = moveDir
		flyBodyGyro.CFrame = camera.CFrame
	end)
end

function stopFly()
	flying = false
	flyToggle.Text = "✈ Fly: OFF"
	flyToggle.BackgroundColor3 = COLORS.DANGER

	if flyBodyVelocity then
		flyBodyVelocity:Destroy()
		flyBodyVelocity = nil
	end
	if flyBodyGyro then
		flyBodyGyro:Destroy()
		flyBodyGyro = nil
	end
	if flyConnection then
		flyConnection:Disconnect()
		flyConnection = nil
	end

	local character = player.Character
	if character then
		local humanoid = character:FindFirstChildOfClass("Humanoid")
		if humanoid then
			humanoid.PlatformStand = false
		end
	end
end

flyToggle.MouseButton1Click:Connect(function()
	if flying then
		stopFly()
	else
		startFly()
	end
end)

-- Stop fly on death
player.CharacterAdded:Connect(function(character)
	if flying then
		stopFly()
	end
	local humanoid = character:WaitForChild("Humanoid")
	humanoid.Died:Connect(function()
		if flying then stopFly() end
	end)
end)

-- ===================== SPEED SLIDER =====================
local MIN_SPEED = 10
local MAX_SPEED = 200

local function updateSpeedSlider(value)
	flySpeed = value
	speedLabel.Text = "Speed: " .. tostring(math.floor(value))
	local percent = (value - MIN_SPEED) / (MAX_SPEED - MIN_SPEED)
	speedSliderFill.Size = UDim2.new(percent, 0, 1, 0)
	speedSliderKnob.Position = UDim2.new(percent, -10, 0, -2)
end

local sliderDragging = false

speedSliderKnob.MouseButton1Down:Connect(function()
	sliderDragging = true
end)

UserInputService.InputChanged:Connect(function(input)
	if sliderDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local relX = (input.Position.X - speedSliderBg.AbsolutePosition.X) / speedSliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		local newSpeed = MIN_SPEED + relX * (MAX_SPEED - MIN_SPEED)
		updateSpeedSlider(newSpeed)
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		sliderDragging = false
	end
end)

-- Click on slider bar to jump to position
speedSliderBg.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		local relX = (input.Position.X - speedSliderBg.AbsolutePosition.X) / speedSliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		local newSpeed = MIN_SPEED + relX * (MAX_SPEED - MIN_SPEED)
		updateSpeedSlider(newSpeed)
		sliderDragging = true
	end
end)

-- Initialize slider
updateSpeedSlider(50)

-- ===================== MM2 ESP LOGIC =====================
--[[
	Credits to Kiriot22 for the Role getter <3
	- poorly coded by FeIix <3
]]
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local function isAlive(p, rolesData)
	for name, data in pairs(rolesData) do
		if p.Name == name then
			if not data.Killed and not data.Dead then
				return true
			else
				return false
			end
		end
	end
	return false
end

local function createHighlights()
	for _, v in pairs(game.Players:GetChildren()) do
		if v ~= player and v.Character and not v.Character:FindFirstChild("EspHighlight") then
			local hl = Instance.new("Highlight")
			hl.Name = "EspHighlight"
			hl.FillTransparency = 0.5
			hl.OutlineTransparency = 0
			hl.Parent = v.Character
		end
	end
end

local function updateHighlights()
	local getDataFunc = ReplicatedStorage:FindFirstChild("GetPlayerData", true)
	if not getDataFunc then return end

	local success, roles = pcall(function()
		return getDataFunc:InvokeServer()
	end)
	if not success or not roles then return end

	for name, data in pairs(roles) do
		if data.Role == "Murderer" then
			Murder = name
		elseif data.Role == "Sheriff" then
			Sheriff = name
		elseif data.Role == "Hero" then
			Hero = name
		end
	end

	for _, v in pairs(game.Players:GetChildren()) do
		if v ~= player and v.Character and v.Character:FindFirstChild("EspHighlight") then
			local hl = v.Character:FindFirstChild("EspHighlight")
			if v.Name == Murder and isAlive(v, roles) then
				hl.FillColor = Color3.fromRGB(225, 0, 0)
			elseif v.Name == Sheriff and isAlive(v, roles) then
				hl.FillColor = Color3.fromRGB(0, 0, 225)
			elseif v.Name == Hero and isAlive(v, roles) and Sheriff and not isAlive(game.Players[Sheriff], roles) then
				hl.FillColor = Color3.fromRGB(255, 250, 0)
			else
				hl.FillColor = Color3.fromRGB(0, 225, 0)
			end
		end
	end
end

local function startEsp()
	espEnabled = true
	espToggle.Text = "👁 MM2 ESP: ON"
	espToggle.BackgroundColor3 = COLORS.SUCCESS

	espConnection = RunService.RenderStepped:Connect(function()
		if not espEnabled then return end
		createHighlights()
		updateHighlights()
	end)
end

local function stopEsp()
	espEnabled = false
	espToggle.Text = "👁 MM2 ESP: OFF"
	espToggle.BackgroundColor3 = COLORS.DANGER

	if espConnection then
		espConnection:Disconnect()
		espConnection = nil
	end

	Murder = nil
	Sheriff = nil
	Hero = nil

	for _, v in pairs(game.Players:GetChildren()) do
		if v.Character and v.Character:FindFirstChild("EspHighlight") then
			v.Character.EspHighlight:Destroy()
		end
	end
end

espToggle.MouseButton1Click:Connect(function()
	if espEnabled then
		stopEsp()
	else
		startEsp()
	end
end)

-- Clean up ESP highlights when players leave
game.Players.PlayerRemoving:Connect(function(leavingPlayer)
	if leavingPlayer.Character and leavingPlayer.Character:FindFirstChild("EspHighlight") then
		leavingPlayer.Character.EspHighlight:Destroy()
	end
end)

-- ===================== FLING LOGIC =====================

local function doFling(targetPlr)
	if not targetPlr or not targetPlr.Character or not targetPlr.Character:FindFirstChild("HumanoidRootPart") then return end
	if not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then return end

	local myHRP = player.Character.HumanoidRootPart
	local targetHRP = targetPlr.Character.HumanoidRootPart

	local savedCFrame = myHRP.CFrame

	myHRP.CFrame = targetHRP.CFrame * CFrame.new(0, 0, 2)

	local weld = Instance.new("WeldConstraint")
	weld.Part0 = myHRP
	weld.Part1 = targetHRP
	weld.Parent = myHRP

	local bav = Instance.new("BodyAngularVelocity")
	bav.AngularVelocity = Vector3.new(flingPower, flingPower, flingPower)
	bav.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
	bav.Parent = myHRP

	task.wait(0.3)

	weld:Destroy()
	bav:Destroy()
	myHRP.CFrame = savedCFrame
end

flingActionButton.MouseButton1Click:Connect(function()
	if flingTarget then
		coroutine.wrap(function()
			flingActionButton.Text = "💨 Flinging..."
			flingActionButton.BackgroundColor3 = COLORS.SUCCESS
			doFling(flingTarget)
			flingActionButton.Text = "💨 Fling Target"
			flingActionButton.BackgroundColor3 = COLORS.ACCENT
		end)()
	end
end)

-- ===================== FLING POWER SLIDER =====================
local MIN_FLING_POWER = 100
local MAX_FLING_POWER = 2000

local function updateFlingPowerSlider(value)
	flingPower = value
	flingPowerLabel.Text = "Power: " .. tostring(math.floor(value))
	multiflingPowerLabel.Text = "Fling Power: " .. tostring(math.floor(value))
	local percent = (value - MIN_FLING_POWER) / (MAX_FLING_POWER - MIN_FLING_POWER)
	flingPowerSliderFill.Size = UDim2.new(percent, 0, 1, 0)
	flingPowerSliderKnob.Position = UDim2.new(percent, -10, 0, -2)
	multiflingPowerSliderFill.Size = UDim2.new(percent, 0, 1, 0)
	multiflingPowerSliderKnob.Position = UDim2.new(percent, -9, 0, -2)
end

local flingSliderDragging = false

flingPowerSliderKnob.MouseButton1Down:Connect(function()
	flingSliderDragging = true
end)

flingPowerSliderBg.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		local relX = (input.Position.X - flingPowerSliderBg.AbsolutePosition.X) / flingPowerSliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		updateFlingPowerSlider(MIN_FLING_POWER + relX * (MAX_FLING_POWER - MIN_FLING_POWER))
		flingSliderDragging = true
	end
end)

multiflingPowerSliderKnob.MouseButton1Down:Connect(function()
	flingSliderDragging = true
end)

multiflingPowerSliderBg.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		local relX = (input.Position.X - multiflingPowerSliderBg.AbsolutePosition.X) / multiflingPowerSliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		updateFlingPowerSlider(MIN_FLING_POWER + relX * (MAX_FLING_POWER - MIN_FLING_POWER))
		flingSliderDragging = true
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if flingSliderDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local sliderBg = flingPowerSliderBg
		local relX = (input.Position.X - sliderBg.AbsolutePosition.X) / sliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		updateFlingPowerSlider(MIN_FLING_POWER + relX * (MAX_FLING_POWER - MIN_FLING_POWER))
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		flingSliderDragging = false
	end
end)

updateFlingPowerSlider(500)

-- ===================== MULTIFLING LOGIC =====================
local function createMultiflingPlayerButton(otherPlayer)
	local row = Instance.new("Frame")
	row.Name = otherPlayer.Name .. "Row"
	row.Size = UDim2.new(1, 0, 0, 35)
	row.BackgroundColor3 = COLORS.SECONDARY
	row.BorderSizePixel = 0
	row.Parent = multiflingPlayerList

	local rowCorner = Instance.new("UICorner")
	rowCorner.CornerRadius = UDim.new(0, 6)
	rowCorner.Parent = row

	local nameLabel = Instance.new("TextLabel")
	nameLabel.Size = UDim2.new(1, -80, 1, 0)
	nameLabel.Position = UDim2.new(0, 8, 0, 0)
	nameLabel.Text = "👤 " .. otherPlayer.Name
	nameLabel.TextColor3 = COLORS.TEXT
	nameLabel.BackgroundTransparency = 1
	nameLabel.TextScaled = true
	nameLabel.Font = Enum.Font.Gotham
	nameLabel.TextXAlignment = Enum.TextXAlignment.Left
	nameLabel.Parent = row

	local flingBtn = Instance.new("TextButton")
	flingBtn.Size = UDim2.new(0, 65, 0, 25)
	flingBtn.Position = UDim2.new(1, -72, 0.5, -12.5)
	flingBtn.Text = "💨 Fling"
	flingBtn.TextColor3 = COLORS.TEXT
	flingBtn.BackgroundColor3 = COLORS.ACCENT
	flingBtn.BorderSizePixel = 0
	flingBtn.TextScaled = true
	flingBtn.Font = Enum.Font.GothamSemibold
	flingBtn.Parent = row

	local flingBtnCorner = Instance.new("UICorner")
	flingBtnCorner.CornerRadius = UDim.new(0, 6)
	flingBtnCorner.Parent = flingBtn

	animateButton(flingBtn, Color3.new(0.65, 0.35, 0.95), COLORS.ACCENT)

	flingBtn.MouseButton1Click:Connect(function()
		coroutine.wrap(function()
			flingBtn.Text = "..."
			flingBtn.BackgroundColor3 = COLORS.SUCCESS
			doFling(otherPlayer)
			flingBtn.Text = "💨 Fling"
			flingBtn.BackgroundColor3 = COLORS.ACCENT
		end)()
	end)
end

local function updateMultiflingList()
	for _, child in pairs(multiflingPlayerList:GetChildren()) do
		if child:IsA("Frame") then
			child:Destroy()
		end
	end
	local count = 0
	for _, otherPlayer in pairs(game.Players:GetPlayers()) do
		if otherPlayer ~= player then
			createMultiflingPlayerButton(otherPlayer)
			count = count + 1
		end
	end
	multiflingPlayerList.CanvasSize = UDim2.new(0, 0, 0, count * 39)
end

flingAllButton.MouseButton1Click:Connect(function()
	coroutine.wrap(function()
		flingAllButton.Text = "💥 Flinging All..."
		flingAllButton.BackgroundColor3 = COLORS.SUCCESS
		for _, otherPlayer in pairs(game.Players:GetPlayers()) do
			if otherPlayer ~= player and otherPlayer.Character and otherPlayer.Character:FindFirstChild("HumanoidRootPart") then
				doFling(otherPlayer)
				task.wait(0.35)
			end
		end
		flingAllButton.Text = "💥 Fling All Players"
		flingAllButton.BackgroundColor3 = COLORS.DANGER
	end)()
end)

multiflingButton.MouseButton1Click:Connect(function()
	if not multiflingOpen then
		multiflingOpen = true
		multiflingFrame.Visible = true
		multiflingFrame.Size = UDim2.new(0, 300, 0, 0)
		updateMultiflingList()
		local showTween = TweenService:Create(multiflingFrame,
			TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, 300, 0, 400)}
		)
		showTween:Play()
	end
end)

multiflingCloseBtn.MouseButton1Click:Connect(function()
	multiflingOpen = false
	local hideTween = TweenService:Create(multiflingFrame,
		TweenInfo.new(0.3, Enum.EasingStyle.Quad),
		{Size = UDim2.new(0, 300, 0, 0)}
	)
	hideTween:Play()
	hideTween.Completed:Connect(function() multiflingFrame.Visible = false end)
end)

animateButton(multiflingCloseBtn, Color3.new(1, 0.3, 0.4), COLORS.DANGER)
animateButton(flingActionButton, Color3.new(0.65, 0.35, 0.95), COLORS.ACCENT)
animateButton(multiflingButton, Color3.new(0.35, 0.65, 1), COLORS.BLUE)
animateButton(flingAllButton, Color3.new(1, 0.3, 0.4), COLORS.DANGER)
animateButton(flingTargetDropdown, Color3.new(0.18, 0.18, 0.24), COLORS.CARD)

game.Players.PlayerAdded:Connect(function()
	if multiflingOpen then
		updateMultiflingList()
	end
end)

game.Players.PlayerRemoving:Connect(function()
	if multiflingOpen then
		updateMultiflingList()
	end
end)

-- ===================== NOCLIP LOGIC =====================
local function startNoclip()
	noclipEnabled = true
	noclipToggle.Text = "🚶 Noclip: ON"
	noclipToggle.BackgroundColor3 = COLORS.SUCCESS

	noclipConnection = RunService.Stepped:Connect(function()
		if not noclipEnabled then return end
		local character = player.Character
		if character then
			for _, part in pairs(character:GetDescendants()) do
				if part:IsA("BasePart") and part.CanCollide then
					part.CanCollide = false
				end
			end
		end
	end)
end

local function stopNoclip()
	noclipEnabled = false
	noclipToggle.Text = "🚶 Noclip: OFF"
	noclipToggle.BackgroundColor3 = COLORS.DANGER

	if noclipConnection then
		noclipConnection:Disconnect()
		noclipConnection = nil
	end

	local character = player.Character
	if character then
		for _, part in pairs(character:GetDescendants()) do
			if part:IsA("BasePart") then
				part.CanCollide = true
			end
		end
	end
end

noclipToggle.MouseButton1Click:Connect(function()
	if noclipEnabled then
		stopNoclip()
	else
		startNoclip()
	end
end)

-- N keybind to toggle noclip
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.KeyCode == Enum.KeyCode.N then
		if noclipEnabled then
			stopNoclip()
		else
			startNoclip()
		end
	end
end)

-- Stop noclip on death
player.CharacterAdded:Connect(function(character)
	if noclipEnabled then
		stopNoclip()
	end
end)

animateButton(noclipToggle, Color3.new(0.25, 0.95, 0.6), COLORS.SUCCESS)

-- ===================== TOUCHFLING LOGIC =====================
local MIN_TOUCH_FLING_POWER = 100
local MAX_TOUCH_FLING_POWER = 2000

local function updateTouchFlingPowerSlider(value)
	touchFlingPower = value
	touchFlingPowerLabel.Text = "Power: " .. tostring(math.floor(value))
	local percent = (value - MIN_TOUCH_FLING_POWER) / (MAX_TOUCH_FLING_POWER - MIN_TOUCH_FLING_POWER)
	touchFlingPowerSliderFill.Size = UDim2.new(percent, 0, 1, 0)
	touchFlingPowerSliderKnob.Position = UDim2.new(percent, -10, 0, -2)
end

local touchFlingSliderDragging = false

touchFlingPowerSliderKnob.MouseButton1Down:Connect(function()
	touchFlingSliderDragging = true
end)

touchFlingPowerSliderBg.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		local relX = (input.Position.X - touchFlingPowerSliderBg.AbsolutePosition.X) / touchFlingPowerSliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		updateTouchFlingPowerSlider(MIN_TOUCH_FLING_POWER + relX * (MAX_TOUCH_FLING_POWER - MIN_TOUCH_FLING_POWER))
		touchFlingSliderDragging = true
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if touchFlingSliderDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local relX = (input.Position.X - touchFlingPowerSliderBg.AbsolutePosition.X) / touchFlingPowerSliderBg.AbsoluteSize.X
		relX = math.clamp(relX, 0, 1)
		updateTouchFlingPowerSlider(MIN_TOUCH_FLING_POWER + relX * (MAX_TOUCH_FLING_POWER - MIN_TOUCH_FLING_POWER))
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		touchFlingSliderDragging = false
	end
end)

updateTouchFlingPowerSlider(500)

local function touchFlingOnTouched(otherPart)
	if not touchFlingEnabled then return end

	local character = otherPart.Parent
	if not character then return end

	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if not humanoid or humanoid.Health <= 0 then return end

	local targetHRP = character:FindFirstChild("HumanoidRootPart")
	if not targetHRP then return end

	-- Don't fling yourself
	if character == player.Character then return end

	-- Debounce per character so we don't fling the same person every frame
	if touchFlingDebounce[character] then return end
	touchFlingDebounce[character] = true
	task.delay(1, function()
		touchFlingDebounce[character] = nil
	end)

	-- Apply fling velocity to the target
	local flingDir = (targetHRP.Position - player.Character.HumanoidRootPart.Position).Unit
	targetHRP.AssemblyLinearVelocity = flingDir * touchFlingPower + Vector3.new(0, touchFlingPower * 0.3, 0)
end

local function startTouchFling()
	touchFlingEnabled = true
	touchFlingToggle.Text = "💫 TouchFling: ON"
	touchFlingToggle.BackgroundColor3 = COLORS.SUCCESS

	-- Clear any old connections
	for _, conn in pairs(touchFlingConnections) do
		conn:Disconnect()
	end
	touchFlingConnections = {}

	-- Connect Touched to every part of the player's character
	local function connectCharacterParts(character)
		for _, part in pairs(character:GetDescendants()) do
			if part:IsA("BasePart") then
				local conn = part.Touched:Connect(touchFlingOnTouched)
				table.insert(touchFlingConnections, conn)
			end
		end
	end

	if player.Character then
		connectCharacterParts(player.Character)
	end

	-- Also connect when character respawns or new parts are added
	local charAddedConn = player.CharacterAdded:Connect(function(character)
		if not touchFlingEnabled then return end
		-- Wait a brief moment for parts to exist
		task.wait(0.5)
		if not touchFlingEnabled then return end
		connectCharacterParts(character)
	end)
	table.insert(touchFlingConnections, charAddedConn)

	local descendantAddedConn = player.Character and player.Character.DescendantAdded:Connect(function(desc)
		if not touchFlingEnabled then return end
		if desc:IsA("BasePart") then
			local conn = desc.Touched:Connect(touchFlingOnTouched)
			table.insert(touchFlingConnections, conn)
		end
	end)
	if descendantAddedConn then
		table.insert(touchFlingConnections, descendantAddedConn)
	end
end

local function stopTouchFling()
	touchFlingEnabled = false
	touchFlingToggle.Text = "💫 TouchFling: OFF"
	touchFlingToggle.BackgroundColor3 = COLORS.DANGER

	for _, conn in pairs(touchFlingConnections) do
		conn:Disconnect()
	end
	touchFlingConnections = {}

	-- Clear debounce
	for key in pairs(touchFlingDebounce) do
		touchFlingDebounce[key] = nil
	end
end

touchFlingToggle.MouseButton1Click:Connect(function()
	if touchFlingEnabled then
		stopTouchFling()
	else
		startTouchFling()
	end
end)

-- Stop touch fling on death
player.CharacterAdded:Connect(function(character)
	if touchFlingEnabled then
		-- Don't fully stop, just let the CharacterAdded handler in startTouchFling reconnect
		-- But if we died, we need to wait for respawn. The connections are already cleaned up
		-- since the old character's parts are destroyed. The charAddedConn will reconnect.
	end
end)

animateButton(touchFlingToggle, Color3.new(0.25, 0.95, 0.6), COLORS.SUCCESS)

-- ===================== CONFIRM DIALOG =====================
local function showConfirmDialog()
	confirmDialog.Visible = true
	confirmDialog.Size = UDim2.new(0, 0, 0, 0)
	local showTween = TweenService:Create(confirmDialog,
		TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
		{Size = UDim2.new(0, 300, 0, 150)}
	)
	showTween:Play()
end

local function hideConfirmDialog()
	local hideTween = TweenService:Create(confirmDialog,
		TweenInfo.new(0.3, Enum.EasingStyle.Quad),
		{Size = UDim2.new(0, 0, 0, 0)}
	)
	hideTween:Play()
	hideTween.Completed:Connect(function() confirmDialog.Visible = false end)
end

yesButton.MouseButton1Click:Connect(function()
	hideConfirmDialog()
	stopFollowing()
	stopFly()
	stopEsp()
	stopNoclip()
	stopTouchFling()
	multiflingFrame.Visible = false
	multiflingOpen = false
	local closeTween = TweenService:Create(frame,
		TweenInfo.new(0.3, Enum.EasingStyle.Quad),
		{Size = UDim2.new(0, 0, 0, 0)}
	)
	closeTween:Play()
	closeTween.Completed:Connect(function()
		screenGui:Destroy()
	end)
end)

noButton.MouseButton1Click:Connect(function()
	hideConfirmDialog()
end)

closeButton.MouseButton1Click:Connect(function()
	showConfirmDialog()
end)

-- ===================== HIDE/SHOW =====================
hideButton.MouseButton1Click:Connect(function()
	if frame.Visible then
		hideButton.Text = "HUB"
		local hideTween = TweenService:Create(frame,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Position = UDim2.new(0.5, -220, 0, -400)}
		)
		hideTween:Play()
		hideTween.Completed:Connect(function() frame.Visible = false end)
	else
		frame.Visible = true
		hideButton.Text = "✕"
		frame.Position = UDim2.new(0.5, -220, 0, -400)
		local showTween = TweenService:Create(frame,
			TweenInfo.new(0.3, Enum.EasingStyle.Quad),
			{Position = UDim2.new(0.5, -220, 0.5, -175)}
		)
		showTween:Play()
	end
end)

-- ===================== CLICK OUTSIDE PLAYER LIST =====================
UserInputService.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		if playerList.Visible then
			local mouse = player:GetMouse()
			local mousePos = Vector2.new(mouse.X, mouse.Y)
			local listPos = playerList.AbsolutePosition
			local listSize = playerList.AbsoluteSize
			if mousePos.X < listPos.X or mousePos.X > listPos.X + listSize.X or
				mousePos.Y < listPos.Y or mousePos.Y > listPos.Y + listSize.Y then
				playerList.Visible = false
				local hideTween = TweenService:Create(playerList,
					TweenInfo.new(0.3, Enum.EasingStyle.Quad),
					{Size = UDim2.new(0, 300, 0, 0)}
				)
				hideTween:Play()
			end
		end
	end
end)
