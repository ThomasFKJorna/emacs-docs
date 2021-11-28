---
slug: Windows-Startup
---

There are several ways of starting Emacs on MS-Windows:

1.  From the desktop shortcut icon: either double-click the left mouse button on the icon, or click once, then press `RET`. The desktop shortcut should specify as its “Target" (in the “Properties" of the shortcut) the full absolute file name of `runemacs.exe`, *not* of `emacs.exe`. This is because `runemacs.exe` hides the console window that would have been created if the target of the shortcut were `emacs.exe` (which is a console program, as far as Windows is concerned). If you use this method, Emacs starts in the directory specified by the shortcut. To control where that is, right-click on the shortcut, select “Properties", and in the “Shortcut" tab modify the “Start in" field to your liking.
2.  From a task-bar shortcut icon, by clicking once the left mouse button. Windows versions since Vista allow you to create such shortcuts by *pinning* the icon of a running program that appears in the task bar. You can do that with Emacs, but afterwards you will have to change the properties of the pinned shortcut to run `runemacs.exe`, *not* of `emacs.exe`. You can also pin Emacs to the task bar by clicking the right mouse button on its icon in the Start menu, then selecting ‘`Pin to taskbar`’. Once again, be sure to specify `runemacs.exe` as the program to run. You can control where Emacs starts by setting the “Start in" field of the shortcut’s Properties.
3.  From the Command Prompt window, by typing `emacs RET` at the prompt. The Command Prompt window where you did that will not be available for invoking other commands until Emacs exits. In this case, Emacs will start in the current directory of the Windows shell.
4.  From the Command Prompt window, by typing `runemacs RET` at the prompt. The Command Prompt window where you did that will be immediately available for invoking other commands. In this case, Emacs will start in the current directory of the Windows shell.
5.  From the Windows `Run` dialog (normally reached by clicking the `Start` button). Typing `runemacs RET` into the dialog will start Emacs in the parent directory of the Windows equivalent of your user’s `HOME` directory, see [Windows HOME](Windows-HOME).
6.  Via `emacsclient.exe` or `emacsclientw.exe`, which allow you to invoke Emacs from other programs, and to reuse a running Emacs process for serving editing jobs required by other programs. See [Emacs Server](Emacs-Server). The difference between `emacsclient.exe` and `emacsclientw.exe` is that the former is a console program, while the latter is a Windows GUI program. Both programs wait for Emacs to signal that the editing job is finished, before they exit and return control to the program that invoked them. Which one of them to use in each case depends on the expectations of the program that needs editing services. If that program is itself a console (text-mode) program, you should use `emacsclient.exe`, so that any of its messages and prompts appear in the same command window as those of the invoking program. By contrast, if the invoking program is a GUI program, you will be better off using `emacsclientw.exe`, because `emacsclient.exe` will pop up a command window if it is invoked from a GUI program. A notable situation where you would want `emacsclientw.exe` is when you right-click on a file in the Windows Explorer and select “Open With" from the pop-up menu. Use the ‘`--alternate-editor=`’ or ‘`-a`’ options if Emacs might not be running (or not running as a server) when `emacsclient` is invoked—that will always give you an editor. When invoked via `emacsclient`, Emacs will start in the current directory of the program that invoked `emacsclient`.

Note that, due to limitations of MS-Windows, Emacs cannot have both GUI and text-mode frames in the same session. It also cannot open text-mode frames on more than a single *Command Prompt* window, because each Windows program can have only one console at any given time. For these reasons, if you invoke `emacsclient` with the `-c` option, and the Emacs server runs in a text-mode session, Emacs will always create a new text-mode frame in the same *Command Prompt* window where it was started; a GUI frame will be created only if the server runs in a GUI session. Similarly, if you invoke `emacsclient` with the `-t` option, Emacs will create a GUI frame if the server runs in a GUI session, or a text-mode frame when the session runs in text mode in a *Command Prompt* window. See [emacsclient Options](emacsclient-Options).