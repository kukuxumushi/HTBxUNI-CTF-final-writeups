# Confirmation of Identity
We get a PE file idconfirm.exe. After analyzing the program, we can see, that it is simply read the HKEY_CURRENT_USER\Control Panel\Desktop\Wallpaper key, take the filename and extension from it, do some checks and decrypt flag, if the checks pass.

To complete this task, we can run the program under debugger and do some patches while program execution.

The patches we need:
1. Patch value on [ebp+var_1f0] to zero to continue program execution.
![](pictures/2021-03-26-23-14-00.png)
After patch:
![](pictures/2021-03-26-23-14-47.png)

2. Patch the return value of IsDebuggerPresent function to zero.
![](pictures/2021-03-26-23-14-57.png)

3. Patch the value in [ebp+pbDebuggerPresent] to zero to bypass debugger check.
![](pictures/2021-03-26-23-15-04.png)

4. Patch the string on stack that ecx points to “\proof” string to make a strcmp function to return zero and to properly decrypt our flag.
![](pictures/2021-03-26-23-15-10.png)
After patch:
![](pictures/2021-03-26-23-15-16.png)

After that patches, program will decrypt a flag and return it to us:

![](pictures/2021-03-26-23-15-24.png)