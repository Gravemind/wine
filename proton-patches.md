
## ValveSoftware/wine Proton patches applied here:

```bash
# Display Proton patch list:
$> git log --oneline wine-3.16..valve/proton_3.16

# Cherry-pick the ones selected ('->') here:
$> grep '^-> ' proton-patches.md | cut -d\  -f 2 | tac | xargs git cherry-pick
```

Patches are enabled somewhat arbitrarily, vaguely trying to:
- enable lsteamclient for steam-for-linux
- have better defaults (no home symlinks, no winemenubuilder...)
- get the simple useful patches (debugging...)
- but no big patches to try to stay close to wine+staging behaviors (no esync,
  no fullscreen hack...).

```
174d487bf8 wine.inf: Substitute Times New Roman for Palatino Linotype
(wine) e2419cdf58 msi: Fix a typo.
-> 1091eaf136 HACK: wined3d: Fake an AMD card in place of Nvidia cards
(wine) 0383764d08 start: Try cycling through extensions if original path failed to execute.
a23b338acc winex11.drv: Force changing lock keys state if hooks blocked keyboard input processing.
907ae52165 user32: Call DefWindowProc() in DesktopWndProc().
66a7462d98 winex11: enable fullscreen clipping even if not already clipping
0fa3321136 winex11: ignore clip_reset when trying to clip the mouse after the desktop has been resized
(wine) 63f934962c wine.inf: Add font registry entries.
212551db58 dinput: Don't dump a NULL effect.
5802561438 wined3d: Avoid accessing the device after deactivation some more.
d992dcb820 wined3d: Avoid accessing the device after minimize in ddraw.
4d742761c5 wined3d: Deactivate the device before minimizing the window.
41f7b9c349 crypt32: Add CRYPT_STRING_BINARY mode for CryptBinaryToStringW().
6169367ac7 crypt32: Fix formatted output length for base64.
dc47a33b40 crypt32: Fix output buffer handling for CRYPT_STRING_BINARY case.
ba61ebe15c crypt32: Fix NULL output buffer handling for CryptBinaryToString().
(wine) a45cb4255d crypt32/base64: Fix certificate request header and trailer in CryptBinaryToStringW() output.
266d11ab06 d3d11: Remove unused 'depth_tex' variable.
d856e7a941 winevulkan: Enable VK_EXT_transform_feedback.
508e940d13 winevulkan: Update vk.xml to 1.1.86.
18407aa65e winevulkan: Parse enum value aliases.
9d57a9e234 winevulkan: Check if conversion is required for pNext chains.
5c35090e4c winevulkan: Remove parsing of validextensionstructs.
141ba5cf73 winex11.drv: Bypass compositor in fullscreen mode
(wine) 7f59fd6d31 winedbg: Ignore ^C events in the parent 32-bit process.
6350a916c1 wined3d: Add GL_ARB_shader_viewport_layer_array extension.
7121928034 Revert "winevulkan: Check if device extensions are supported."
04a83c6f48 Revert "winevulkan: Check if instance extensions are supported."
2defa0be4d ntdll: Improve heap allocation performance. (v2)
37c6d158a6 ntdll: Add helper function to delete free blocks.
d594b87433 d3d11: Pass IWineD3D11Texture2D to access_gl_texture().
edb56564cb wined3d: Load TEXTURE_RGB location for synchronous texture access.
1a540c0bc0 wined3d: Implement synchronous texture access.
867cfaca90 wined3d: Get rid of wined3d_cs_emit_wait_idle().
7a0711b3d3 winex11.drv: Fix sub pixel raw motion v3
(wine) 60be769e19 winedbg: In gdbproxy file, allow wine paths with spaces
-> d012d137e4 HACK: dbghelp: Disable DWARF parsing
e619f83959 winex11: Always show a close button
8c78517f1b winex11: Allow the application to change window size and states during PropertyNotify
eb87472b52 winex11: Detect erroneous FocusOut messages for longer
39075cb0aa winex11: Don't set ABOVE on minimized fullscreened windows
2e09c33f98 winex11: Fullscreen hack, don't clip when restoring real resolution
75fc0f36aa winex11: Fullscreen hack, don't ever blit to the frontbuffer after a wglSwapBuffers().
84a0501fed winex11: Fullscreen hack, also hook glBindFramebufferEXT().
2717f60b56 winex11: Fullscreen hack, don't setup the hack again on every wglMakeCurrent().
-> eece6bb2e4 ntdll,server: Never use CLOCK_MONOTONIC_RAW
fd316f75c8 winebus: Show an ERR on old SDL
15c6ecef86 dinput: Don't fail to load on old SDL
132b08339e winex11.drv: fs hack, round scaled coordinates to nearest int
830bef4031 winex11: Revamp display resolution options
6706472d4d ntdll: Correctly allocate the esync handle cache.
daefcfea47 HACK: winex11: Grab mouse in fullscreen windows by default
f59f59650f HACK: winex11: Work around mutter WM bug
29a2c4f1b8 secur32: Return real Unix username from GetUserNameEx(NameDisplay)
1c327ac707 winex11: Also set up fs hack during framebuffer swap
c6152e760d winex11: Set up the context again for fs hack if the size changes
b8ecb9e4d3 esync: Update README.
003c2092fd ntdll, server: Abort if esync is enabled for the server but not the client, and vice versa.
aa7fa7ce94 server: Set default timeout to 0
a3752f468d dinput: Use the VID/PID for the first chunk of the device product GUID
4d49baf456 winebus: Don't override real VID/PID for controllers
ded6f0fb31 ntdll: Fix a missing break statement.
93fbd06513 server: Update the shared memory state when (re)setting an event.
580e74ae3f ntdll: Fix growing the shm_addrs array.
35b6e77232 ntdll: Store an event's signaled state internally.
cc7d88d5ae ntdll: Try to avoid poll() for uncontended objects.
c3dbf18a30 ntdll: Ignore pseudo-handles.
afc08b394a esync: Add note about file limits not being raised when using systemd.
1c0f2f6600 esync: Update README.
583ff94d83 ntdll: Cache the esync struct itself instead of a pointer to it.
567d7386ab server: Create eventfd descriptors for pseudo-fd objects and use them for named pipes.
da9ba5bc63 ntdll: Implement NtQueryMutant().
8c0ec80838 ntdll: Implement NtQueryEvent().
b1b2e330de ntdll: Implement NtQuerySemaphore().
41c705a214 server: Try to remove a preëxisting shm file.
1235c8bffa kernel32/tests: Zigzag test.
-> 3c9b9d5a29 wine.inf: Set amd_ags_x64 to built-in for Wolfenstein 2
-> e0c31d82fb amd_ags_x64: Add dll.
-> e10f7f83b4 amd_ags_x64: Make amd_ags.h usable with gcc.
-> afaf271f5a amd_ags_x64: Import v5.1.1 amd_ags.h.
-> 059a15a1d5 HACK: mshtml: Don't install wine-gecko on prefix creation
-> 7f3acf2172 HACK: mscoree: Don't install wine-mono on prefix creation
(staging) e9528f72ef winepulse: Don't rely on pulseaudio callbacks for timing
242ef5ef0d HACK: winex11: Let the WM focus our windows by default
7d6875dee3 xaudio2: Make a log file when the game uses WMA
4449b36208 server: Don't check for a hung queue when sending low-level hooks.
15dd3e8acf user32: Remove hooks that time out.
71cb6db452 ntdll: Avoid server_select() when waiting for critical sections.
b69924e8cc ntdll: Let the server know when we are doing a message wait.
be2d123be9 server: Alter conditions in is_queue_hung(), again.
514acc47ca server: Create eventfd descriptors for console_input_events objects.
81cf57aef6 ntdll: Go through the server if necessary when performing event/semaphore/mutex ops.
116c9d6bdd kernel32/tests: Add some tests for wait timeouts.
70d08f34d1 kernel32/tests: Add some mutex tests.
f7971be236 kernel32/tests: Add some event tests.
edba7fe507 kernel32/tests: Add some semaphore tests.
2f04931404 kernel32/tests: Mark some existing tests as failing under esync.
5acffc9720 esync: Update README.
9e872eff42 server, ntdll: Implement alertable waits.
df9df05bdb server, ntdll: Pass the shared memory index back from get_esync_fd.
dfe91edd06 ntdll: Lock creating and opening objects with volatile state.
68814f7005 ntdll: Use shared memory segments to store semaphore and mutex state.
aa4406c4da server: Allocate shared memory segments for semaphores and mutexes.
3f268381ef server: Create eventfd descriptors for timers.
d77c90403c ntdll, server: Allow DuplicateHandle() to succeed by implementing esync_get_esync_fd().
e36c544654 server: Alter conditions in is_queue_hung().
48b84dcc4e server: Implement esync_map_access().
9867348c30 ntdll: Record the current count of a semaphore locally.
6408b4b38c ntdll: Implement NtOpenMutant().
90a8e72b9d ntdll: Implement NtOpenEvent().
ec0e8494c6 ntdll, server: Implement NtOpenSemaphore().
1ae7b2d1b6 server, ntdll: Also store the esync type in the server.
03bc93a6c6 ntdll: Implement NtSignalAndWaitForSingleObject().
4ef202694f esync: Add a README.
33aa029c36 ntdll: Implement wait-all.
b8232599eb ntdll: Implement waiting on mutexes.
3c46142728 ntdll: Implement NtReleaseMutant().
6fff0717e8 ntdll: Create esync objects for mutexes.
9208f0ee4f server: Create eventfd descriptors for device manager objects.
c9cf5e414a server, ntdll: Also wait on the queue fd when waiting for driver events.
0f03b23191 ntdll, wineandroid.drv, winemac.drv, winex11.drv: Store the thread's queue fd in ntdll.
5f5f8df31b server: Create eventfd file descriptors for message queues.
cae43f25a9 rpcrt4: Avoid closing the server thread handle while it is being waited on.
313d41923a server: Create eventfd file descriptors for thread objects.
ac8a776667 ntdll: Try again if poll() returns EINTR.
78ea0e7b39 server: Allow (re)setting esync events on the server side.
bec3538ac7 server: Create eventfd file descriptors for event objects.
f0da1e702e ntdll, server: Implement waiting on server-bound objects.
113a3e44cf server: Create eventfd file descriptors for process objects.
f439667136 server: Add a request to get the eventfd file descriptor associated with a waitable handle.
93716b1282 server: Add an object operation to grab the esync file descriptor.
d77e77d0c0 ntdll: Implement waiting on events.
ca75c63126 ntdll: Implement NtPulseEvent().
8e5c187902 ntdll: Implement NtResetEvent().
9837be039e ntdll: Implement NtSetEvent().
e2253c867a ntdll: Create esync objects for events.
7b4abee3bf ntdll: Implement waiting on esync objects.
3f2c9b17ec ntdll: Close esync objects.
ac3edf0cfe ntdll: Implement NtReleaseSemaphore().
7d4d462efc ntdll: Store esync objects locally.
a3f5faf8f9 ntdll: Create eventfd-based objects for semaphores.
bbac68a893 server: Create server objects for eventfd-based synchronization objects.
b616987d26 configure: Check for sys/eventfd.h, ppoll(), and shm_open().
-> 971dc3c422 ntdll: Notice THREADNAME_INFO exceptions and set thread name on Linux
6cdbdae7e9 winex11: Fullscreen hack, handle multisample FBConfig.
e237641cd1 winex11: Fullscreen hack, attach a depth / stencil buffer when necessary.
-> f375f8dafa winex11.drv: Log more information about X errors
-> 59e3f7faf3 kernel32: Implement Set and GetThreadDescription
-> 134fa05a0e HACK: winex11.drv: Disable XIM by default
-> 68caf4ef0a winex11: Always load the indexed scissor functions
(staging ?) 6e4d4aefc3 xaudio2_7: Update ffmpeg usage for ffmpeg 4.0
(staging ?) 8caae1a0c4 xaudio2: Use ffmpeg to convert non-PCM formats
ef2ecf0f3c winex11: Set the scissor rect before doing fs hack blit
5483f4128b winex11: Use hacked fbo for drawing immediately After setting up fs hack
1f7d06d56b winex11: In FS hack, don't clear the front buffer during context setup
e07f2588f2 winex11: Set WM hints before setting FS state
d13af02716 winevulkan: Blit directly to swapchain images if possible
81f198f28e winevulkan: Implement fs hack
8efca5790f winevulkan: Track swapchains in VkDevice
cf9791c734 winevulkan: Wrap swapchain object
6dc193b560 winevulkan: Move FS hack functions out of thunk
b142c004fe Revert "winevulkan: Get rid of unused "phys_dev" field from VkDevice_T."
ac9cd627df wined3d: Support retrieving depth texture in GL texture callback
94b4e1e4fc wined3d: Implement wined3d_device_wait_idle().
3d4a261491 winevulkan: Add struct unwrappers for vrclient
50b26687ab d3d11: Add IWineD3D11Device interface.
517f0cc07f d3d11: Add IWineD3D11Texture2D interface.
98d5b35869 wined3d: Implement command stream callbacks.
0fce68f807 wined3d: Implement GL texture access callbacks.
-> a13270aea5 winedbg: When crash dialog is not shown, dump crash info to stderr
-> b902a1b789 xaudio2: Prefer native xaudio2 in 32-bit
-> 0400502cb3 HACK: wine.inf: Add native,builtin overrides for msvcrt DLLs
-> 3340c66267 HACK: Don't build winemenubuilder
-> a7542e9e27 wine.inf: Don't show crash dialog by default
e5f7b5460b HACK: user32: Replace Wine glass with generic window icon
-> bac899cd45 kernel32: Don't force-load Steam.dll
c569fbd676 HACK: winex11: Give fullscreen windows focus
d669b1e261 Frontbuffer blitting hack...
4cd1ae0e2c winex11.drv: Improved fullscreen hack
-> 15f05e3ee2 winex11.drv: Log errors that we pass on
ff8c17e8f9 user32: Correct monitor flags from EnumDisplayDevices
9b6e961506 user32: Return a more reasonable display DeviceID.
fa8f5f4221 winemac: Make GetMonitorInfo() give a different device name (\\.\DISPLAY<n>) to each monitor.
72e6e5880c user32: Implement EnumDisplayDevicesW() based on EnumDisplayMonitors() and GetMonitorInfoW().
37d3751b25 winex11: Make GetMonitorInfo() give a different device name (\.\DISPLAY<n>) to each monitor
b47f1b0fa8 gdi32: Also accept "\\.\DISPLAY<n>" devices names with <n> other than 1 as display devices.
-> 81be78aa53 HACK: wineboot: Don't show "updating prefix" window
-> ec9e7190ea HACK: shell32: Never create links to the user's home dirs
819b923a3b HACK: advapi32: Use steamuser as Wine username
888a35da8e dinput: implement DISFFC_PAUSE/DISFFC_CONTINUE for SDL
8a7f8a41b2 dinput: Implement FF effects for SDL joysticks
30257203d3 dinput: Implement GetEffectInfo, SendForceFeedbackCommand and EnumCreatedEffectObjects
6ef7ecf144 dinput: Begin SDL haptic implemeting Get/SetProperty
337ef7e8ca dinput: Add SDL support
-> a2f9e2806a kernel32: Support steamclient64
-> aa88eb017b loader: Set up Steam stuff in the registry
-> 3835eee939 HACK: kernel32: Put Steam program files dir into PATH
-> 183eac81ab HACK: kernel32: Return steamclient instead of lsteamclient during GetModuleHandleEx
-> acda0915ca HACK: kernel32: Load hard-coded Steam.dll path if relative load fails
-> a277e32030 HACK: kernel32: Swap requests for steamclient.dll with lsteamclient
-> 7bd039f34f HACK: ws2_32: Fake success when trying to bind to an IPX address
-> bc614834ee HACK kernel32: Substitute the current pid for the Steam client pid
```
