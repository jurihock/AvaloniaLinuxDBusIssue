# AvaloniaLinuxDBusIssue

Minimal example to reproduce the Avalonia DBus issue on Linux using the official Avalonia documentation:

- create an Avalonia app
- add a context menu
- forward logs to console
- finally run the app

## Create basic Avalonia app

https://docs.avaloniaui.net/docs/get-started/create-your-first-project#create-the-project

```
dotnet new avalonia.app -o AvaloniaLinuxDBusIssue
```

## Add sample context menu

https://docs.avaloniaui.net/controls/menus/contextmenu

```xml
<Window>

  <TextBox AcceptsReturn="True" TextWrapping="Wrap" Text="Right-click here">
    <TextBox.ContextMenu>
      <ContextMenu>
        <MenuItem Header="Copy"/>
        <MenuItem Header="Paste"/>
      </ContextMenu>
    </TextBox.ContextMenu>
  </TextBox>

</Window>
```

## Add logging callback

https://docs.avaloniaui.net/docs/app-development/logging-errors-and-warnings#logtodelegate

```csharp
public static AppBuilder BuildAvaloniaApp()
    => AppBuilder.Configure<App>()
        // ...
        .LogToDelegate(Console.WriteLine);
```

## Run AvaloniaLinuxDBusIssue

https://docs.avaloniaui.net/docs/get-started/create-your-first-project#run-the-project

```
cd AvaloniaLinuxDBusIssue
dotnet run
```

### Expected behavior

We see the context menu after right click.

### Actual behavior

```
[IME] Error while destroying the context:
Tmds.DBus.Protocol.DBusException: org.freedesktop.DBus.Error.UnknownMethod: Method Destroy is not implemented on interface org.freedesktop.IBus.Service
   at Tmds.DBus.Protocol.InnerConnection.MyValueTaskSource`1.System.Threading.Tasks.Sources.IValueTaskSource.GetResult(Int16 token)
   at Tmds.DBus.Protocol.InnerConnection.CallMethodAsync(MessageBuffer message)
   at Tmds.DBus.Protocol.DBusConnection.CallMethodAsync(MessageBuffer message)
   at Avalonia.FreeDesktop.DBusIme.DBusTextInputMethodBase.Dispose() (IBusX11TextInputMethod #45933772)
[IME] Error:
Tmds.DBus.Protocol.DBusException: org.freedesktop.DBus.Error.UnknownMethod: Object does not exist at path “/org/freedesktop/IBus/InputContext_485”
   at Tmds.DBus.Protocol.InnerConnection.MyValueTaskSource`1.System.Threading.Tasks.Sources.IValueTaskSource.GetResult(Int16 token)
   at Tmds.DBus.Protocol.InnerConnection.CallMethodAsync(MessageBuffer message)
   at Tmds.DBus.Protocol.DBusConnection.CallMethodAsync(MessageBuffer message)
   at Avalonia.FreeDesktop.DBusIme.IBus.IBusX11TextInputMethod.SetCapabilitiesCore(Boolean supportsPreedit, Boolean supportsSurroundingText)
   at Avalonia.FreeDesktop.DBusIme.DBusTextInputMethodBase.<>c__DisplayClass40_0.<<UpdateCapabilities>b__0>d.MoveNext()
--- End of stack trace from previous location ---
   at Avalonia.FreeDesktop.DBusCallQueue.Process() (IBusX11TextInputMethod #45933772)
[IME] Error while destroying the context:
Tmds.DBus.Protocol.DBusException: org.freedesktop.DBus.Error.UnknownMethod: Object does not exist at path “/org/freedesktop/IBus/InputContext_485”
   at Tmds.DBus.Protocol.InnerConnection.MyValueTaskSource`1.System.Threading.Tasks.Sources.IValueTaskSource.GetResult(Int16 token)
   at Tmds.DBus.Protocol.InnerConnection.CallMethodAsync(MessageBuffer message)
   at Tmds.DBus.Protocol.DBusConnection.CallMethodAsync(MessageBuffer message)
   at Avalonia.FreeDesktop.DBusIme.DBusTextInputMethodBase.QueueOnErrorAsync(Exception e) (IBusX11TextInputMethod #45933772)
```
