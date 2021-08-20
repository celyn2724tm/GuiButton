# GuiButton
Global $g_hWnd1, $g_hWnd2 Global $g_hCheckBox

Run('MSTSC.exe "C:\Users\Public\Desktop\RDP Consoles\administrator@windows-1.rdp"')

; There's two warning windows that appear

$g_hWnd1 = WinWait('Remote Desktop Connection', '', 5) ; Wait for the first warning window
If IsHWnd($g_hWnd1) = 1 Then ; Check if the first warning window handle was obtained
    Sleep(2500) ; Wait 2.5 seconds - without a wait, the buttons aren't clicked
    $g_hCheckBox = ControlGetHandle($g_hWnd1, '', '[CLASS:Button; INSTANCE:1]') ; Get the control handle for the checkbox
    _GUICtrlButton_SetCheck($g_hCheckBox, True) ; Check the checkbox
    ControlClick($g_hWnd1, '', '[CLASS:Button; INSTANCE:11]') ; Click the Yes button
EndIf

Sleep(1000)

$g_hWnd1 = WinWait('Remote Desktop Connection', '', 5) ; Wait for the second warning window
If IsHWnd($g_hWnd1) = 1 Then ; Check if the second warning window handle was obtained
    Sleep(2500) ; Wait 2.5 seconds - without a wait, the buttons aren't clicked
    $g_hCheckBox = ControlGetHandle($g_hWnd1, '', '[CLASS:Button; INSTANCE:3]') ; Get the control handle for the checkbox
    _GUICtrlButton_SetCheck($g_hCheckBox, True) ; Check the checkbox
    ControlClick($g_hWnd1, '', '[CLASS:Button; INSTANCE:5]') ; Click the Yes button
EndIf

Sleep(1000)

$g_hWnd1 = WinWait('administrator - windows-1', '', 5) ; Wait for the Remote Desktop Connection to appear
If IsHWnd($g_hWnd1) = 1 Then ; Check if the Remote Desktop Connection window handle was obtained
    WinClose($g_hWnd1) ; Close the window
    $g_hWnd2 = WinWait('Remote Desktop Connection', '', 5) ; Wait for the close confirmation window
    If IsHWnd($g_hWnd2) = 1 Then ; Check that we found the above window
        ControlClick($g_hWnd2, '', '[CLASS:Button; INSTANCE:1]') ; Click Yes
    EndIf
    WinWaitClose($g_hWnd1, '', 5) ; Wait for the RDP to close
EndIf
